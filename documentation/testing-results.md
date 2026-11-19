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

## Security Testing Summary

The following security configurations were successfully verified during this lab:

### 1. SSH Authentication
- Successfully connected from the Mac administrator workstation to the Jump Server.
- Successfully connected from the Jump Server to the Internal Server.
- Verified SSH public-key authentication.

### 2. UFW Firewall
- Confirmed UFW is active on both Ubuntu servers.
- Verified incoming traffic is denied by default.
- Verified outgoing traffic is allowed by default.
- Confirmed SSH access is permitted.

### 3. Fail2ban Protection
- Confirmed the SSHD jail is enabled on both servers.
- Maximum failed attempts: 5.
- Find time: 600 seconds (10 minutes).
- Ban time: 1800 seconds (30 minutes).

### 4. Network Connectivity
- Verified SSH connectivity between the Mac and Jump Server.
- Verified SSH connectivity between the Jump Server and Internal Server.
- Confirmed the Internal Server is reachable through the Jump Server.

### Testing Limitations
- Deliberate failed-login and account-lockout testing has not been performed.
- No formal penetration test has been conducted.

## Conclusion

This lab demonstrates practical Linux server administration and foundational cybersecurity skills, including SSH hardening, firewall configuration, brute-force protection, and secure remote administration.

## Additional Security Verification — November 19, 2026

Additional testing was performed to verify SSH connectivity, firewall configurations, and Fail2ban protection on both Ubuntu servers.

### 1. SSH Connectivity Verification

**MacBook Air → Jump Server**
- Successfully connected using SSH public-key authentication.
- Verified access to the Jump Server.
- Private SSH key protected by a passphrase.

**Jump Server → Internal Server**
- Successfully connected using SSH public-key authentication.
- Verified access to the Internal Server.
- Confirmed the Internal Server received the connection from `192.168.50.10`.

### 2. Jump Server Firewall Verification

- UFW status: Active.
- Default incoming policy: Deny.
- Default outgoing policy: Allow.
- SSH port 22 permitted for IPv4 and IPv6.
- Firewall logging enabled.

### 3. Internal Server Firewall Verification

- UFW status: Active.
- Default incoming policy: Deny.
- Default outgoing policy: Allow.
- SSH port 22 permitted only from `192.168.50.10`.
- Firewall logging enabled.

### 4. Fail2ban Verification

Both servers successfully passed configuration checks.

| Configuration | Jump Server | Internal Server |
|---|---:|---:|
| SSH jail | Enabled | Enabled |
| Maximum retries | 5 | 5 |
| Find time | 600 seconds | 600 seconds |
| Ban time | 1800 seconds | 1800 seconds |

### 5. Testing Results

- SSH connectivity verified successfully.
- UFW firewall configurations verified.
- Fail2ban SSH protection verified.
- Internal Server SSH access restricted to the Jump Server.

### Testing Limitations

Deliberate failed-login testing and actual IP banning have not been performed. These results verify configuration and connectivity, not successful blocking of a simulated brute-force attack.

## Verification Conclusion

Both Ubuntu servers passed the additional security configuration checks. The lab demonstrates controlled SSH administration, firewall access restrictions, and Fail2ban-based SSH protection.
