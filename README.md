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

## Progress Log – October 3, 2026

### Milestone: Verify Server Identity and Configure Networking

#### Steps Completed

1. Verified that the Windows computer name is LAB-DC01.
2. Checked the time zone and confirmed it is correct.
3. Reviewed the VirtualBox NAT Network DHCP configuration.
4. Changed the NatNetwork DHCP range to 10.0.2.100–10.0.2.254,
   leaving addresses outside that range available for static configuration.
5. Applied the following static IPv4 settings:
   - IP address: 10.0.2.10
   - Subnet mask: 255.255.255.0
   - Default gateway: 10.0.2.1
   - Temporary preferred DNS server: 192.168.1.254
   - Alternate DNS server: None
6. Ran ipconfig /all and verified the computer name, static address,
   subnet mask, gateway, and DNS server.
7. Confirmed DHCP is disabled on the server's Ethernet adapter.
8. Verified browser access and Google search after applying the static IP.

#### Result

LAB-DC01 has a verified static IPv4 configuration outside the
configured DHCP pool.

The computer name and time zone were checked, and browser access
worked after the network changes.

Active Directory has not yet been installed or configured.
The DNS client setting is temporary and will be updated when
the server's Active Directory and DNS roles are configured.

#### Troubleshooting Notes

Before applying the static IP, DNS resolution and ping succeeded,
but TCP port 443 tests to Microsoft and Google failed inside the VM.

A TCP port 443 test to Google also failed on the host computer.
Browser access worked on both the host and VM despite these failures.

The cause of the TCP test failures remains unresolved.
No firewall settings were changed.
#### Troubleshooting Notes

**Issue: TCP connection tests failed despite working browser access**

1. Checked DNS resolution inside LAB-DC01.
   A lookup for www.microsoft.com returned IP addresses.
2. Tested connectivity using PowerShell.
   Ping succeeded, but TCP port 443 tests returned
   TcpTestSucceeded: False.
3. Repeated a TCP port 443 test on the host computer.
   It also failed, showing that the test failure was not
   limited to the VM.
4. Opened Google and performed a search on the host computer.
   Search results loaded successfully.
5. Repeated the browser test inside LAB-DC01.
   Search results also loaded successfully.

**Outcome:** Browser access worked on both computers despite the
failed TCP tests. The cause of the TCP test failures was not
determined. No firewall settings were changed.

**Issue: Planned static IP overlapped the DHCP allocation range**

1. Reviewed VirtualBox DHCP settings from PowerShell on the host:

   & "C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" list dhcpservers

2. Found that NatNetwork assigned addresses from
   10.0.2.3 through 10.0.2.254.
   The planned server address, 10.0.2.10, was within this range.
3. Changed the DHCP allocation range:

   & "C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" dhcpserver modify --network=NatNetwork --lower-ip=10.0.2.100 --upper-ip=10.0.2.254

4. Ran list dhcpservers again and confirmed that NatNetwork
   now used 10.0.2.100–10.0.2.254.
5. Left the separate host-only network's DHCP settings unchanged.

**Outcome:** The planned server address was outside the updated
DHCP pool. This addressed a potential allocation conflict;
an actual duplicate-IP conflict was not observed.

**Verification after applying the static IP**

1. Configured LAB-DC01 with:
   - IP address: 10.0.2.10
   - Subnet mask: 255.255.255.0
   - Default gateway: 10.0.2.1
   - Temporary DNS server: 192.168.1.254
2. Ran ipconfig /all inside the VM.
3. Confirmed the computer name was LAB-DC01, DHCP was disabled,
   and the configured IPv4 settings matched the intended values.
4. Opened Google inside the VM and successfully performed a search.

**Outcome:** The static configuration was applied, and browser
access continued to work after the change. This did not establish
that the earlier TCP test failures were resolved.

#### Next Milestone

Install Active Directory Domain Services and configure the first
domain controller for the lab.
