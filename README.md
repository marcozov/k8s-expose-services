# Exposing Kubernetes services

This repository contains a PoC of different ingress controllers in order to expose services.

The following setups are deployed on AKS.

The goal of this repository is to share a starting point for setting up different ingress
controllers that have been tried out.

## Ingress Controllers

 - [Kubernetes Ingress Controller](k8s-ingress-controller): The standard Kubernetes Ingress Controller, based on [NGINX](https://github.com/kubernetes/ingress-nginx).
 - [NGINX Ingress Controller](nginx-ingress-controller): The [NGINX Ingress Controller](https://github.com/nginxinc/kubernetes-ingress).
 - [Istio Ingress Gateway](istio-ingress-gateway): The ingress gateway provided by [Istio](https://istio.io/latest/docs/tasks/traffic-management/ingress/).
 - [Traefik Edge Router](traefik): [Traefik](https://docs.traefik.io/).
