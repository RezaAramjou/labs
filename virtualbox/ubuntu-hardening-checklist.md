# Ubuntu Hardening Checklist

| Task                                   | Status       | Notes                                             |
| -------------------------------------- | ------------ | ------------------------------------------------- |
| Create new non-root administrative user | ✅ Completed | User `radmin` created and added to `sudo` group.  |
| Set up SSH key-based authentication     | ✅ Completed | Public key added to `~/.ssh/authorized_keys`.     |
| Disable SSH root login                  | ✅ Completed | Set `PermitRootLogin no` in `sshd_config`.        |
| Disable SSH password authentication     | ✅ Completed | Set `PasswordAuthentication no` in `sshd_config`. |
| Configure UFW firewall                  | ✅ Completed | Enabled firewall and allowed OpenSSH.             |
| Verify SSH access after changes         | ✅ Completed | Successful login without a password.              |
