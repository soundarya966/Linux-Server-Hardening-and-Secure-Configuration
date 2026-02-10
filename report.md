# Linux Server Hardening & Secure Configuration

## Objective
The objective of this task was to perform Linux server hardening by securing system configurations, restricting access, enabling firewall protection, and monitoring system activity to reduce vulnerabilities and improve overall security.

Server hardening helps minimize the attack surface and protects the system from unauthorized access and exploitation.

---

## Environment
Operating System: Kali Linux / Ubuntu Linux
Tools Used:
- SSH
- UFW Firewall
- systemctl
- unattended-upgrades
- Lynis (optional security auditing tool)

---

## Implementation Steps

### 1. System Review
First, the system environment was reviewed to identify users, services, and open ports.

Commands used:
- whoami
- uname -a
- cat /etc/passwd
- ss -tuln
- systemctl list-units --type=service

This helped understand the current system configuration before applying security controls.

---

### 2. User Account Management
Unused user accounts were identified and removed to reduce unauthorized access risk.

Example command:
- sudo deluser testuser

Sudo privileges were reviewed using:
- getent group sudo

This ensures the principle of least privilege.

---

### 3. SSH Hardening
SSH configuration was secured by disabling root login and password authentication.

File modified:
- /etc/ssh/sshd_config

Changes made:
- PermitRootLogin no
- PasswordAuthentication no

SSH service restarted:
- sudo systemctl restart ssh

SSH key authentication was configured using:
- ssh-keygen
- ssh-copy-id user@localhost

---

### 4. System Updates
System packages were updated to ensure the latest security patches were installed.

Commands:
- sudo apt update
- sudo apt upgrade -y

Automatic updates were enabled:
- sudo apt install unattended-upgrades
- sudo dpkg-reconfigure unattended-upgrades

---

### 5. Firewall Configuration
UFW firewall was enabled to allow only required traffic.

Commands:
- sudo ufw enable
- sudo ufw allow OpenSSH
- sudo ufw status

This protects the server from unauthorized network connections.

---

### 6. Service Management
Unnecessary services increase the attack surface. These services were stopped and disabled.

Example:
- sudo systemctl stop apache2
- sudo systemctl disable apache2

---

### 7. File Permission Hardening
Sensitive system files were secured with appropriate permissions.

Commands:
- sudo chmod 600 /etc/shadow
- sudo chmod 644 /etc/passwd

This prevents unauthorized modification of critical files.

---

### 8. Log Monitoring
System logs were reviewed to monitor authentication attempts and system events.

Commands:
- sudo journalctl -p 3 -xb
- sudo tail -f /var/log/auth.log

Log monitoring helps detect suspicious activity.

---

### 9. Security Audit (Optional)
The Lynis tool was used to perform a security audit.

Commands:
- sudo apt install lynis
- sudo lynis audit system

This provided recommendations for additional hardening.

---

## Results
The Linux system was successfully hardened by:
- Restricting root access
- Enabling firewall protection
- Updating system packages
- Disabling unnecessary services
- Securing file permissions
- Monitoring system logs

These measures significantly reduce the risk of unauthorized access and system compromise.

---

## Conclusion
Linux server hardening is an essential security practice that protects systems against common cyber threats. By applying least privilege, securing SSH, enabling firewall protection, and maintaining updates, the system becomes more resilient to attacks.

This task provided practical experience in securing Linux environments using industry-recommended techniques.
