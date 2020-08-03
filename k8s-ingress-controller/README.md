# Mock webserver

This is to deploy a simple web service and expose it to external clients.

## Namespace
`kubectl apply -f namespace.yaml`

## Service account

To create the service account: `kubectl create sa ingress-serviceaccount -n mzo-ingress-space`.

Or: `kubectl apply -f service-account.yaml`.

## Roles and role bindings
 - roles: `kubectl apply -f ingress-role.yaml`
 - bindings: `kubectl apply -f ingress-role-binding.yaml`

## Applications

Deploy the two applications:
 - webapp video app: `kubectl apply -f deployments/webapp-video.yaml`
 - webapp wear app: `kubectl apply -f deployments/webapp-wear.yaml`
 - default backend app: `kubectl apply -f deployments/default-backend.yaml`


## Services
The deployments must be exposed:
 - `kubectl apply -f services/webapp-wear-service.yaml`
 - `kubectl apply -f services/webapp-video-service.yaml`
 - `kubectl apply -f services/default-http-backend-service.yaml`

## Config Map

`kubectl apply -f config-map.yaml`

## Ingress Controller
Setting up the ingress controller: `kubectl apply -f deployments/ingress-controller.yaml`.

## Ingress Service
Exposing the controller: `kubectl apply -f services/ingress-service.yaml`.

## Ingress Resource
Make sure that each path provides the right application: `kubectl apply -f ingress-resource.yaml`.

## Run a curl image
`kubectl -n mzo-app-space run ubuntu --rm -i --tty --image curlimages/curl -- sh`
