# Ubuntu Server Hardening Steps

This document logs the exact steps and commands used to harden the base Ubuntu Server VM.

## 1. User Creation

A new administrative user was created to avoid using the default user for operations.

```bash
sudo adduser radmin
sudo usermod -aG sudo radmin
