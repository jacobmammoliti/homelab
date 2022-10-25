# Homelab
[![k3s](https://img.shields.io/badge/k3s-v1.24.4-brightgreen?style=for-the-badge&logo=kubernetes&logoColor=white)](https://k3s.io/)

## :book: Overview
This repository contains everything I use to run my lab at home. For more specific details, see the README in the following directories:

- [ansible](ansible/)
- [certs](certs/)
- [kubernetes](kubernetes/)

## :gear: Hardware
- 3 x Raspberry Pi 4 Model B
    - OS: Raspberry Pi OS (64-bit) (Debian 11 Buster)
    - RAM: 8GB
    - SD Card: 32GB
- 2 x Mac Mini (Late 2012)
    - OS: Ubuntu 22.04 LTS (64-bit)
    - RAM: 16GB
    - SSD: 250GB
- 1 x Synology 2 Bay NAS DS220j
    - HDD: 2 x Seagate Ironwolf 6TB

## :hammer_and_wrench: Notable Tooling
### Ansible
[Ansible](https://www.ansible.com/) is a configuration management tool responsible for the automation of initializing each node and building Kubernetes clusters.

### Flux
[Flux](https://fluxcd.io) is a continuous delivery tool responsible for deploying all applications and resources to the Kubernetes cluster.

### K3s
[K3s](https://k3s.io/) is a lightweight distribution of Kubernetes and is responsible for running the applications.

### Longhorn
[Longhorn](https://longhorn.io/) is storage solution responsible for providing persistent storage to the Kubernetes clusters.

### HashiCorp Vault
[HashiCorp Vault](https://www.vaultproject.io/) is a secrets management solution responsible for storing and encrypting secrets.

### Traefik
[Traefik](https://doc.traefik.io/traefik/) is an ingress gateway responsible for exposing services outside of the Kubernetes cluster.

### Plex
[Plex](https://www.plex.tv/) is a media service responsible for organizing and streaming content.