# PoC Kubernetes Ingress Controller

Steps to easily deploy and configure a PoC Ingress Controller.

### Namespace
Create the namespaces involved in this PoC: `kubectl apply -f namespace.yaml`.

### Service account

To create the service account: `kubectl create sa ingress-serviceaccount -n mzo-ingress-space`.

Or: `kubectl apply -f service-account.yaml`.

### Roles and role bindings
 - roles: `kubectl apply -f ingress-role.yaml`
 - bindings: `kubectl apply -f ingress-role-binding.yaml`

### Applications
Check the [applications subfolder](deployments).

### Services
Check the [services subfolder](services) for exposing the pods internally.

### Ingress
Check the [ingress subfolder](ingress) for exposing the internal services to external clients.

### Run an interactive curl image
This can be a quick way to check whether a service is reachable within the Kubernetes cluster.

- run the image: `kubectl -n mzo-app-space run curl --rm -i --tty --image curlimages/curl -- sh`
- reach a service: `curl echo-service.mzo-app-space.svc.cluster.local:500`.

### Redis
A separate [folder](redis) was created for this application.
