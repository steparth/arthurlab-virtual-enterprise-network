Configure Network Settings

Both Windows clients were connected to the ArthurLab Internal Network.

Network Adapter:

Attached to: Internal Network
Network Name: ArthurLab

Obtain IP settings automatically using DHCP.

Verify using:

ipconfig /all

Expected result:

DHCP Enabled: Yes
IPv4 Address: 192.168.10.x
DNS Server: 192.168.10.10


3. Verify DNS Resolution

Before joining the domain, verify that the client can locate the domain controller.

Run:

nslookup server01.int.arthurlab.com

Expected result:

Name: server01.int.arthurlab.com
Address: 192.168.10.10

Successful DNS resolution confirms that the client can locate the domain controller.

4. Joining  the Domain

Open:

Settings → System → About → Rename this PC (Advanced)

or

System Properties → Computer Name → Change

Select:

Domain

Enter:

int.arthurlab.com

When prompted, enter domain administrator credentials.

Example:

Username:
ARTHURLAB\Administrator

After successful authentication, Windows displays:

Welcome to the int.arthurlab.com domain.

Restart the computer.



5. Sign In Using a Domain Account

After restarting, select Other user.

Log in using a domain account.

ARTHURLAB\stephen.admin

or

stephen.admin@int.arthurlab.com
6. Verify Domain Membership

Open Command Prompt.

Run:

whoami

Expected result:

arthurlab\stephen.admin

Verify the computer has joined the domain:

systeminfo


Expected result:

ARTHURLAB



7. Verify Active Directory

On SERVER01, open Active Directory Users and Computers.

Navigate to:

Computers

Verify that:

WIN11-PC1
WIN10-PC2

appear as domain-joined computer objects.



Validation Checklist
Test	Expected Result	Status
DHCP Address Assigned	Client receives 192.168.10.x	Complete
DNS Resolution	Domain controller resolves correctly	Complete
Domain Join	Client joins int.arthurlab.com	Complete
Domain Login	User authenticates successfully	Complete
Active Directory	Client appears in ADUC	Complete
