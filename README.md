# Windows Server Home Lab

## Overview

I’m documenting my progress learning Windows Server administration, networking, and cybersecurity through a virtual home lab.

## Current Status

Windows Server 2025 Standard Evaluation (Desktop Experience) has been
installed successfully on the LAB-DC01 virtual machine in VirtualBox.

The VM has 4 GB of RAM, 2 virtual CPUs, an 80 GB virtual disk,
EFI enabled, and a network adapter configured for NAT.

Initial setup is complete. I signed in with the built-in Administrator
account and confirmed that the desktop and Server Manager opened.

The next milestone is to review and configure the Windows computer name,
time zone, and network settings. Active Directory has not been configured.

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


## Progress Log — October 3, 2026

### Milestone: Install Windows Server

#### Steps Completed

1. Started the LAB-DC01 virtual machine.
2. Opened UEFI Boot Manager and selected UEFI VBOX CD-ROM to start the installer.
3. Configured the installation language and keyboard settings.
4. Selected Windows Server 2025 Standard Evaluation (Desktop Experience).
5. Accepted the license terms.
6. Selected the 80 GB unallocated virtual disk.
7. Completed the Windows Server installation.
8. Created a password for the built-in Administrator account.
9. Signed in and confirmed that the desktop and Server Manager opened.

#### Result

Windows Server installed and booted successfully.
Administrator sign-in and access to the graphical desktop were verified.

Active Directory has not been configured.
LAB-DC01 is the VirtualBox VM name; the Windows computer name still
needs to be checked.

#### Troubleshooting Notes

The VM initially opened the UEFI firmware menu instead of Windows Setup.
Selecting UEFI VBOX CD-ROM in Boot Manager started the installer.

#### Next Milestone

Review and configure the Windows computer name, time zone, and network settings.
