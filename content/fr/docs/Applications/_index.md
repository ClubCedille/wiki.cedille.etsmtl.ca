---
title: Applications
weight: 5
description: >
  Présente tous nos déploiements que l'on héberge
---

## Contour

Contour est une solution d'Ingress Controller pour Kubernetes. Elle utilise le serveur proxy Envoy comme back-end.

### Configuration 

Le service proxy de Envoy à été configuré avec un Nodeport pour diriger le traffic externe vers contour qui achemine ensuite les requêtes vers les services dédiés. 

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