# Hardening role

## Proposed named checks
These are the initial checks for group approval. The project brief states that the final list is still open.

| ID | Check | Module | Verification |
|---|---|---|---|
| HARD-SSH-01 | SSH root login disabled | `lineinfile` | `sshd -T \| grep permitrootlogin` |
| HARD-SSH-02 | SSH password authentication disabled | `lineinfile` | `sshd -T \| grep passwordauthentication` |
| HARD-FW-01 | SSH allowed before firewall activation | `community.general.ufw` | `ufw status verbose` |
| HARD-FW-02 | Default incoming policy is deny | `community.general.ufw` | `ufw status verbose` |
| HARD-FW-03 | Default outgoing policy is allow | `community.general.ufw` | `ufw status verbose` |
| HARD-FW-04 | Firewall enabled | `community.general.ufw` | `ufw status verbose` |
| HARD-PERM-01 | `/etc/shadow` mode is 0640 | `file` | `stat -c %a /etc/shadow` |

## Run
```bash
ansible-playbook playbooks/site.yml --tags hardening
```

## Safety
The SSH rule is applied before UFW is enabled. Test SSH configuration on one VM or a snapshot first. Do not remove or weaken the `ansible` account.

## Dependencies
The role uses `community.general.ufw`.
