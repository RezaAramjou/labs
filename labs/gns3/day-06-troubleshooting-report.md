# Day 6 - GNS3 Lab: Troubleshooting and Resolution Report

## 1. Objective
The goal for Day 6 was to build, configure, and document a basic dual-router network topology in GNS3. The lab was designed to demonstrate dynamic routing using the **OSPF protocol** on a free, open-source router platform (**VyOS**).

## 2. Executive Summary
The initial *local server* integration approach, where GNS3 on the Ubuntu host directly manages a VirtualBox VM, failed due to a cascade of complex, deep-level system incompatibilities. After an exhaustive and methodical troubleshooting process that spanned software licensing, VM installation, host system package management (`dkms`), and multiple layers of GNS3 bugs (template misconfigurations, a broken setup wizard, and a non-functional web UI), it was determined that the local integration method on this specific host was fundamentally unstable.

The key takeaway is that while the lab was not completed, the diagnostic process itself became the deliverable, demonstrating a far more valuable set of professional skills: **persistence, methodical problem-solving, and the ability to diagnose and navigate undocumented system-level conflicts**. The final, correct architectural solution was identified as using the **official GNS3 VM**, which isolates the lab from the host and bypasses these integration issues.

## 3. Chronological Troubleshooting Log

### Problem 1: Host System Package Manager (apt) in a Broken State
- **Symptom:** Attempting to install the `openssh-server` on the Ubuntu host (to facilitate secure file transfers for Day 5) failed with a `dpkg` error code.

- **Diagnosis:** The `apt` package manager was in a broken state, blocked by a failure to configure the `linux-headers` package. The root cause was traced to several old, incompatible `dkms` modules for a Realtek Wi-Fi adapter (`8188eu` and `rtl8188eus`) that were failing to build against the new Linux kernel.

- **Resolution:**
  - Used `dkms status` to identify all faulty modules.
  - Manually removed all conflicting `dkms` modules one by one.
  - Ran:
    ```bash
    sudo apt --fix-broken install
    ```
    to repair the package manager state.

- **Success:** Successfully repaired the host OS package manager, a complex system administration task, which allowed `openssh-server` to be installed.

---

### Problem 2: GNS3 & VirtualBox Integration Failures (Local Server Method)
This was a series of nested configuration issues.

- **Initial Setup:** Successfully installed GNS3, VirtualBox, and the VyOS operating system from an `.iso` file, demonstrating fundamental virtualization skills.

- **Symptom 1: VM Template Issues:** The GNS3 template for the VyOS VM was not configured correctly out-of-the-box.
  - **Resolution:** Methodically debugged the template by enabling *Linked Clones*, allowing GNS3 to use any adapter, correcting the interface name format, and ensuring the master VM in VirtualBox had two network adapters enabled.

- **Symptom 2: PermissionError on Configuration Commit:** This was the critical failure. Committing a configuration to an interface (`set interfaces ethernet eth0...`) inside the VyOS VM would fail with a low-level `PermissionError`.
  - **Diagnosis:** A deep incompatibility between GNS3's management process, VirtualBox, and the VyOS guest.

- **Attempted Fixes (All Failed):**
  - Disabling GNS3's *headless* mode.
  - Loading a factory-default configuration to fix a boot error.
  - Changing the virtual network adapter type to `virtio-net`.

- **Conclusion:** The direct GNS3-to-VirtualBox control plane was fundamentally broken on this host.

---

### Problem 3: GNS3 GUI and Setup Wizard Bugs
- **Symptom:** Attempting to pivot to the recommended *GNS3 VM* method was blocked by bugs in the GNS3 GUI.

  - **The Broken Wizard:** The Setup Wizard would ignore the *Run appliances in a virtual machine* selection and force the user into the *Local server* configuration path.
  - **The Broken Web UI:** The GNS3 VM's web interface for uploading images was non-functional, with key links redirecting incorrectly.
  - **The Broken Marketplace:** All automated appliance download links in the GNS3 marketplace were found to be outdated, pointing to paid subscription portals instead of public download files.

- **Resolution:** Bypassed the GUIs entirely, using the command-line tool `scp` to securely transfer the VyOS `.iso` file directly into the GNS3 VM after creating the destination directory with `mkdir` via an SSH session. This demonstrated mastery of fundamental Linux command-line skills.

---

## 4. Final Analysis and Path Forward
The exhaustive process proved that the *local server* GNS3 architecture is fragile and prone to system-specific conflicts. The final attempt to use the GNS3 VM was the correct path, but was hampered by a series of unrelated GUI bugs and outdated templates.

The final, guaranteed solution (which we will proceed with on another day) is the manual GNS3 VM setup:

1. Manually configure GNS3 to disable the local server and enable the GNS3 VM.
2. Manually transfer appliance images (`.iso` files) into the GNS3 VM using `scp`.
3. Manually build a custom GNS3 appliance template from that `.iso` file.

---

This day was a testament to the importance of **resilience in a technical role**. While the initial objective was not met, the skills practiced and documented here are arguably more valuable.
