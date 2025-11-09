# Linux Server Provisioning & Hardening on GCP

This project demonstrates secure provisioning and configuration of a Linux Virtual Machine (VM) on Google Cloud Platform (GCP). It includes hardened SSH access, user security, firewall policies, automated updates, NGINX deployment, and scheduled system backups.

## Overview

This project implements practical Linux system administration and security controls aligned with RHCSA-level skills. It showcases the ability to deploy, configure, and secure a production-like Linux environment in the cloud.

## Project Goals

* Deploy a Linux virtual machine on GCP
* Enforce secure authentication and user management
* Configure SSH hardening and disabled root access
* Enable and validate firewall controls
* Install and manage NGINX web service
* Enable automatic security patches
* Configure automated home-directory backup
* Manage version-controlled documentation on GitHub

## Tech Stack

| Component | Technology |
|-----------|------------|
| Cloud Provider | Google Cloud Platform |
| OS | Ubuntu/Debian |
| Web Server | NGINX |
| Firewall | UFW |
| Backup Tool | cron + tar |
| Access | SSH |
| Version Control | Git + GitHub |

## Implementation Summary

### 1. VM Provisioning
* Created Linux VM using GCP Compute Engine
* Assigned external static IP
* Verified system connectivity over SSH

### 2. User & Access Control
* Created non-root user for administrative access
* Added user to sudoers group
* Disabled root login via SSH

### 3. SSH Hardening
* Updated `/etc/ssh/sshd_config`
  * `PermitRootLogin no`
* Restarted SSH daemon to apply changes

### 4. Firewall Configuration
* Enabled UFW
* Allowed SSH + HTTP traffic
* Denied all other ports

### 5. NGINX Deployment
* Installed and started NGINX
* Enabled service persistence on boot
* Verified successful page load via external IP

### 6. Automated Security Updates
* Installed unattended-upgrades
* Enabled auto-patching

### 7. Automated Backup
* Created shell script to compress `/home`
* Added cron job to run daily at 2 AM

## Directory Structure

```
linux-server-hardening-gcp/
│
├── README.md
├── scripts/
│   └── backup_home.sh
└── evidence/
    ├── vm-details.png
    ├── nginx-test.png
    └── firewall-rules.png
```

## Key Commands

### System Update
```bash
sudo apt update && sudo apt upgrade -y
```

### Create User
```bash
sudo adduser secureuser
sudo usermod -aG sudo secureuser
```

### SSH Hardening
Edit config:
```bash
sudo nano /etc/ssh/sshd_config
```

Restart SSH:
```bash
sudo systemctl restart ssh
```

### Firewall
```bash
sudo ufw enable
sudo ufw allow ssh
sudo ufw allow http
```

### NGINX
```bash
sudo apt install nginx -y
sudo systemctl enable nginx
```

### Auto Updates
```bash
sudo apt install unattended-upgrades -y
sudo dpkg-reconfigure --priority=low unattended-upgrades
```

### Scripted Backup
```bash
tar -czvf /tmp/home-backup.tar.gz /home
```

Cron entry:
```bash
0 2 * * * /home/secureuser/backups/backup_home.sh
```

## Evidence Collected

Stored in the `evidence/` directory. Includes:
* VM configuration
* Firewall rule snapshot
* NGINX access result

## Skills Demonstrated

* Linux system administration
* GCP compute provisioning
* User / privilege management
* SSH + firewall security
* Package & service management
* Shell scripting + cron automation
* Documentation & Git versioning

## Potential Enhancements

* Harden SSH further (key-based access only)
* Enable HTTPS via Let's Encrypt
* Add Fail2Ban
* Automated deployment via Ansible
* Log monitoring & alerting
* CI/CD integration for web content

## Conclusion

This project demonstrates the ability to provision, secure, and automate a Linux server in a cloud environment. It reflects real-world practices relevant to Cloud / DevOps / SysAdmin roles and validates hands-on capability with essential tools and services.

---

**Author:** Shabin Shareefa 
**License:** MIT  
**Repository:** https://github.com/shabinshareefa5018

