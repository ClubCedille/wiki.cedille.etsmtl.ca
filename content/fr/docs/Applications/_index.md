---
title: Applications
weight: 5
description: >
  Présente tous nos déploiements que l'on héberge
---

# Application existantes

## Système

### ArgoCD

ArgoCD est notre système de GitOps. Il s'occupe de déployer et synchronizer toutes les ressources YAML dans notre repértoire `Plateforme-Cedille`. Pour le faire, on utiliser Kustomize pour regrouper toutes les ressources de type `Application` dans le dossier `/apps/argo-apps/`.

Voici un apercu visuel de cette structure:

TODO: Insérer graphique.

### Ingress - Contour

Contour est une solution d'Ingress Controller pour Kubernetes. Elle utilise le serveur proxy Envoy comme back-end.

#### Configuration 

Le service proxy de Envoy à été configuré avec un Nodeport pour diriger le traffic externe vers contour qui achemine ensuite les requêtes vers les services dédiés. 

## Workloads

### apps/sample/kustomize-example-app

Application qui démontre la structure de base a prendre pour déployer une nouvelle application avec Kustomize avec des environments prod et staging.

Pour plus de détails, voir: [Déployer des applications](./deploying-workloads)

### Tester

Commencer par déployer une application web comme [httpbin](https://httpbin.org/#/). À partir du repertoire du projet :
```bash
kubectl apply -f apps/testing/httpbin.yaml
```
Vérifier ensuite que les 3 pods arrivent à un status **Running**: 
```bash
kubectl get po,svc,ing -l app=httpbin
```
Afin d'utiliser Contour et Envoy, on va utiliser la fonction `kubectl port-foward` pour diriger le traffic vers envoy :
```bash
kubectl -n projectcontour port-forward service/envoy 8888:80
```
Puis visiter http://local.projectcontour.io:8888/. Pour notre environnement de production, on utiliserait l'adresse du service de Envoy.

Pour plus d'informations sur Contour, consultez [la documentation officielle](https://projectcontour.io/docs/).