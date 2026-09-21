# Network role

## Purpose
This role enforces the agreed network-policy scope: restrict outbound access to configured AI-model IP destinations for student accounts while leaving staff accounts unrestricted.

It deliberately does **not** configure `ens33` or `ens34`, their addresses, or their routes.

## Important limitation
IP-based filtering requires an approved, maintained list of AI-model destination IP addresses/CIDRs. The project brief does not provide that list. Therefore `network_ai_block_ipv4` is empty and blocking is disabled by default until the group supplies and approves the destination list.

This avoids silently inventing endpoint addresses or breaking unrelated traffic.

## Variables
- `network_student_usernames`: accounts subject to the restriction.
- `network_ai_block_ipv4`: approved IPv4 destinations/CIDRs.
- `network_ai_block_ipv6`: optional IPv6 destinations/CIDRs.
- `network_ai_block_enabled`: enables the policy.

## Example group_vars
```yaml
network_ai_block_enabled: true
network_student_usernames:
  - student
  - student01
  - student02

network_ai_block_ipv4:
  - 203.0.113.10
```

The address above is documentation-only TEST-NET space and must not be treated as a real AI endpoint. Replace it only with the group's approved test destinations.

## Run
```bash
ansible-playbook playbooks/site.yml --tags network
```

## Safety
The role never changes the management interface. Test on one VM/snapshot first.
