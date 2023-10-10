---
title: Rétrospective 1
description: Documentation et analyse des rétrospectives de chaque sprint.
date: 2023-10-09
toc_hide: true
hide_summary: true
---
# Rétrospective d'Itération

Date: 11 octobre 2023

## 1. Travail réalisé

| Tâche | Responsable | Statut | Commentaires |
|-------|-------------|--------|--------------|
| Preparer les questionnaires par client | Jonathan / Thomas | Complété |  |
| Entrevue AlgoETS | Jonathan | Complété |  |
| Entrevue des membres du club | Thomas / Jonathan | Complété |  |
| Entrevue club Raconteurs d'angles | Jonathan | Complété |  |
| Entrevue club Saveurs de génie | Jonathan | Complété |  |
| Entrevue services TI | Thomas | Complété |  |
| À partir des entrevues, définir métriques de succès | Jonathan / Thomas / Simon / Michael | Complété |  |
| Deployer le cluster physique avec Talos/Omni | Michael / Simon  | Complété |  |
| Configuration de base de rook/ceph | Michael / Simon | Complété |  |
| Evaluer stack networking k8s | Simon | Complété |  |
| Mise en place d'un wiki pour la documentation | Jonathan | Complété |  |
| Rédaction initiale du document de vision | Jonathan / Thomas / Simon / Michael | Complété |  |
| Migrer les serveurs physiques vers la salle de serveurs | Simon / Jonathan / Thomas | Complété |  |
| Configuration de KubeVirt | Thomas | Complété |  |


## 2. Travail non terminé

### 2.1 En cours
- **Achat des nouveaux disques** : L'évaluation de nos besoins a été complétée, la requête au TI est sur le point d'être envoyée.

### 2.2 Ne sera pas fait
- **Ajouter le networking pour le provider terraform XCP-NG** : Raison pour laquelle la tâche n'a pas été réalisée.

## 3. Problèmes et défis
- **Configuration d'un ISO/image dans un PVC pour KubeVirt**: Utiliser un ISO ubuntu dans un PVC pour l'utiliser comme CD-ROM lors du boot de la VM.
    - **Solution** : Installer le [CDI](https://kubevirt.io/user-guide/operations/containerized_data_importer/) de KubeVirt qui permet d'importer des images disque depuis un serveur web ou un registre de conteneurs, de cloner des volumes persistants existants, et de télécharger des images disquPe locales, le tout vers un DataVolume. Bref, il simplifie et optimise l'utilisation des revendications de volumes persistants (PVCs) comme disques pour les machines virtuelles.
- **Problème 1** : Description détaillée du problème et de son impact.
    - **Solution envisagée** : Description de la solution ou des étapes pour résoudre le problème.
- **Défi 2** : Description du défi et pourquoi il a été un obstacle.
    - **Solution envisagée** : Mesures ou étapes pour surmonter ce défi à l'avenir.

---

