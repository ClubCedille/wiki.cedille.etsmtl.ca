---
title: Cluster Kubernetes
description: Les differents environnements au sein du cluster.
date: 2023-10-30
weight: 6
---

{{% pageinfo %}}
Description des environnements au sein du cluster kubernetes de Cluster Cédille.
{{% /pageinfo %}}

# Cluster Kubernetes
Le cluster Kubernetes de la Plateforme Cédille héberge les sites web de tous les clubs étudiants de l'école, ainsi que les projets du club. Les environnements se trouvent tous sur le même cluster Kubernetes, mais utilisent [vcluster](https://www.vcluster.com/) pour isoler les environnements dans des clusters virtuels séparés.

## Environnements

### Production

L'environnement Production est utilisé pour héberger les services "live" de la plateforme, dans un état prêt à l'utilisation par les usagers finaux.

### Staging

L'environnement Staging est utilisé comme environnement de pré-production. Il sert à tester des changements avant qu'ils soient déployés dans l'environnement de production.

### Sandbox

Cet environnement est utilisé pour expérimenter librement sur le cluster. Les déploiements dans cet environnement n'ont pas d'objectif de fiabilité et peuvent être ajoutés, modifiés et retirés librement.