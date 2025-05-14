# 🖥️ Born2beroot Project

## 📋 Project Overview

The Born2beroot project focused on creating a secure virtual machine configuration using Debian. The project introduced several fundamental system administration concepts:

- 🔹 **Virtual Machine Basics**: Creating and managing a virtualized computing environment that shares physical resources
- 🔹 **Linux Distributions**: Understanding Debian's features and package management systems
- 🔹 **Security Fundamentals**: Implementing multiple layers of system protection

I selected Debian for this project due to its stability, robust package support, and suitability for personal use compared to enterprise-focused alternatives like Rocky/RHEL.

## ⚙️ System Setup

The system configuration included:

- 🔸 **Base OS**: Debian (confirmed via `cat /etc/os-release`)
- 🔸 **CLI-only Environment**: No graphical interface
- 🔸 **Security Components**:
  - AppArmor: A Mandatory Access Control system that restricts program capabilities
  - UFW (Uncomplicated Firewall): Configured and enabled
  - SSH: Configured for secure remote access
  
Verification commands:
```bash
uname -a                   # OS and kernel version
sudo systemctl status ufw  # Firewall status
sudo systemctl status ssh  # SSH service status
```

## 👤 User Management

I implemented strict password policies and user management:

- 🔒 **Password Requirements**:
  - Minimum 10 characters
  - Must include uppercase, lowercase, and numbers
  - No more than 3 consecutive identical characters
  - Cannot contain username
  - Must differ from previous password by at least 7 characters
  - Root user subject to same policy

- ⏱️ **Password Expiration**:
  - 30 days maximum validity
  - 2 days minimum between password changes
  - Warning 7 days before expiration

Configured through:
```bash
sudo vim /etc/pam.d/common-password  # Password complexity rules
sudo vim /etc/login.defs             # Password expiration settings
sudo chage -l [username]             # Verify password aging information
```

## 💾 Hostname & Partitioning

- 🏷️ **Hostname Configuration**: Set to `ryabuki42`, manageable via `hostnamectl`
- 📊 **Logical Volume Management (LVM)**: Implemented disk partitioning using LVM, which provides:
  - Flexible storage management
  - Ability to resize volumes without system downtime
  - Simplified disk administration

Verification command:
```bash
lsblk  # Shows partitioning scheme with LVM implementation
```

## 🛡️ SUDO Configuration

Enhanced security through custom sudo configurations:

- 🔑 **Limited Authentication Attempts**: Maximum 3 password attempts
- ⚠️ **Custom Error Message**: Configured for failed authentication
- 🖥️ **TTY Requirement**: Prevents non-terminal access
- 🛣️ **Path Restrictions**: Limits command execution paths
- 📝 **Logging**: All sudo commands are logged to `/var/log/sudo/sudo.log`

Implemented through:
```bash
sudo visudo  # Sudo configuration editor
```

## 🔥 UFW Configuration

Implemented network security through UFW:

- 🚫 **Default Policy**: Deny incoming, allow outgoing connections
- ✅ **Specific Permissions**: Only port 4242 opened for SSH access
- 🔄 **Easy Management**: Simple rule addition/removal demonstrated

Management commands:
```bash
sudo ufw status                # View current rules
sudo ufw allow [port]          # Open specific port
sudo ufw delete allow [port]   # Remove rule
```

## 🔐 SSH Configuration

Implemented secure remote access:

- 🔢 **Port Configuration**: Changed from default 22 to 4242
- 👑 **Root Access**: Disabled direct root SSH login
- 🔏 **Authentication**: Password-based authentication configured

Benefits learned:
- Encrypted communications preventing data interception
- Strong authentication mechanisms
- Secure remote server management

Configuration location:
```bash
sudo nano /etc/ssh/sshd_config  # SSH server configuration file
```

## 📊 Monitoring Script

Created a Bash script that displays system information every 10 minutes:

- 💻 **System Details**: OS, kernel version, CPU usage, memory usage
- 📈 **Resource Utilization**: Processor count, memory/disk usage percentages  
- 🌐 **Network Information**: IP address, MAC address, active connections
- 👥 **User Activity**: Connected user count, sudo command usage

The script is scheduled using cron:
```bash
sudo crontab -l  # View current cron jobs
```

