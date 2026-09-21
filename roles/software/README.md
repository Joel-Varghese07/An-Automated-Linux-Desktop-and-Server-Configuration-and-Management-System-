# Software role

## Purpose
Installs the project's configurable package list and optionally removes or upgrades packages.

## Variables
- `software_packages`: packages to install.
- `software_remove_packages`: packages to remove.
- `software_update_cache`: refresh APT metadata.
- `software_upgrade_packages`: upgrade installed packages.

## Run
```bash
ansible-playbook playbooks/site.yml --tags software
```

## Test
```bash
ansible-playbook playbooks/site.yml --tags software --check --diff
ansible-playbook playbooks/site.yml --tags software
ansible-playbook playbooks/site.yml --tags software
```

The second normal run should report `changed=0` when the system already matches the variables.
