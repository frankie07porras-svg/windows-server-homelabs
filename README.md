# Windows Server Home Lab

## Overview

I’m documenting my progress learning Windows Server administration, networking, and cybersecurity through a virtual home lab.

## Current Status

The LAB-DC01 virtual machine has been created in VirtualBox.
It has 4 GB of RAM, 2 virtual CPUs, an 80 GB virtual disk,
and EFI enabled. The Windows Server 2025 evaluation ISO is
attached, and the network adapter is set to NAT.

The VM is currently powered off. Windows Server installation
is the next milestone.

## Planned Milestones

- Install VirtualBox and verify it opens.
- Create a Windows Server virtual machine.
- Configure basic server settings and networking.
- Practice file sharing and permissions.
- Add a Windows client virtual machine.
- Practice Active Directory, user and group management, and Group Policy.
- Document test results and troubleshooting as I go.

## Lab Environment

| Component | Configuration |
|---|---|
| Host operating system | Windows 11 Home, 64-bit |
| Host processor type | x64-based |
| Host memory | 16 GB |
| Hardware virtualization | Enabled, confirmed in Task Manager |
| Virtualization software | Oracle VirtualBox 7.2.20 |

## Documentation Approach


For each milestone, I’ll record the goal, steps taken, important settings, test results, and lessons learned. I’ll use sample data and won’t publish passwords or other sensitive information.
## Progress Log — October 3, 2026

### Milestone: Create the Server Virtual Machine

#### Steps Completed
1. Opened the New Virtual Machine wizard in VirtualBox.
2. Named the virtual machine LAB-DC01.
3. Selected the Windows Server 2025 evaluation ISO.
4. Selected Windows Server 2025 (64-bit) as the operating system type.
5. Disabled unattended installation to use manual Windows Setup.
6. Allocated 4096 MB of RAM and 2 virtual CPUs.
7. Configured an 80 GB virtual disk.
8. Enabled EFI.
9. Finished creating the VM.
10. Verified that LAB-DC01 appears in VirtualBox Manager.

#### Verified Configuration

| Component | Setting |
|---|---|
| VM name | LAB-DC01 |
| Installation media | Windows Server 2025 evaluation ISO |
| Memory | 4096 MB |
| Virtual CPUs | 2 |
| Virtual disk | 80 GB VDI |
| Firmware | EFI |
| Network adapter | NAT |
| Current state | Powered Off |

#### Result
The virtual machine has been created with the installation
ISO attached. Windows Server has not been installed.
Booting and operating system installation have not been tested yet.

#### Next Milestone
Install Windows Server and verify that it starts successfully.
