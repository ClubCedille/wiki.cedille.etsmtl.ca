---
title: Rétrospective 2
#date: 2023-11-08
hide_summary: true
toc_hide: true
---
## Rétrospective de l'itération 2

Date: 8 novembre 2023

## 1. Travail réalisé

| Tâche                                                                                                                                              | Responsable                     |
| -------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- |
| [Deployer cluster staging (vcluster)](https://github.com/ClubCedille/Plateforme-Cedille/issues/6)                                                  | Antoine                         |
| [Deployer cluster sandbox (vcluster)](https://github.com/ClubCedille/Plateforme-Cedille/issues/7)                                                  | Antoine                         |
| [Installation/Configuration de k8s-sigs/external-dns dans le cluster](https://github.com/ClubCedille/Plateforme-Cedille/issues/35)                 | Michael                         |
| [Deployer/Configurer Hashicorp Vault](https://github.com/ClubCedille/Plateforme-Cedille/issues/14)                                                 | Simon                           |
| [Déploiement de cert-manager (ou équivalent) dans le système](https://github.com/ClubCedille/Plateforme-Cedille/issues/26)                         | Antoine                         |
| [Acheter SSDs](https://github.com/ClubCedille/Plateforme-Cedille/issues/9)                                                                         | Thomas                          |
| [Installation/Configuration de Crossplane sur le cluster](https://github.com/ClubCedille/Plateforme-Cedille/issues/31)                             | Michael                         |
| [Creation de la structure Kustomize](https://github.com/ClubCedille/Plateforme-Cedille/issues/25)                                                  | Michael                         |
| [Configurer ArgoCD sur le cluster](https://github.com/ClubCedille/Plateforme-Cedille/issues/5)                                                     | Henri, Antoine, Simon, Jonathan |
| [Configuration de Contour (reverse-proxy/ingress)](https://github.com/ClubCedille/Plateforme-Cedille/issues/11)                                    | Jonathan                        |
| [Gabarit de pull request (PR) pour le repo Plateforme Cedille](https://github.com/orgs/ClubCedille/projects/3/views/5?pane=issue&itemId=41043072)  | Henri                           |
| [Gabarit de issues pour le repo Plateforme Cedille](https://github.com/orgs/ClubCedille/projects/3/views/5?pane=issue&itemId=41043078)             | Henri                           |
| [Configurer la gestion a distance des serveurs physiques](https://github.com/ClubCedille/Plateforme-Cedille/issues/16)                             |                                 |
| [Documenter le déploiement avec Omni](https://github.com/ClubCedille/Plateforme-Cedille/issues/17)                                                 |                                 |
| [Documenter la configuration d'environnement locale avec Omni](https://github.com/ClubCedille/Plateforme-Cedille/issues/19)                        | Jonathan                        |
| [Deployer/Configurer Kuma + Merbridge (service-mesh)](https://github.com/ClubCedille/Plateforme-Cedille/issues/20)                                 | Thomas                          |
| [Configurer/Deployer grafana](https://github.com/ClubCedille/Plateforme-Cedille/issues/21)                                                         | Thomas                          |
| [Configuration des routes sur Talos](https://github.com/orgs/ClubCedille/projects/3/views/5?pane=issue&itemId=41582552)                            |                                 |
| [Configurer et deployer Gateway API](https://github.com/ClubCedille/Plateforme-Cedille/issues/27)                                                  | Thomas                          |
| [Deployer et configurer Mayastor](https://github.com/ClubCedille/Plateforme-Cedille/issues/33)                                                     |                                 |
| [Documenter KubeVirt](https://github.com/ClubCedille/Plateforme-Cedille/issues/28)                                                                 | Thomas                          |
| [Documenter Kuma et Merbridge](https://github.com/ClubCedille/Plateforme-Cedille/issues/29)                                                        | Thomas                          |
| [Documenter Contour](https://github.com/ClubCedille/Plateforme-Cedille/issues/30)                                                                  | Jonathan                        |
| [Résoudre les problèmes de stabilité Rook/Ceph](https://github.com/ClubCedille/Plateforme-Cedille/issues/34)                                       |                                 |
| [clickhouse operator with sample application](https://github.com/ClubCedille/Plateforme-Cedille/issues/37)                                         | Thomas                          |
| [Configure argocd-lovely-plugin](https://github.com/ClubCedille/Plateforme-Cedille/issues/42)                                                      | Simon                           |
| [Configurer/Deployer clickhouse](https://github.com/ClubCedille/Plateforme-Cedille/issues/58)                                                      | Thomas                          |
| [Configurer OTEL](https://github.com/ClubCedille/Plateforme-Cedille/issues/60)                                                                     | Thomas, Jonathan                |
| [Configure RBAC for grafana and argoCD](https://github.com/ClubCedille/Plateforme-Cedille/issues/61)                                               | Jonathan                        |
| [Configure SSO for argocd and grafana](https://github.com/ClubCedille/Plateforme-Cedille/issues/62)                                                | Jonathan                        |
| [Configurer/Deployer Linkerd](https://github.com/ClubCedille/Plateforme-Cedille/issues/32)                                                         | Thomas                          |

---

## 2. Travail non terminé

### 2.1 En cours

- **[Configurer et deployer Gateway API #27](https://github.com/ClubCedille/Plateforme-Cedille/issues/27)** : La configuration de la Gateway API est actuellement en développement.
- **[Déployer et configurer Mayastor #33](https://github.com/ClubCedille/Plateforme-Cedille/issues/33)** : L'intégration de Mayastor pour le stockage est en cours de déploiement.
- **[Configurer OTEL #60](https://github.com/ClubCedille/Plateforme-Cedille/issues/60)** : La configuration de l'OpenTelemetry Collector est en cours pour permettre la collecte et l'exportation des données de télémétrie.

### 2.2 Ne sera pas fait

- **[Configurer/Deployer Linkerd #32](https://github.com/ClubCedille/Plateforme-Cedille/issues/32)** : Nous avons choisi de ne pas aller de l'avant avec Linkerd en tant que maillage de service pour le moment. Nous avons rencontrés des problèmes similaires à des issues ouvertes sur ce projet ([11156](https://github.com/linkerd/linkerd2/issues/11156) & [10994](https://github.com/linkerd/linkerd2/issues/10994)). Sans solution proposé, ont a decidé de se diriger vers une alternative (Kuma).

### 2.3 À faire

- **[Deployer cluster staging (vcluster) #6](https://github.com/ClubCedille/Plateforme-Cedille/issues/6)** & **[Deployer cluster sandbox (vcluster) #7](https://github.com/ClubCedille/Plateforme-Cedille/issues/7)** : Le déploiement du cluster de staging et sandbox avec vcluster est prévu.
- **[Documenter le déploiement avec Omni #17](https://github.com/ClubCedille/Plateforme-Cedille/issues/17)** : La documentation du processus de déploiement en utilisant Omni doit être créée.
- **[Documenter la configuration d'environnement locale avec Omni #19](https://github.com/ClubCedille/Plateforme-Cedille/issues/19)** : Il est nécessaire de documenter la configuration de l'environnement local pour Omni.
- **[Configuration des routes sur Talos #0](https://github.com/orgs/ClubCedille/projects/3/views/5?pane=issue&itemId=41582552)** : La configuration des routes pour le système d'exploitation Talos doit être mise en place.
- **[Configurer la gestion à distance des serveurs physiques #16](https://github.com/ClubCedille/Plateforme-Cedille/issues/16)** : Pour permettre à l'équipe d'intéragir avec les serveurs à distance.

---

## 3. Problèmes et défis

- **Problème 1** : Stabilité de Rook/Ceph. Le redémarrage d'un node rend le cluster ceph non-healthy. Les pods de ceph sur le serveurs associé ne finissent jamais leur processus de démarrage et ces disques ne sont jamais disponible.
  - **Cause** : Le problème semble être du au fait qu'un nouveau mon est créé puisque celui du node redémarré est mort. Puisqu'on ne permet pas la colocation de mon, il ne redémarre sur aucun autre serveur. Quand on redémarre sur le serveur on dirait que le nouveau et ancien mon se font compétition. Après une investigation approfondie, du au petit scale du cluster ceph (3 nodes), il semble y avoir une complexité et risque additionel.
  - **Solution** : Nous avons décidé que résoudre tous ces problèmes est trop de problèmes. Après une rapide preuve de concept, nous avons décidé de changer vers [Mayastor](https://openebs.io/docs/concepts/mayastor). Ce système est bati pour kubernetes à partir de 0, ce qui devrait réduire le genre de problèmes opérationnels rencontrés avec ceph. Voir #33 pour plus de détails.

- **Problème 2** : Configuration d'un service mesh pour kubernetes
  - **Cause** : TODO
  - **Solution** : TODO

- **Défi 1** : External-DNS
  - **Solution** : TODO

- **Défi 2** : Configuration du SSO pour ArgoCD sans gestion sécurisée des secrets. Nous avons rencontré un problème récurrent lors de la recréation des pods d'ArgoCD où les secrets nécessaires à la configuration du SSO ne pouvaient pas être conservés de manière sécurisée. La configuration initiale a été effectuée en utilisant le fichier `values` d'un Helm chart, incluant un token secret provenant de GitHub pour permettre l'authentification. Cependant, cela posait un problème de sécurité puisque le secret se retrouvait exposé sur GitHub lorsque le fichier `values` était sauvegardé. De plus, le secret devait être saisi à nouveau via `kubectl` à chaque fois que le namespace était recréé pour des raisons de débogage, ce qui ajoutait des tâches répétitives et fastidieuses à notre travail.
  
  - **Solution proposée** : Pour résoudre ce problème,  nous devons configuré le service Vault par HashiCorp, qui permettra de centraliser la gestion des secrets et de les injecter de manière sécurisée dans nos configurations sans les exposer dans notre dépôt GitHub. Cela réduirait considérablement les risques liés à la sécurité et optimiserait notre flux de travail en évitant la resaisie manuelle des secrets à chaque intervention sur l'infrastructure.

---
