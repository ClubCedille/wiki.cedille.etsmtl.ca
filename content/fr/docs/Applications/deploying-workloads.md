---
title: Déployer des applications
---

## Application exemplaire (httpbin)

L'application d'exemple est mise en place afin de documenter la méthodologie qui devrait être utilisé pour déployer des application en production avec Kustomize et ArgoCD.

- Code source: [/apps/samples/kustomize-example-app](https://github.com/ClubCedille/Plateforme-Cedille/tree/master/apps/samples/kustomize-example-app)

## Fonctionnement avec Kustomize

### Base

Chaque application devrait definir un dossier `base` qui contient toutes les ressources Kubernetes que l'application aurait besoin. Ce dossier doit aussi contenir un Kustomization qui pointe sur toute les fichiers Kubernetes de `base`:
```yaml
# base/Kustomization.yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization

resources:
  - network.yaml
  - deployment.yaml
```

### Envrionments

Ensuite, il faut définir les dossiers `prod` et `staging` qui auront comme objectif de modifier des propriétés dans `base` selon les besoins différents et d'ajouter des ressources qui ne seront pas communs a toutes les environments.

Par exemple, voici le fonctionnement pour `prod`:
```yaml
# prod/kustomization.yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization

resources:
  - ../base
  - ingress.yaml
  - dns.yaml

patches:
  - path: patch.yaml
```

Dans l'extrait ci-haut:
1. On inclut le base
2. On inclut les ressources 
3. On applique des `patches`:


```yaml
# prod/patches.yaml
# [...]
      replicas: 3
      containers:
      - name: httpbin
        resources:
          requests:
            cpu: "0.1"
            memory: "256Mi"
---
# On peut mettre d'autres patches avec des séparateurs ---
---
```
On voit qu'ici on applique des requêtes de ressources qui seront différents de `base`

### Structure Globale

```
$ kustomize cfg tree .
──── base
  │  ├── [deployment.yaml]  Deployment httpbin
  │  ├── [kustomization.yaml]  Kustomization
  │  └── [network.yaml]  Service httpbin
  ├── prod
  │   ├── [dns.yaml]  RecordSet prod-dns-record
  │   ├── [ingress.yaml]  Ingress httpbin
  │   ├── [kustomization.yaml]  Kustomization
  │   └── [patch.yaml]  Deployment httpbin
  └── staging
      ├── [dns.yaml]  RecordSet staging-dns-record
      ├── [ingress.yaml]  Ingress httpbin
      ├── [kustomization.yaml]  Kustomization
      └── [patch.yaml]  Deployment httpbin
```
