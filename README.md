# SAMBA Server Setup Guide

This guide provides step-by-step instructions to set up a Samba server on a Linux machine. Samba is a utility/tool that allows sharing Linux files and print services with other operating systems using SMB (Server Message Block) and CIFS (Common Internet File System) protocols.

---

## **1. Installing Samba**

To install Samba and its dependencies, run the following command:

```bash
yum install samba samba-client samba-common -y

Enabling Samba Through Firewall
firewall-cmd --permanent --zone=public --add-service=samba
firewall-cmd --reload

If Firewall Commands Are Not Working:
Install the firewall packages:

RHEL/CentOS/AlmaLinux/Rocky Linux:
sudo yum install firewalld -y
Ubuntu/Debian:
sudo apt update
sudo apt install firewalld -y
Then enable and start the firewall service:
sudo systemctl enable firewalld
sudo systemctl start firewalld
3. Setting Up the Samba Directory
Create the Directory:
mkdir -p /samba/apps
Navigate to the directory:
cd /samba
mkdir apps
Create a Test File:
touch samba/apps/samba_testfile
Grant Permissions:
chmod a+rwx samba/
chmod a+rwx samba/apps/
chmod a+rwx samba/apps/*
 Handling SELinux
If SELinux is enabled, adjust the security context for the Samba shared directory.

Change the Security Context:
chcon -t samba_share_t /samba/apps
If chcon Does Not Work:
Verify SELinux status:
getenforce
Ensure the directory exists:
ls -ld /samba/apps
Use the restorecon command:
sudo restorecon -Rv /samba/apps
5. Configuring Samba
Edit the smb.conf file located at /etc/samba/smb.conf and add the following configuration:
[global]
    workgroup = SAMBA
    netbios name = amazon linux
    security = user
    map to guest = bad user
    dns proxy = no

[apps]
    comment = Shared Directory
    path = /samba/apps
    browsable = yes
    writable = yes
    guest ok = yes
    guest only = yes
    read only = no
Test the Configuration:
testparm

Here is the README.md file formatted for your GitHub repository:

markdown
Copy code
# SAMBA Server Setup Guide

This guide provides step-by-step instructions to set up a Samba server on a Linux machine. Samba is a utility/tool that allows sharing Linux files and print services with other operating systems using SMB (Server Message Block) and CIFS (Common Internet File System) protocols.

---

## **1. Installing Samba**

To install Samba and its dependencies, run the following command:

```bash
yum install samba samba-client samba-common -y
2. Enabling Samba Through Firewall
Allow Samba services through the firewall and reload the firewall configuration:

bash
Copy code
firewall-cmd --permanent --zone=public --add-service=samba
firewall-cmd --reload
If Firewall Commands Are Not Working:
Install the firewall packages:

RHEL/CentOS/AlmaLinux/Rocky Linux:
bash
Copy code
sudo yum install firewalld -y
Ubuntu/Debian:
bash
Copy code
sudo apt update
sudo apt install firewalld -y
Then enable and start the firewall service:

bash
Copy code
sudo systemctl enable firewalld
sudo systemctl start firewalld
3. Setting Up the Samba Directory
Create the Directory:
bash
Copy code
mkdir -p /samba/apps
Navigate to the directory:

bash
Copy code
cd /samba
mkdir apps
Create a Test File:
bash
Copy code
touch samba/apps/samba_testfile
Grant Permissions:
bash
Copy code
chmod a+rwx samba/
chmod a+rwx samba/apps/
chmod a+rwx samba/apps/*
4. Handling SELinux
If SELinux is enabled, adjust the security context for the Samba shared directory.

Change the Security Context:
bash
Copy code
chcon -t samba_share_t /samba/apps
If chcon Does Not Work:
Verify SELinux status:
bash
Copy code
getenforce
Ensure the directory exists:
bash
Copy code
ls -ld /samba/apps
Use the restorecon command:
bash
Copy code
sudo restorecon -Rv /samba/apps
5. Configuring Samba
Edit the smb.conf file located at /etc/samba/smb.conf and add the following configuration:

ini
Copy code
[global]
    workgroup = SAMBA
    netbios name = amazon linux
    security = user
    map to guest = bad user
    dns proxy = no

[apps]
    comment = Shared Directory
    path = /samba/apps
    browsable = yes
    writable = yes
    guest ok = yes
    guest only = yes
    read only = no
Test the Configuration:
bash
Copy code
testparm
6. Enable and Start Samba Services
Run the following commands to enable and start the Samba services:
systemctl enable smb nmb
systemctl start smb nmb
Conclusion
This guide helps set up a Samba server to share directories between Linux and Windows systems. Follow these steps carefully, and your Samba server will be up and running in no time!

