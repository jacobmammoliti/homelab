# Homelab
Repository containing all the orchestration code and configuration that I use to manage my homelab.

## Hardware
- 3 x Raspberry Pi 4 Model B
    - OS: Raspberry Pi OS (64-bit) (Debian 11 Buster)
    - RAM: 8GB
    - SD Card: 32GB
    - USB Drive: Kingston 32GB USB 3.0 DataTraveler
- 1 x Mac Mini (Late 2012)
    - OS: Ubuntu 20.04 LTS (64-bit)
    - RAM: 8GB
    - SSD: 250GB
    - USB Drive: Kingston 64GB USB 3.0 DataTraveler
- 1 x Synology 2 Bay NAS DS220j
    - HDD: 2 x Seagate Ironwolf 6TB

## Notable Tooling
### Ansible
[Ansible](https://www.ansible.com/) is a configuration management tool responsible for the automation of initializing each node and building Kubernetes clusters.

### Flux
[Flux](https://fluxcd.io) is a continuous delivery tool responsible for deploying all applications and resources to the Kubernetes cluster.

### Kuberetes
[K3s](https://k3s.io/) is a lightweight distribution of Kubernetes and is responsible for running the applications.

### Longhorn
[LongHorn](https://longhorn.io/) is storage solution responsible for providing persistant storage to the Kubernetes clusters.

### HashiCorp Vault
[HashiCorp Vault](https://www.vaultproject.io/) is a secrets management solution responsible for storing and encrypting secrets.

### HashiCorp Consul
[HashiCorp Consul](https://www.consul.io/) is a service networking solution responsible for providing service discovery in the environment.

### Plex
[Plex](https://www.plex.tv/) is a media service responsible for organizing and streaming content.

## Setup Environment
```bash
# Create a python virtual environment
python3 -m virtualenv venv

# Activate the environment
source venv/bin/activate

# Install all necessary modules
pip install requirements.txt

# Bootstrap all the nodes; Install K3s on MacMini
ansible-playbook -i inventory site.yml

# Bootstrap the Kubernetes cluster via Flux
flux bootstrap github \                                            
--owner=$GITHUB_USER \
--repository=homelab \
--branch=main \
--path=./kubernetes/clusters/macmini \
--personal
```