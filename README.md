
# ArthurLab Virtual Enterprise Network

A reproducible Windows Server home lab demonstrating **Active Directory Domain Services (AD DS)**, **DNS**, **DHCP**, **Group Policy**, **SMB file services**, and **Ubuntu SMB/CIFS validation**.

## Project Summary

ArthurLab is a VirtualBox-based lab built to simulate a small enterprise network. The environment uses **Windows Server 2022** as the central domain controller and service host, with **Windows 10/11** and **Ubuntu** clients used to validate domain membership, network services, file sharing, and cross-platform interoperability.

## Architecture

| Component      | Configuration                          |
| -------------- | -------------------------------------- |
| Virtualization | Oracle VirtualBox                      |
| Domain         | `int.arthurlab.com`                    |
| Server FQDN    | `server01.int.arthurlab.com`           |
| Server         | `SERVER01` running Windows Server 2022 |
| Server IP      | `192.168.10.10`                        |
| Subnet         | `192.168.10.0/24`                      |
| Clients        | Windows 11, Windows 10, Ubuntu         |

## Network Diagram


Flowchart TD
    Internet[Internet / Updates] --> Host[VirtualBox Host]
    Host --> ArthurLab[Internal Network: ArthurLab<br/>192.168.10.0/24]

    ArthurLab --> Server[SERVER01<br/>Windows Server 2022<br/>192.168.10.10<br/>server01.int.arthurlab.com]

    Server --> AD[AD DS<br/>int.arthurlab.com]
    Server --> DNS[DNS]
    Server --> DHCP[DHCP]
    Server --> SMB[SMB Shares]

    ArthurLab --> Win11[WIN11-PC1<br/>Domain Join + GPO Test]
    ArthurLab --> Win10[WIN10-PC2<br/>Domain Join + Lease Test]
    ArthurLab --> Ubuntu[UBUNTU-01<br/>SMB/CIFS + DNS Test]
```

## What This Project Demonstrates

* Built a Windows Server domain controller from scratch.
* Configured AD DS, DNS, and DHCP for an isolated lab network.
* Joined Windows 10/11 clients to the domain.
* Created users, OUs, and Group Policy Objects.
* Applied an account lockout policy and validated enforcement.
* Created SMB shares for Public, IT, and HR use cases.
* Tested Linux interoperability using `smbclient`, `cifs-utils`, and Samba.
* Documented the full build with screenshots, diagrams, and verification notes.

## Repository Structure


arthurlab-virtual-enterprise-network/
├── README.md
├── docs/
│   ├── installation-steps.md
│   ├── ad-dns-dhcp-configuration.md
│   ├── group-policy-and-security.md
│   ├── file-services-smb.md
│   ├── ubuntu-smb-cifs-validation.md
│   └── troubleshooting.md
├── diagrams/
│   └── arthurlab-network.mmd
├── screenshots/
│   ├── 01-environment/
│   ├── 02-ad-dns-dhcp/
│   ├── 03-domain-join/
│   ├── 04-gpo-security/
│   ├── 05-file-services/
│   └── 06-ubuntu-validation/
├── configs/
├── reports/
└── .gitignore
```

## Verification Matrix

| Component    | Evidence to Show                    | Expected Result                          | Status   |
| ------------ | ----------------------------------- | ---------------------------------------- | -------- |
| AD DS        | ADUC users/computers                | Domain objects present                   | Complete |
| DNS          | FQDN/domain lookup                  | Clients resolve lab names                | Complete |
| DHCP         | Address leases                      | Clients receive `192.168.10.x` addresses | Complete |
| Windows Join | System properties                   | Domain shows `int.arthurlab.com`         | Complete |
| Group Policy | Policy settings + `gpupdate /force` | Security/desktop rules apply             | Complete |
| SMB Shares   | Share inventory + permissions       | Access aligns with users/groups          | Complete |
| Ubuntu       | `ip addr`, `smbclient`, CIFS tools  | Linux client can discover Windows shares | Complete |

## Screenshots

Place screenshots under the matching folders. Use clear names such as:

* `01-server-static-ip.png`
* `02-ad-ds-role-installed.png`
* `03-dhcp-scope-created.png`
* `04-windows-11-domain-joined.png`
* `05-account-lockout-policy.png`
* `06-smb-share-permissions.png`
* `07-ubuntu-smbclient-validation.png`

## Skills Highlighted

* Windows Server Administration
* Active Directory
* DNS
* DHCP
* Group Policy
* SMB File Services
* Linux Interoperability
* VirtualBox Networking
* Technical Documentation
* Troubleshooting


