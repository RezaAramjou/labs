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
