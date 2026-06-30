AD DS, DNS, and DHCP Installation Configuration
Overview

This document describes the main configuration steps for Active Directory Domain Services (AD DS), DNS, and DHCP in the ArthurLab Virtual Enterprise Network.

The Windows Server 2022 system, SERVER01, was configured as the domain controller, DNS server, and DHCP server for the internal lab network.

1. Server Name and Static IP Configuration

The server was renamed to:

SERVER01

The server was assigned a static IPv4 address.

Setting	Value
Server Name	SERVER01
IP Address	192.168.10.10
Subnet Mask	255.255.255.0
Preferred DNS	192.168.10.10
FQDN	server01.int.arthurlab.com

Verification command:

ipconfig /all
hostname

Expected result:

Hostname shows SERVER01
IPv4 address shows 192.168.10.10
DNS server points to 192.168.10.10


2. Domain Name and NetBIOS Name

The Active Directory domain was configured as:

Item	Value
Domain Name	int.arthurlab.com
Domain Controller FQDN	server01.int.arthurlab.com
NetBIOS Name	ARTHURLAB

The domain name was selected to represent an internal enterprise lab environment.

3. AD DS Role Installation

The Active Directory Domain Services role was installed using Server Manager.

Steps:

Open Server Manager.
Select Add Roles and Features.
Choose Role-based or feature-based installation.
Select SERVER01.
Install Active Directory Domain Services.
Promote the server to a domain controller.
Create a new forest using:
int.arthurlab.com

Expected result:

SERVER01 becomes the domain controller.
The int.arthurlab.com domain is created.
Active Directory Users and Computers becomes available.
SYSVOL and NETLOGON shares are created.

Verification command:

Get-ADDomain
Get-ADDomainController


4. DNS Configuration

DNS was installed with Active Directory and configured to support domain name resolution for the lab.

The DNS zone created was:

int.arthurlab.com

The server record should resolve as:

server01.int.arthurlab.com

Verification commands:

nslookup server01.int.arthurlab.com
nslookup int.arthurlab.com

Expected result:

Name: server01.int.arthurlab.com
Address: 192.168.10.10


5. DHCP Scope Configuration

The DHCP role was installed on SERVER01 to automatically assign IP addresses to client machines.

DHCP Setting	Value
Scope Name	ArthurLab-Scope
Network	192.168.10.0/24
Start IP	192.168.10.100
End IP	192.168.10.200
Subnet Mask	255.255.255.0
DNS Server	192.168.10.10
Domain Name	int.arthurlab.com

The DHCP server was authorized in Active Directory.

Expected result:

Windows and Ubuntu clients receive 192.168.10.x addresses.
Clients use SERVER01 as their DNS server.
Clients can resolve int.arthurlab.com.

Verification commands on Windows clients:

ipconfig /release
ipconfig /renew
ipconfig /all


6. Client DNS Settings

Windows clients were configured to use DHCP so they could automatically receive the correct IP address and DNS configuration from SERVER01.

Client DNS should point to:

192.168.10.10

Verification command:

ipconfig /all

Expected result:

DHCP Enabled: Yes
IPv4 Address: 192.168.10.x
DNS Server: 192.168.10.10
Connection-specific DNS suffix: int.arthurlab.com
7. Validation Checklist
Component	Test	Expected Result	Status
Server Name	hostname	Shows SERVER01	Complete
Static IP	ipconfig /all	Shows 192.168.10.10	Complete
AD DS	Get-ADDomain	Shows int.arthurlab.com	Complete
DNS	nslookup server01.int.arthurlab.com	Resolves to 192.168.10.10	Complete
DHCP	Client ipconfig /all	Client receives 192.168.10.x	Complete
Client DNS	Client DNS setting	Points to 192.168.10.10	Complete
