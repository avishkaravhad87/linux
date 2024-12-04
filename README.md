# Samba Server Installation on Ubuntu

This repository provides a step-by-step guide to install and configure a **Samba server** on **Ubuntu**. Samba allows you to share files and printers between Linux and Windows systems, making it a useful tool for cross-platform file sharing.

## Table of Contents

- [About](#about)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## About

This guide will walk you through the process of installing Samba on Ubuntu to enable file sharing between Ubuntu and Windows systems on the same network. Once configured, you can share directories or printers with other machines using Samba.

---

## Prerequisites

- Ubuntu 18.04 or later (tested on Ubuntu 22.04)
- Sudo or root privileges
- A network connection for accessing the server from other machines (Windows/Linux)

---

## Installation

### Step 1: Update Package List

Open a terminal and make sure your package list is up-to-date.

```bash
sudo apt update
sudo apt install samba
samba --version
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.backup
sudo vim /etc/samba/smb.conf
##At the bottom of the file, add the following configuration to create a share called shared
[shared]
   path = /home/yourusername/shared
   browsable = yes
   writable = yes
   guest ok = yes
   read only = no
mkdir -p /home/<username>/shared
sudo chmod 777 /home/<username>/shared
sudo systemctl restart smbd
sudo systemctl enable smbd
\\ubuntu-ip\shared




