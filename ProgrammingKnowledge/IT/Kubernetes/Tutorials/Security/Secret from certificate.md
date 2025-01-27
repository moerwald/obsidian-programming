

```bash
# Extract the private key (key.pem)
openssl pkcs12 -in your-file.pfx -nocerts -nodes -out key.pem

# Extract the certificate (cert.pem)
openssl pkcs12 -in your-file.pfx -clcerts -nokeys -out cert.pem

# Extract the CA certificates (if any) (chain.pem)
openssl pkcs12 -in your-file.pfx -cacerts -chain -nokeys -out chain.pem
```

Create a K8S secret:

```bash
kubectl create secret tls your-tls-secret \
  --cert=fullchain.pem \
  --key=key.pem

```


#Security
#Certificates 
#Kubernetes 