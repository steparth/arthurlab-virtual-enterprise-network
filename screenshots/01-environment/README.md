Installation Steps

# Installation Steps

This document describes the deployment and initial configuration of the **ArthurLab Virtual Enterprise Network**, a Windows Server 2022 lab environment built using Oracle VirtualBox. The lab simulates a small enterprise network providing Active Directory Domain Services (AD DS), DNS, DHCP, Group Policy, SMB file services, and cross-platform validation using Windows and Ubuntu clients.

---

# 1. Lab Environment

## Hardware

| Component        | Specification            |
| ---------------- | ------------------------ |
| Host Computer    | Intel Core Ultra 7 275HX |
| Memory           | 32 GB RAM / 1TB SSD               |
| Operating System | Windows 11 Pro           |
| Virtualization   | Oracle VirtualBox        |

---

## Virtual Machines

| Virtual Machine | Operating System    | Purpose                               |
| --------------- | ------------------- | ------------------------------------- |
| SERVER01        | Windows Server 2022 | Active Directory, DNS, DHCP, SMB      |
| WIN11-PC1       | Windows 11          | Domain-joined workstation             |
| WIN10-PC2       | Windows 10          | Domain-joined workstation             |
| UBUNTU-01       | Ubuntu 22.04 LTS    | Linux validation and SMB/CIFS testing |


---

# 2. Create the Virtual Machines

Create four virtual machines in Oracle VirtualBox.

### SERVER01

| Setting          | Value                        |
| ---------------- | ---------------------------- |
| Name             | SERVER01                     |
| Operating System | Windows Server 2022          |
| Memory           | 8– GB                      |
| CPU              | 4 vCPUs                      |
| Disk             | 70 GB                        |
| Network          | Internal Network (ArthurLab) |

### WIN11-PC1

| Setting          | Value      |
| ---------------- | ---------- |
| Operating System | Windows 11 |
| Memory           | 4 GB     |
| CPU              | 2 vCPUs    |
| Disk             | 60 GB      |

### WIN10-PC2

| Setting          | Value      |
| ---------------- | ---------- |
| Operating System | Windows 10 |
| Memory           | 4 GB       |
| CPU              | 2 vCPUs    |
| Disk             | 50 GB      |

### UBUNTU-01

| Setting          | Value            |
| ---------------- | ---------------- |
| Operating System | Ubuntu 25.04 LTS |
| Memory           | 4 GB             |
| CPU              | 2 vCPUs          |
| Disk             | 30 GB            |


---

# 3. Configure Virtual Networking

Create an **Internal Network** named:

```text

ArthurLab

```

Connect all virtual machines to this internal network.

Network configuration:

| Item         | Value           |
| ------------ | --------------- |
| Network Name | ArthurLab       |
| Subnet       | 192.168.10.0/24 |


---

# 4. Install Windows Server 2022

Install Windows Server 2022 on SERVER01.

During installation:

* Select Windows Server 2022 Standard (Desktop Experience)
* Create the local Administrator password


After installation:

* Rename the server to **SERVER01**
* Restart the server


---

# 5. Configure Static IP Address

Configure the server with a static IPv4 address.

| Setting         | Value           |
| --------------- | --------------- |
| IP Address      | 192.168.10.10   |
| Subnet Mask     | 255.255.255.0   |
| Default Gateway | (if applicable) |
| Preferred DNS   | 192.168.10.10   |

Verify using:

```powershell

ipconfig /all

```


# 6. Verify Network Connectivity

Before installing server roles, verify that the server is functioning correctly.

Run:

```powershell

hostname



ipconfig /all



ping 127.0.0.1

```

Expected result:

* SERVER01 displays the correct hostname.
* Static IP configuration is correct.
* Local network stack responds successfully.


---

# 7. Prepare for Server Role Installation

Open **Server Manager** and verify that the server is ready for role installation.

The following roles will be installed in the subsequent documentation:

* Active Directory Domain Services
* DNS Server
* DHCP Server
* File and Storage Services (SMB)



