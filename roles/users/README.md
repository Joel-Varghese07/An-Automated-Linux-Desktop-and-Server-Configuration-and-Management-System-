# Users role

## Purpose
Creates the project's admin, generic student, named class and staff accounts. All created accounts use Bash. Only the admin account is added to `sudo`.

## Password handling
Passwords must be supplied as pre-hashed values in Ansible variables. Do not put plaintext passwords in the repository.

The example variables intentionally contain empty hashes. Replace them with approved pre-hashed values outside this template before integration.

## Variables
- `users_admin`
- `users_student`
- `users_staff`
- `users_class_accounts`
- `users_remove_accounts`
- `users_shell`

## Run
```bash
ansible-playbook playbooks/site.yml --tags users
```

## Test
```bash
ansible-playbook playbooks/site.yml --tags users --check --diff
ansible-playbook playbooks/site.yml --tags users
ansible-playbook playbooks/site.yml --tags users
```
