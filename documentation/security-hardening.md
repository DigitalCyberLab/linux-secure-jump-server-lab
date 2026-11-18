# Security Hardening

## Overview

This document describes the security controls implemented on the Ubuntu Jump Server and Internal Server.

## 1. SSH Security

- Configured SSH key-based authentication.
- Established secure administrative access from macOS to the Jump Server.
- Configured key-based SSH authentication from the Jump Server to the Internal Server.
- Verified successful public-key authentication.

## 2. UFW Firewall

Both Ubuntu servers have UFW enabled.

Firewall configuration:

- Default incoming traffic: Deny
- Default outgoing traffic: Allow
- SSH port: TCP 22
- SSH access: Allowed
- Firewall logging: Enabled

## 3. Fail2ban Intrusion Prevention

Fail2ban is installed and running on both servers.

SSH jail configuration:

| Setting | Value |
|---|---|
| Jail | sshd |
| Maximum failed attempts | 5 |
| Detection window | 10 minutes |
| Ban duration | 30 minutes |
| Backend | systemd |

## 4. Verification

The following commands were used to verify the configuration:

```bash
sudo systemctl status fail2ban
sudo fail2ban-client status sshd
sudo fail2ban-client get sshd maxretry
sudo fail2ban-client get sshd findtime
sudo fail2ban-client get sshd bantime
sudo ufw status verbose
```

## Security Outcome

Both servers have SSH key-based access, active firewall protection, and Fail2ban monitoring configured.

These controls provide multiple layers of protection for the lab environment.
