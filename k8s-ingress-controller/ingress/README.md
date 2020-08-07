# Ingress

The manifests to configure the ingress controller, expose it,
and use it to expose services in the cluster to external clients.

## Config Map
The configuration of the controller: `kubectl apply -f config-map.yaml`.

## Ingress Controller
Setting up the ingress controller: `kubectl apply -f ingress-controller.yaml`.

## Ingress Service
Exposing the controller: `kubectl apply -f ingress-service.yaml`.

## Ingress Resource
Make sure that each path provides the right application: `kubectl apply -f ingress-resource.yaml`.

## Exposing additional services
Although Kubernetes Ingress only supports HTTP/HTTPS by default, it is possible to setup
a config map to allow arbitrary TCP traffic: `kubectl apply -f tcp-service-cm.yaml`.

Then, it has to be added to the ingress controller args:
`--tcp-services-configmap=$(POD_NAMESPACE)/tcp-services`.

Finally, the same port has to be exposed in the ingress service (the load balancer):
```
    - port: 500
      protocol: TCP
      name: "proxied-tcp-500"
      targetPort: 500
```

One debugging tip that proves quite useful is to check whether the ingress controller really gets
the ports configuration:
 - spawn a shell: `kubectl -n mzo-ingress-space exec -it $CONTROLLER_POD_ID -- bash`.
 - check `/etc/nginx/nginx.conf`. The new port should be found in the TCP (or UDP) services settings.

## Accessing the exposed services

The services in the related [folder](../services) must be deployed.

Then, the services can be accessed via the IP address assigned to the load balancer (the ingress service)
and the service port.


