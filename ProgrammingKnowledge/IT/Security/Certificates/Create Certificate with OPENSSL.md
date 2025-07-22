
Here’s the complete, simplified flow using an external `leaf_ext.cnf` for your SANs. You’ll end up with:

- **rootCA.key** / **rootCA.pem**
    
- **inter.key** / **inter.pem**
    
- **leaf.key** / **leaf.crt**
    

---

### 1. Create the Root CA

```bash
# Generate root private key
openssl genrsa -out rootCA.key 4096

# Create a self-signed root certificate
openssl req -x509 -new -nodes \
  -key rootCA.key \
  -sha256 -days 3650 \
  -subj "/C=US/ST=YourState/L=YourCity/O=YourOrg/CN=My Root CA" \
  -out rootCA.pem
```

---

### 2. Create the Issuing (Intermediate) CA

```bash
# Generate intermediate private key
openssl genrsa -out inter.key 4096

# Create a CSR for the intermediate CA
openssl req -new \
  -key inter.key \
  -subj "/C=US/ST=YourState/L=YourCity/O=YourOrg/CN=My Issuing CA" \
  -out inter.csr

# Self-sign the intermediate CSR with root CA and embed CA extensions inline
openssl x509 -req \
  -in inter.csr \
  -CA rootCA.pem -CAkey rootCA.key -CAcreateserial \
  -sha256 -days 1825 \
  -extfile <(printf "\
basicConstraints=CA:TRUE,pathlen:0\n\
keyUsage=critical,keyCertSign,cRLSign\n\
subjectKeyIdentifier=hash\n\
authorityKeyIdentifier=keyid,issuer\n") \
  -out inter.pem
```

---

### 3. Create the Leaf Certificate (with SANs via `leaf_ext.cnf`)

First, ensure you have a `leaf_ext.cnf` alongside your keys/CSRs:

```ini
# leaf_ext.cnf
[ v3_req ]
basicConstraints     = CA:FALSE
keyUsage             = digitalSignature, keyEncipherment
extendedKeyUsage     = serverAuth, clientAuth
subjectAltName       = @alt_names

[ alt_names ]
DNS.1 = example.com
DNS.2 = www.example.com
IP.1  = 192.168.1.100
```

Then run:

```bash
# 1. Generate leaf private key
openssl genrsa -out leaf.key 2048

# 2. Create the CSR (no SANs here—it comes from leaf_ext.cnf)
openssl req -new \
  -key leaf.key \
  -subj "/C=US/ST=YourState/L=YourCity/O=YourOrg/CN=example.com" \
  -out leaf.csr

# 3. Sign the CSR with the intermediate CA, pulling in your SANs
openssl x509 -req \
  -in leaf.csr \
  -CA inter.pem -CAkey inter.key -CAcreateserial \
  -sha256 -days 825 \
  -extfile leaf_ext.cnf -extensions v3_req \
  -out leaf.crt
```

---

### 4. Verify Your Leaf’s SAN Entries

```bash
openssl x509 -in leaf.crt -noout -ext subjectAltName
```




#Certificates