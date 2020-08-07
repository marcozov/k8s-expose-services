# PoC Kubernetes Ingress Controller

Steps to easily deploy and configure a PoC Ingress Controller.

## Namespace
Create the namespaces involved in this PoC: `kubectl apply -f namespace.yaml`.

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

## Run an interactive curl image
This can be a quick way to check whether a service is reachable within the Kubernetes cluster.

`kubectl -n mzo-app-space run curl --rm -i --tty --image curlimages/curl -- sh`

### TLS
- Create key + certificate: `openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ${KEY_FILE} -out ${CERT_FILE} -subj "/CN=${HOST}/O=${HOST}"`
- Create a tls secret: `kubectl -n mzo-app-space create secret tls ${CERT_NAME} --key ${KEY_FILE} --cert ${CERT_FILE}`
- Create CA Key + certificate: `openssl req -x509 -sha256 -newkey rsa:4096 -keyout ca.key -out ca.crt -days 356 -nodes -subj '/CN=My Cert Authority'`
- Server Key, Server certificate, sign the certificate with the CA Certificate:
```$xslt
openssl req -new -newkey rsa:4096 -keyout server.key -out server.csr -nodes -subj '/CN=mydomain.com'
openssl x509 -req -sha256 -days 365 -in server.csr -CA ca.crt -CAkey ca.key -set_serial 01 -out server.crt
```
- Client Key, Client certificate, sign the certificate with the CA Certificate:
```$xslt
openssl req -new -newkey rsa:4096 -keyout client.key -out client.csr -nodes -subj '/CN=My Client'
openssl x509 -req -sha256 -days 365 -in client.csr -CA ca.crt -CAkey ca.key -set_serial 02 -out client.crt
```

### Redis
A separate folder was created for this application.
