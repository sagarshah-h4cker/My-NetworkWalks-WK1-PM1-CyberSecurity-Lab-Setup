# Project: Cyber Security Lab Environment Setup

**Building and setting up an isolated virtual lab environment for penetration testing and ethical hacking practices.**

---

## Project Overview

In this project, I set up a **virtual environment** that would be used as a **cybersecurity and penetration testing laboratory** using VirtualBox, Kali Linux, and Windows 10.

The main purpose of this lab was to create a controlled environment where I can test, use, and learn cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities.

This lab is configured on a private virtual network, so that additional machines can be added later and used as targets for authorized security testing.

---

## Objectives of this Project

1. Installation and configuration of VirtualBox.
2. Downloading and importing Kali Linux as a virtual machine in VirtualBox.
3. Setting up Windows 10 as a target machine in VirtualBox.
4. Creating a private NAT Network for the cybersecurity lab.
5. Configuring network connectivity for Kali Linux and Windows 10.
6. Assigning consistent IP addresses to both VMs.
7. Verify network connectivity between Kali Linux and Windows 10.
8. Take a clean VM snapshot for recovery.
9. Document the complete setup process.
10. Prepare the environment for future cybersecurity projects.

---

## Lab Configuration

| Components       | Configuration         |
| ---------------- | --------------------- |
| Host OS          | Windows 10            |
| Host RAM         | 16GB                  |
| Processor        | AMD Ryzen 7           |
| GPU              | RTX 4060              |
| Hypervisor       | VirtualBox            |
| Attacker OS      | Kali Linux            |
| Target OS        | Windows 10            |
| Kali RAM         | 4096MB                |
| Windows RAM      | 4096MB                |
| Virtual Network  | NAT Network           |
| Network Address  | 10.0.0.0/24           |
| Kali IP Address  | 10.0.0.2/24           |
| Windows IP       | 10.0.0.10/24          |
| Default Gateway  | 10.0.0.1              |
| DNS Server       | 8.8.8.8               |

---

## Network Architecture

```
VirtualBox NAT Network (10.0.0.0/24)
├── Kali Linux   → 10.0.0.2  (Attacker Machine)
└── Windows 10   → 10.0.0.10 (Target Machine)
```

---

## Lab Setup Procedure

### Step 1 → Install VirtualBox
- Downloaded and installed latest VirtualBox from official website.

### Step 2 → Create NAT Network
- Created NATNetwork in VirtualBox with subnet 10.0.0.0/24.
- Enabled DHCP.

### Step 3 → Setup Kali Linux VM
- Downloaded Kali Linux from official website.
- Imported into VirtualBox.
- Configured network adapter to NAT Network.
- Set static IP: 10.0.0.2/24

### Step 4 → Setup Windows 10 VM
- Downloaded Windows 10 ISO from Microsoft official website.
- Created new VM in VirtualBox.
- Installed Windows 10.
- Configured network adapter to NAT Network.
- Set static IP: 10.0.0.10/24

### Step 5 → Verify Network Connectivity
- Pinged Windows 10 from Kali Linux successfully.
- Pinged Kali Linux from Windows 10 successfully.
- Verified internet access on both VMs.

### Step 6 → Take VM Snapshot
- Took clean snapshot of both VMs for future recovery.

---

## Lab Verification

| Test | Command | Result |
| ---- | ------- | ------ |
| Check Kali IP | `ip a` | 10.0.0.2 ✅ |
| Kali → Gateway | `ping 10.0.0.1` | Success ✅ |
| Kali → Internet | `ping 8.8.8.8` | Success ✅ |
| Kali → Windows | `ping 10.0.0.10` | Success ✅ |
| Windows → Kali | `ping 10.0.0.2` | Success ✅ |

---

## Problems Encountered & Solutions

### Problem 1 — NATNetwork IP Wrong
- **Issue:** NATNetwork IPv4 was set to 10.0.2.0/24 instead of 10.0.0.0/24
- **Solution:** Fixed IPv4 prefix to 10.0.0.0/24 in VirtualBox Network settings

### Problem 2 — Kali Internet Not Working
- **Issue:** Kali Linux not getting IP address
- **Solution:** Used nmcli commands to fix connection:
```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

### Problem 3 — Windows 10 Freezing
- **Issue:** Windows 10 VM was freezing
- **Solution:** Increased RAM to 4GB and CPU cores to 4

---

## What I Learned

1. **NAT vs NAT Network** — NAT Network allows multiple VMs to communicate with each other.
2. **Static IP Configuration** — How to set manual IP in both Linux and Windows.
3. **VM Snapshots** — Importance of taking snapshots before risky activities.
4. **Network Troubleshooting** — How to diagnose and fix network issues in VMs.
5. **Linux Commands** — nmcli, ping, ip a commands for network management.
6. **Shared Folders** — How to share files between VM and host machine.

---

## Security & Ethical Use

This laboratory is intended strictly for **educational purposes only**.
All testing is performed in an isolated virtual environment.

---

## Tools & Resources

- **VirtualBox:** https://virtualbox.org/wiki/Downloads
- **Kali Linux:** https://kali.org/get-kali
- **Windows 10:** https://www.microsoft.com/software-download/windows10

---

## Author

**Sagar Shah**

**Program:** Cybersecurity at Networkwalks
**Week:** 01
**Project:** WK1-PM1 — Cybersecurity & Pentesting Lab Setup
