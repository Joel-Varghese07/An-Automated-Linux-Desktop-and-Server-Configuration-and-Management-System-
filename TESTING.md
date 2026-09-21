# Testing checklist

## 1. Syntax
```bash
ansible-playbook playbooks/site.yml --syntax-check
```

## 2. Lint
```bash
ansible-lint
```

## 3. Connectivity
```bash
ansible all -m ping
ansible all -b -m command -a 'id'
```

## 4. Check mode
Run each role separately:
```bash
ansible-playbook playbooks/site.yml --tags software --check --diff
ansible-playbook playbooks/site.yml --tags users --check --diff
ansible-playbook playbooks/site.yml --tags network --check --diff
ansible-playbook playbooks/site.yml --tags hardening --check --diff
```

## 5. First real test
Use one VM only:
```bash
ansible-playbook playbooks/site.yml --limit desktop-1
```

For network/firewall/SSH changes, take or use a VM snapshot first.

## 6. Idempotency
Run the same command twice:
```bash
ansible-playbook playbooks/site.yml --limit desktop-1
ansible-playbook playbooks/site.yml --limit desktop-1
```

The second run should report `changed=0` for resources already in the desired state.

## 7. Hardening verification
```bash
sudo sshd -T | grep -E 'permitrootlogin|passwordauthentication'
sudo ufw status verbose
stat -c '%a %U %G' /etc/shadow
```

## 8. Network verification
Before enabling the network policy, confirm that the approved destination list exists. Do not substitute arbitrary real AI-service IP addresses.
