---
title: Rétrospective 3
#date: 2023-12-6
hide_summary: true
toc_hide: true
---
## Rétrospective de l'itération 3

Date: 6 décembre 2023

## 1. Travail réalisé

| Tâche                                                                                                                                                          | Responsable       |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- |
| [Déploiement de cert-manager (ou equiv) dans le ns système](https://github.com/ClubCedille/Plateforme-Cedille/issues/26)                                       | Antoine           |
| [Mayastor Documentation](https://github.com/ClubCedille/Plateforme-Cedille/issues/24)                                                                          | Michael           |
| [Documenter la configuration d'environnement locale avec Omni](https://github.com/ClubCedille/Plateforme-Cedille/issues/19)                                    | Antoine           |
| [Documenter Kuma et Merbridge](https://github.com/ClubCedille/Plateforme-Cedille/issues/29)                                                                    | Thomas            |
| [Configure OTEL](https://github.com/ClubCedille/Plateforme-Cedille/issues/60)                                                                                  | Thomas            |
| [Tracking Clickhouse with Open Telemetry](https://github.com/ClubCedille/Plateforme-Cedille/issues/63)                                                         | Thomas            |
| [Déployer un sample de Grav avec configuration git-sync](https://github.com/ClubCedille/Plateforme-Cedille/issues/97)                                          | Simon et Jonathan |
| [Déploiement de Calidum-Rotae](https://github.com/ClubCedille/Plateforme-Cedille/issues/98)                                                                    | Jonathan et Thomas|
| [As SRE, I want to create nested span and I want to test and see the traces before going further](https://github.com/ClubCedille/Plateforme-Cedille/issues/83) | Thomas            |
| [As SRE, I want to update the README.md with the actual architecture](https://github.com/ClubCedille/Plateforme-Cedille/issues/71)                             | Thomas            |
| [As SRE, I want to remove the database (postgresql) from the project](https://github.com/ClubCedille/Plateforme-Cedille/issues/70)                             | Thomas            |
| [As SRE, I want to remove the phone number from the sender obj (protobuf)](https://github.com/ClubCedille/Plateforme-Cedille/issues/69)                        | Thomas            |
| [As SRE, I want to instrument the application with OTEL.](https://github.com/ClubCedille/Plateforme-Cedille/issues/68)                                         | Thomas            |

---

## 2. Travail non terminé

### 2.1 En cours

- **[Déploiement de cert-manager (ou equiv) dans le ns système](https://github.com/ClubCedille/Plateforme-Cedille/issues/26)** : 
- **[Documenter Vault](https://github.com/ClubCedille/Plateforme-Cedille/issues/69)** : 

### 2.2 Ne sera pas fait

- **[Installation/Configuration de k8s-sigs/external-dns dans le cluster](https://github.com/ClubCedille/Plateforme-Cedille/issues/35)** : 

### 2.3 À faire

- **[Deployer cluster staging [vcluster]](https://github.com/ClubCedille/Plateforme-Cedille/issues/6)** :
- **[Deployer cluster sandbox [vcluster]](https://github.com/ClubCedille/Plateforme-Cedille/issues/7)** :
- **[Mayastor Backup](https://github.com/ClubCedille/Plateforme-Cedille/issues/23)** :
- **[Installation plugin Vault+ArgoCD](https://github.com/ClubCedille/Plateforme-Cedille/issues/103)** :
- **[Update ArgoCD and Grafana SSO secrets with vault](https://github.com/ClubCedille/Plateforme-Cedille/issues/110)** : Nous étions en attente que le déploiement de vault dans le cluster soit terminés avec un exemple de configuration et gestion de secret pour pouvoir accomplir cette tâche. Elle pourra maintenant être complété avec des nouveaux secrets générés.
- **[Documenter OTEL (configuration du collecteur et operateur)](https://github.com/ClubCedille/Plateforme-Cedille/issues/121)** : Maintenant que la configuration de OTEL avec un exemple de déploiement est complété, on va pouvoir documenter comment la configuration à été effectuée.

---

## 3. Problèmes et défis

- **Problème 1** : Déploiement du service Calidum-rotae pour la démonstration de OTEL sur le cluster de production partiellement fonctionnel. 50% des requêtes étaient acheminées.
  - **Cause** : Le service communique avec un service api qui reçoit des requêtes http et les envois dans un channel discord à l'aide d'une webhook. Nous avons réalisé que le problème est externe au service 
  Calidum-rotae et provient du service API qui est déployé sur un autre cluster kubernetes.
  - **Solution** : Configuration d'une webhook discord directement avec l'application au lieu du service API comme solution temporaire jusqu'à temps que le problème de réception de requêtes soit régler avec l'API.

---