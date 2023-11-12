---
title: Gestion des secrets avec Vault
date: 2023-11-12
weight: 1
type: "docs"
---

## Mise en contexte

HashiCorp Vault est un outil open source conçu pour la gestion centralisée des secrets et des identités dans un environnement informatique. Il fournit un moyen sécurisé de stocker, gérer et contrôler l'accès à divers types d'informations sensibles, tels que des mots de passe, des clés d'API, des certificats, des jetons d'accès, et d'autres données confidentielles. L'une des fonctionnalités clés de Vault est la gestion des secrets dynamiques, qui génère des secrets à la demande plutôt que de les stocker statiquement.

Pour comprendre comment HashiCorp Vault s'intègre dans une infrastructure applicative roulant dans Kubernetes, examinons les aspects principaux de son utilité :

### 1. **Stockage sécurisé des secrets :**
   - **Centralisation :** Vault permet de centraliser la gestion des secrets, évitant ainsi la dispersion d'informations sensibles dans différents fichiers de configuration ou bases de données.
   - **Chiffrement :** Tous les secrets stockés dans Vault sont chiffrés, ce qui garantit une protection adéquate des données sensibles.

### 2. **Gestion des identités et des accès :**
   - **Contrôle d'accès :** Vault offre un contrôle d'accès granulaire, permettant de définir qui peut accéder à quel secret. Cela est essentiel pour garantir que seules les applications et les utilisateurs autorisés ont accès aux informations sensibles.
   - **Authentification :** Vault prend en charge plusieurs méthodes d'authentification, telles que les jetons, les certificats, l'authentification LDAP, etc., permettant de s'intégrer facilement dans des environnements variés.

### 3. **Secrets dynamiques :**
   - **Génération à la demande :** Vault peut générer des secrets à la demande, ce qui signifie qu'il peut créer des paires de clés, des mots de passe, etc., au moment de la demande. Cela renforce la sécurité en réduisant la durée de vie des secrets.

### 4. **Intégration avec Kubernetes :**
   - **Authentification Kubernetes :** Vault peut s'authentifier auprès d'un cluster Kubernetes, ce qui permet aux applications s'exécutant dans ce cluster d'accéder aux secrets stockés dans Vault.
   - **Dynamic Secrets pour Kubernetes :** Vault peut générer des secrets spécifiques à une application s'exécutant dans un pod Kubernetes. Ces secrets sont automatiquement renouvelés et révoqués après utilisation, renforçant la sécurité.

### 5. **Audit et suivi :**
   - **Journalisation :** Vault propose une journalisation détaillée de toutes les opérations, ce qui facilite l'audit des accès aux secrets et le suivi des changements.

En résumé, HashiCorp Vault offre une solution robuste et flexible pour la gestion des secrets dans un environnement Kubernetes, répondant aux besoins de sécurité et de conformité des applications déployées dans des clusters conteneurisés.

## Architecture

![Architecture Vault](./vault.drawio.svg)


## Comment déployer

Le déploiement de Vault est plus complexe que la plupart des modules déployés dans la configuration système, notamment la configuration
de certfificats et de GCP KMS qui sont des opérations externes à Kubernetes. Pour automatiser ces opérations, un module terraform a été
créé et devrait être déployé (`terraform/vault`). Celui-ci génère un fichier de configuration helm (`system/vault/helm/vault.values.yaml`) à partir
d'un template (`terraform/vault/overrides-values.yaml.tmpl`), des ressources clouds créés ainsi que des certificats générés. ATTENTION: il faut modifier le template et non le fichier généré, puis le commit. Sinon les changements effectués pourraient se retouvés perdus.

Pour débuter, suivre les instructions pour appliquer les configurations terraform: **REFERENCES MANQUANTES**.

Ensuite, s'assurer que vault est déployé en utilisant ArgoCD: **REFERENCES MANQUANTES**. Les pods devraient être `running`, mais pas `healthy`. Si ils sont en `CrashLoopBackoff`, supprimer les pods pour que de nouveaux soient créés. Par la suite, il faut se connecter au premier pod et initialiser le cluster: `kubectl exec -it -n vault pods/vault-0 -- vault operator init`. La commande va retourner des *recovery keys*. Garder ces valeurs précieusement en backup; au cas ou GCP KMS ne fonctionne plus ou est supprimé par accident ceci pourra être utilisé pour *unseal* Vault. Un *initial root key* sera aussi créé, conservez-la pour vous permettre de vous connecter avant de créer des utilisateurs additionnels.

Vous pouvez ensuite lancer le UI en faisant `kubectl -n vault port-forward vault-ui 8200` et en allant à https://localhost:8200. Utilisez le *initial root token* pour vous connecter. 

Tout d'abord, ajouter un *policy*: `Policies > Create ACL policy`. Mettez `config-admin` pour le *Name* et la policy correspodante à ce nom (voir `system/vault/configs/policy.yaml`). Au moment d'écrire ces lignes, il s'agit de:

```hcl
path "sys/*" {
  capabilities =  ["create", "read", "update", "delete", "list"]
}

path "auth/*" {
  capabilities =  ["create", "read", "update", "delete", "list"]
}
```

Ensuite, allez activer l'authentification Kubernetes: `Access > Authentication Methods > Enable new method > Kubernetes > Enable method`. Retourner à la méthode que vous venez de créer: `Access > Authentication Methods > Kubernetes`. Cliquez sur `create role` et mettez les valeurs suivantes:
```
Name: config-admin
Alias Name Source: serviceaccount_uid
Bound service account names: default
Bound service account namespaces: vault
Tokens >  Generated Token's Policies: config-admin
```
Cliquez sur save.

Si vous utilisez argoCD, les configurations devraient s'appliquer automatiquement. si ce n'est pas le cas, recréer `system/vault/config/argo.yaml`.

