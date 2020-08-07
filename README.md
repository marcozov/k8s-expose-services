# Exposing Kubernetes services

This repository contains a PoC of different ingress controllers in order to expose services.

The goal is to setup different environments in order to get familiar with some available options
and being able to evaluate them properly.

## Ingress Controllers

 - [Kubernetes Ingress Controller](k8s-ingress-controller): The standard Kubernetes Ingress Controller, based on [NGINX](https://github.com/kubernetes/ingress-nginx).
 - [NGINX Ingress Controller](nginx-ingress-controller): The [NGINX Ingress Controller](https://github.com/nginxinc/kubernetes-ingress).
 - [HAProxy Ingress Controller](haproxy-ingress-controller): The [HAProxy Ingress Controller](https://github.com/jcmoraisjr/haproxy-ingress).
 - [Istio Ingress Gateway](istio-ingress-gateway): The ingress gateway provided by [Istio](https://istio.io/latest/docs/tasks/traffic-management/ingress/).
 - [Traefik Edge Router](traefik): [Traefik](https://docs.traefik.io/).
