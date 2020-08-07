# TLS

### How-to
`kubectl -n mzo-app-space create secret tls test-cert --key ${KEY_FILE} --cert ${CERT_FILE}`

### Common TLS operations
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
