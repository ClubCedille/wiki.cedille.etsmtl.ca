---
title: Cluster Kubernetes
description: Les differents environnements au sein du cluster.
date: 2023-10-30
weight: 6
type: "docs"
---

# Cluster Kubernetes

Le cluster Kubernetes de la Plateforme Cédille héberge les sites web de tous les clubs étudiants de l'école, ainsi que les projets du club cédille. 

## Cluster hôte

Le cluster hôte héberge les services de système et infrastructures de base. Le cluster hôte est déployé sur les serveurs du club cédille. Le système d'exploitation utilisé est Talos Linux.

## V-Clusters pour chaque environment

Les environnements sont hébergés chacun sur un v-cluster hébergé par le cluster hôte., mais utilisent [vcluster](https://www.vcluster.com/) pour isoler les environnements dans des clusters virtuels séparés.

