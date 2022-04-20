
## Deploy Prometheus Stack
```bash
helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack \
--create-namespace \
--namespace monitoring \
--values kube-prometheus-stack/values.yaml
```

## Deploy Loki
```bash
helm install loki grafana/loki \
--create-namespace \
--namespace logging \
--values loki/values.yaml 
```

## Deploy Promtail
```bash
helm install promtail grafana/promtail \
--create-namespace \
--namespace logging \
--values promtail/values.yaml
```

## Deploy Longhorn
```bash
helm install longhorn longhorn/longhorn \
--create-namespace \
--namespace longhorn-system \
--values longhorn/values.yaml
```

## Deploy HashiCorp Vault
```bash
kubectl create ns vault

kubectl create secret tls tls --cert=cert.pem --key=cert-key.pem --namespace vault

kubectl create secret generic tls-ca --from-file=ca.crt=ca.crt --namespace vault

helm install vault hashicorp/vault \
--namespace vault \
--values vault/values.yaml
```