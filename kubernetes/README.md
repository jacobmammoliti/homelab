# Flux
[Flux](https://fluxcd.io/) is the core driver to deploying applications to the Kubernetes clusters. Once deployed, it constantly watches the appropriate directory for changes based on the YAML manifests.

## :open_file_folder: Directory structure
This directory contains the following directories under `flux` and are ordered below by how Flux will apply them.

```bash
./flux
├── ./clusters       # entrypoint to Flux
├── ./core           # core cluster configuration, loaded before `crds`
├── ./crds           # custom resource definitions (CRDs), loaded before `infrastructure`
├── ./infrastructure # key infrastructure applications, loaded before `apps`
└── ./apps           # common applications, loaded last
```

There are two types of configuration in the `clusters` directory, "home" and "development". The home configuration is applied to the Mac minis and is treated as the "production" environment. The development configuration is applied to a Kind cluster to test out configuration changes, updates, etc.

## :nut_and_bolt: Bootstrap Mac mini cluster
```bash
flux bootstrap github \
  --owner=jacobmammoliti \
  --repository=homelab \
  --branch=main \
  --path=./kubernetes/flux/clusters/home \
  --personal
```

## :nut_and_bolt: Bootstrap Development Cluster
```bash
flux bootstrap github \
  --owner=jacobmammoliti \
  --repository=homelab \
  --branch=main \
  --path=./kubernetes/flux/clusters/development \
  --personal
```