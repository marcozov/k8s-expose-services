# Mock webserver

This is to deploy a simple web service and expose it to external clients.

## Namespace
 - app namespace: `kubectl create ns mzo-app-space`
 - ingress namespace: `kubectl create ns mzo-ingress-space`

## Service account

To create the service account: `kubectl create sa ingress-serviceaccount -n mzo-ingress-space`.

## Roles and role bindings
 - roles: `kubectl apply -f ingress-role.yaml`
 - bindings: `kubectl apply -f ingress-role-binding.yaml`

## Applications

Deploy the two applications:
 - webapp video app: `kubectl apply -f webapp-video.yaml`
 - webapp wear app: `kubectl apply -f webapp-wear.yaml`
 - default backend app: `kubectl apply -f default-backend.yaml`


## Services
The deployments must be exposed:
 - `kubectl apply -f kubectl apply -f webapp-wear-service.yaml`
 - `kubectl apply -f kubectl apply -f webapp-video-service.yaml`
 - `kubectl apply -f kubectl apply -f default-http-backend-service.yaml`

## Config Map

`kubectl apply -f config_map.yaml`

## Ingress Controller
Setting up the ingress controller: `kubectl apply -f ingress-controller.yaml`.

## Ingress Service
Exposing the controller: `kubectl apply -f ingress-service.yaml`.

## Ingress Resource
Make sure that each path provides the right application: `kubectl apply -f ingress-resource.yaml`.

