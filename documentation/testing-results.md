# Security Testing and Verification Results

## Overview

This document records the security testing and configuration verification performed on the Ubuntu Jump Server and Internal Server.

The purpose of this testing was to verify SSH authentication, firewall configurations, Fail2ban protection, and secure network connectivity.

## 1. SSH Authentication Verification

**Result: Successful**

The following SSH connections were successfully verified:

- Connected from the MacBook Air administrator workstation to the Jump Server.
- Connected from the Jump Server to the Internal Server.
- Confirmed successful SSH public-key authentication on both connections.
- Confirmed the Internal Server received SSH connections from the Jump Server IP address `192.168.50.10`.

Both SSH private keys are protected with passphrases.

## 2. UFW Firewall Verification

**Result: Successful**

UFW was confirmed active on both Ubuntu servers.

### Jump Server

- Firewall status: Active.
- Default incoming policy: Deny.
- Default outgoing policy: Allow.
- SSH port 22: Allowed for IPv4 and IPv6.
- Firewall logging: Enabled.

### Internal Server

- Firewall status: Active.
- Default incoming policy: Deny.
- Default outgoing policy: Allow.
- SSH port 22: Allowed only from `xxx.xxx.xx.xx`.
- Firewall logging: Enabled.

The Internal Server firewall restricts SSH access to the Jump Server, helping enforce the intended network access architecture.

## 3. Fail2ban Verification

**Result: Configuration Verified**

Fail2ban was confirmed installed and running on both Ubuntu servers.

The SSHD jail was enabled on both systems.

| Configuration | Jump Server | Internal Server |
|---|---:|---:|
| SSHD jail | Enabled | Enabled |
| Maximum failed attempts | 5 | 5 |
| Detection window | 600 seconds (10 minutes) | 600 seconds (10 minutes) |
| Ban duration | 1800 seconds (30 minutes) | 1800 seconds (30 minutes) |

Fail2ban status checks showed zero failed attempts and zero banned IP addresses at the time of verification.

## 4. Network Connectivity Verification

**Result: Successful**

- Verified SSH connectivity from the MacBook Air to the Jump Server.
- Verified SSH connectivity from the Jump Server to the Internal Server.
- Confirmed the Internal Server was reachable through the Jump Server.
- Verified that the Internal Server SSH firewall rule permits connections from the Jump Server IP address.

This confirms the intended administrator access path:

**MacBook Air → Jump Server → Internal Server**

## 5. Verification Commands

The following commands were used to verify the security configurations.

### Fail2ban Verification

```bash
sudo systemctl status fail2ban
sudo fail2ban-client status
sudo fail2ban-client status sshd
```

### Fail2ban Configuration Checks

```bash
sudo fail2ban-client get sshd maxretry
sudo fail2ban-client get sshd findtime
sudo fail2ban-client get sshd bantime
```

### UFW Firewall Verification

```bash
sudo ufw status verbose
```

These commands were executed on the respective Ubuntu servers.

## 6. Testing Limitations

The following tests have not yet been performed:

- Deliberate failed-login testing.
- Verification of an actual Fail2ban IP ban.
- Formal penetration testing.

Fail2ban installation, service status, jail activation, and configuration values were verified. However, actual blocking behavior has not yet been tested through simulated failed login attempts.

## 7. Final Assessment

The security verification confirmed that both Ubuntu servers have active UFW firewalls and configured Fail2ban SSH protection.

The lab successfully demonstrates:

- Linux server administration.
- SSH public-key authentication.
- Secure remote administration.
- UFW firewall configuration.
- Network access restrictions.
- Fail2ban installation and configuration.
- Security configuration verification.

## Conclusion

This cybersecurity home lab demonstrates foundational Linux security and network administration practices through a two-server environment.

The Jump Server provides the administrative entry point to the Internal Server, while SSH authentication, firewall restrictions, and Fail2ban provide additional layers of security.
