Ubuntu SMB/CIFS Validation

Overview

This document validates cross-platform interoperability between Ubuntu 24.04 LTS and the Windows Server 2022 file server in the ArthurLab Virtual Enterprise Network.

Ubuntu was configured to access SMB file shares hosted on SERVER01, demonstrating successful communication between Linux and Windows systems.

Lab Environment
Component	Value
Ubuntu Hostname	UBUNTU-01
Operating System	Ubuntu 24.04 LTS
Domain	int.arthurlab.com
Windows Server	SERVER01
Server FQDN	server01.int.arthurlab.com
Step 1 – Verify Ubuntu Network Configuration

First, verify that Ubuntu obtained an IP address from the Windows DHCP server.

Run:

ip addr

Expected result:

Ubuntu receives an IP address in the 192.168.10.0/24 subnet.
The client can communicate with SERVER01.


Step 2 – Install SMB Client

Initially, the smbclient utility was not installed.

Attempting to list Windows shares returned:

smbclient -L //server01.int.arthurlab.com -U ARTHURLAB/Administrator

Ubuntu suggested installing the required package.

Install it using:

sudo apt install smbclient



Step 3 – Install CIFS Utilities

To support mounting Windows SMB shares as local directories, install the CIFS utilities package.

Run:

sudo apt install cifs-utils

Accept the installation when prompted.


Step 4 – Verify CIFS Installation

Confirm that the CIFS utilities were installed successfully.

Run:

mount.cifs --version

Expected output:

mount.cifs version: 7.0

Step 5 – Install Samba

Install Samba to enable additional SMB tools and services.

Run:

sudo apt install samba

Wait for the installation to complete.


Step 6 – Discover Windows Shares

List the SMB shares available on the Windows Server.

Run:

smbclient -L //server01.int.arthurlab.com -U ARTHURLAB/Administrator

After entering the administrator password, Ubuntu successfully discovered the following shares:

ADMIN$
C$
HR Share
IT Share
NETLOGON
Public Shares
SYSVOL

This confirms successful SMB communication between Ubuntu and Windows Server.



Step 7 – Access the Public Share

Connect to the Public Shares directory.

Run:

smbclient "//server01.int.arthurlab.com/Public Shares" -U ARTHURLAB/Administrator

List the available files:

ls

Expected output includes:

Documentation on Purchased Items
Softwares
Computer Repair Technician.pdf




Step 8 – Mount the SMB Share

Create a local mount point.

sudo mkdir -p /mnt/share

Mount the network share.

sudo mount -t cifs "//192.168.10.10/Public Shares" /mnt/share \
-o username=Administrator

After authentication, the Windows shared folder is mounted and accessible through the Ubuntu file manager.

Validation Summary
Test	Expected Result	Status
DHCP Address Assigned	Ubuntu receives 192.168.10.x	
smbclient Installed	Successful	
CIFS Utilities Installed	Successful	
Samba Installed	Successful	
SMB Shares Discovered	Successful	
Public Share Accessed	Successful	
Share Mounted	Successful
Lessons Learned

This validation demonstrates successful interoperability between Ubuntu Linux and Windows Server 2022 using the SMB/CIFS protocol. Ubuntu obtained its network configuration from the Windows DHCP service, authenticated to the Active Directory file server using domain credentials, and successfully discovered, accessed, and mounted SMB shares. These results confirm that the ArthurLab environment supports secure cross-platform file sharing and enterprise network integration.
