# Ubuntu Server Hardening Report & Procedures

This document outlines the steps taken to harden a base Ubuntu Server VM, explaining the rationale behind each security measure.

---

## 1. User Account Management

### Rationale
The Principle of Least Privilege dictates that users should only have the permissions necessary to perform their tasks. Operating directly as the `root` user or the default installer user is risky. A new, non-root administrative user was created to separate daily operations from the highest system privileges.

### Commands Executed
A new administrative user (`radmin`) was created and added to the `sudo` group to grant it the ability to perform administrative tasks when required.

```bash
sudo adduser radmin
sudo usermod -aG sudo radmin
```

---

## 2. Enforcing SSH Key-Only Authentication

### Rationale
Passwords can be weak, reused, or stolen. They are vulnerable to brute-force attacks, where an attacker tries thousands of passwords per second. Cryptographic keys (SSH keys) are vastly more secure. By disabling password authentication, we enforce a much stronger authentication method, significantly reducing the risk of unauthorized access.

### Commands Executed
An SSH public key was copied from the host machine to the new user's `authorized_keys` file on the VM.

```bash
# On the host machine, copy the public key to the VM
ssh-copy-id radmin@192.168.56.102
```

---

## 3. SSH Daemon Hardening (`/etc/ssh/sshd_config`)

### Rationale
The default SSH server configuration is often too permissive. Hardening it involves explicitly disabling high-risk features to shrink the attack surface.

- **Disabled Root Login** (`PermitRootLogin no`): The `root` user is the ultimate target for an attacker. Disabling direct SSH login for this user forces attackers to first compromise a less-privileged account and then attempt to escalate privileges, adding another layer of defense.  
- **Disabled Password Authentication** (`PasswordAuthentication no`): This setting tells the SSH server to reject any login attempt that tries to use a password, ensuring our key-only policy is effective.

### Commands Executed
The SSH server configuration file was edited, and the service was restarted to apply the changes.

```bash
# Edit the configuration file
sudo nano /etc/ssh/sshd_config

# Restart the service to apply changes
sudo systemctl restart sshd
```

---

## 4. Firewall Configuration (UFW)

### Rationale
A firewall operates on a "default deny" principle. By default, it should block all incoming traffic. We then explicitly open only the specific ports for services that we need. This prevents attackers from accessing other potentially vulnerable services running on the machine.

### Commands Executed
The Uncomplicated Firewall (UFW) was enabled and configured to only allow incoming traffic on the standard SSH port (22).

```bash
# Allow OpenSSH traffic (port 22)
sudo ufw allow OpenSSH

# Enable the firewall
sudo ufw enable
```

---

