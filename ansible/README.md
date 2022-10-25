# Configuring the homelab Instances
All instances in the homelab are configured with Ansible roles to ensure consistency and repeatability. The following sections show the steps used to configure the instances depending on their use case.

## Activate Virtual Environment
A python virtual environment is used to prevent interference with system packages.

```bash
# Create a python virtual environment
python3 -m virtualenv venv

# Activate the environment
source venv/bin/activate

# Install all necessary modules
pip install -r requirements.txt
```

## :hammer: Initialization
The initialize role is run against all instances, regardless of their purpose. It is responsible for installing required packages, updating existing packages, creating initial users, mounting NFS storage, etc.

This role is also used throughout the lifecycle of the instance to keep their packages up-to-date.

> **Note:** On first run, you need to pass in `--ask-become-pass` since passwordless sudo is not yet enabled. On future runs, this does not need to be passed again.

### Initialize the Mac minis
Ensure all instances reachable:
```bash
ansible macminis \
--inventory inventory \
--module-name ping \
--user ubuntu
```

> output
```bash
macmini01.blizzard.internal | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
macmini02.blizzard.internal | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

Run the playbook:
```bash
ansible-playbook initialize.yml \
--inventory inventory \
--limit macminis \
--ask-become-pass
```

### Initialize the Rapsberry Pis
Ensure all instances are reachable:
```bash
ansible raspberrypis \
--inventory inventory \
--module-name ping \
--user pi
```

> output
```bash
raspberrypi01.blizzard.internal | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
raspberrypi02.blizzard.internal | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
raspberrypi03.blizzard.internal | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

Run the playbook:
```bash
ansible-playbook initialize.yml \
--inventory inventory \
--limit raspberrypis \
--ask-become-pass
```

## :ferris_wheel: K3s
This role is used to deploy a K3s on the Mac minis. It configures one Mac mini to act as the Controller and configures the other to act as the Worker.

Run the playbook:
```bash
ansible-playbook -i inventory k3s.yml
```

## :key: HashiCorp Vault
This role is used to deploy HashiCorp Vault on the Mac minis. It configures the Mac minis in HA mode and to use a [GCS bucket](https://cloud.google.com/storage/docs/introduction) for storage and [GCP KMS](https://cloud.google.com/kms/docs) as the seal mechanism.

> **Note:** The HashiCorp Vault role is maintained externally [here](https://github.com/jacobmammoliti/ansible-role-vault).

Install the role locally:
```
ansible-galaxy install -r requirements.yml
```

Run the playbook:
```bash
ansible-playbook -i inventory vault.yml
```

## :repeat: Keepalived
This role is used to deploy Keepalived on the Mac minis. Its used to provide a single virtual IP address for HashiCorp Vault.

Run the playbook:
```bash
ansible-playbook -i inventory keepalived.yml
```