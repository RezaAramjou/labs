# Virtual Machine Snapshot Policy

This policy outlines the standardized procedure for creating, naming, and managing VirtualBox snapshots to ensure a consistent and recoverable lab environment.

## 1. Naming Convention

All snapshots MUST follow the `YYYYMMDD-VMNAME-STEP` format.

- **YYYYMMDD**: The date the snapshot was taken (e.g., `20250829`).
- **VMNAME**: The name of the virtual machine (e.g., `ubuntu-server`, `kali`).
- **STEP**: A short, descriptive name for the state of the VM.

**Examples:**
- `20250829-ubuntu-server-base-install` (A clean, post-installation snapshot)
- `20250830-kali-tools-updated` (After running system updates and installing tools)
- `20250905-ubuntu-server-before-hardening` (Before applying security changes)

## 2. Snapshot Frequency

Snapshots should be taken at critical points to allow for easy rollbacks:

- **Immediately** after a clean OS installation and initial updates ("base-install").
- **Before** making any major configuration changes (e.g., installing a web server, changing network settings, applying security hardening).
- **Before** running any potentially destructive tests or pentesting activities against the VM.
- **After** successfully configuring a complex lab setup that you may want to return to.

## 3. Retention and Management

To manage disk space, follow this retention policy:

- **Keep the last 5 snapshots** for each VM.
- **Delete older, redundant snapshots**. For example, once a "before-hardening" snapshot is no longer needed because the hardening was successful, it can be removed.
- **Export critical base snapshots** as an appliance (`.ova` file) for long-term backup.

Step 2: Create a README for the VirtualBox Directory
This file will give an overview of the VMs and useful commands.

Content for labs/virtualbox/README.md:

# VirtualBox Lab Environment

This directory contains setup notes and policies for the virtual machines used in these labs.

## Recommended VM Resources

- **Ubuntu Server**: 2GB RAM, 2 vCPUs, 25GB Dynamic Disk
- **Kali Linux**: 2-4GB RAM, 2 vCPUs, 30GB Dynamic Disk
- **Security Onion**: (Minimum) 12GB RAM, 4 vCPUs, 200GB Dynamic Disk

## Managing Snapshots

Refer to the [Snapshot Policy](./snapshots_policy.md) for detailed guidelines on naming and frequency.

### Key Commands (VBoxManage)

You can manage snapshots from the command line using `VBoxManage`.

**List Snapshots for a VM:**
`VBoxManage snapshot "Your-VM-Name" list`

**Take a Snapshot:**
`VBoxManage snapshot "Your-VM-Name" take "YYYYMMDD-VMNAME-STEP" --description "A brief description"`

**Restore a Snapshot:**
`VBoxManage snapshot "Your-VM-Name" restore "snapshot-name-or-uuid"`
