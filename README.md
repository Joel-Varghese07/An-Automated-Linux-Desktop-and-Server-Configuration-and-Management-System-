# CNLA Ansible Playbooks and Roles

Project: An Automated Linux Desktop and Server Configuration and Management System for College Labs and Offices



## Roles
- `software`: package installation, removal and optional upgrades.
- `users`: admin, student, class and staff account provisioning/removal.
- `network`: per-user outbound AI-destination filtering; does not touch `ens33` or `ens34`.
- `hardening`: SSH, UFW and `/etc/shadow` baseline checks.

## Layout
```text
playbooks/site.yml
roles/
  software/
  users/
  network/
  hardening/
group_vars/
requirements.yml
.gitignore
```

## Prerequisites
The control node already has Ansible and the inventory configured according to the project documentation. The UFW role additionally requires the `community.general` collection.

Install the collection:
```bash
ansible-galaxy collection install -r requirements.yml
```

## Validation
From `~/cnla`:

```bash
ansible-playbook playbooks/site.yml --syntax-check
ansible-lint
ansible-playbook playbooks/site.yml --check --diff
```

Then test on one VM first:

```bash
ansible-playbook playbooks/site.yml --limit desktop-1
ansible-playbook playbooks/site.yml --limit desktop-1
```

The second normal run should show `changed=0` for already-correct resources.

## Tags
```text
software
users
network
hardening
HARD-SSH-01
HARD-SSH-02
HARD-FW-01
HARD-FW-02
HARD-FW-03
HARD-FW-04
HARD-PERM-01
```

## Important project decisions
- Never modify the `ens34` management interface in shared runs.
- SSH access must be allowed before UFW is enabled.
- Never weaken the `ansible` account.
- Passwords are stored only as pre-hashed Ansible variables; plaintext stays outside the repository.
- The final software package list and final hardening-check list still require group approval.
- The network role's approved AI destination list still needs to be supplied by the group.
