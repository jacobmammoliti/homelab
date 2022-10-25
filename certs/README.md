# Certificates
This directory is only used to generate an internal Certificate Authority (CA) and a signed certificated for the HashiCorp Vault instance. All other application certificates are generated via cert-manager and Vault.

## CFSSL
[CFSSL](https://github.com/cloudflare/cfssl)  is CloudFlare's PKI/TLS tool for signing, verifying, and bundling TLS certificates. It can be installed on MacOS with [brew](https://brew.sh/):
```bash
brew install cfssl
```

## Generate the certificate authority
Generate a CA and private key:
```bash
cfssl gencert -initca ca.json | cfssljson -bare ca
```

Read the certificate to ensure correct attributes:
```bash
openssl x509 -in ca.pem -text -noout
```

## Generate a signed certificate for HashiCorp Vault
Generate the certificate and private key:
```bash
cfssl gencert -ca ../root/ca.pem -ca-key ../root/ca-key.pem client.json | cfssljson -bare server
```

Read the certificate to ensure correct attributes:
```bash
openssl x509 -in server.pem -text -noout
```