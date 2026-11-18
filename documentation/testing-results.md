# Security Testing and Verification Results

## Overview

This document records the verification performed on the Ubuntu Jump Server and Internal Server.

## 1. SSH Authentication

**Result: Successful**

- Verified SSH connectivity from macOS to the Jump Server.
- Verified SSH connectivity from the Jump Server to the Internal Server.
- Confirmed successful public-key authentication.

## 2. UFW Firewall

**Result: Successful**

Both servers reported that UFW was active.

Verified firewall policies:

- Incoming connections: Denied by default.
- Outgoing connections: Allowed by default.
- SSH port 22: Allowed.
- Logging: Enabled.

## 3. Fail2ban

**Result: Successful**

Fail2ban was installed and running on both servers.

Verified SSH jail settings:

| Configuration | Jump Server | Internal Server |
|---|---:|---:|
| Maximum attempts | 5 | 5 |
| Detection window | 600 seconds | 600 seconds |
| Ban duration | 1800 seconds | 1800 seconds |
| SSH jail | Enabled | Enabled |

## 4. Verification Commands

```bash
sudo systemctl status fail2ban
sudo fail2ban-client status
sudo fail2ban-client status sshd
sudo ufw status verbose
```

## 5. Final Assessment

The lab successfully demonstrates:

- SSH key-based authentication.
- Firewall protection using UFW.
- SSH intrusion monitoring using Fail2ban.
- Secure administration across two Ubuntu servers.

**Note:** Active configuration checks were performed. Deliberate failed-login testing and penetration testing have not yet been performed.

## Conclusion

The two-server environment provides a practical demonstration of foundational Linux security and network administration skills.
