# VM1 - DNSMasq Server Setup

This file documents the full setup process for VM1, which acts as the DHCP and DNS server using `dnsmasq`.

## 🔧 Virtual Machine Configuration

- **VM software**: UTM on macOS
- **OS**: Ubuntu Server 22.04 LTS (ARM64)
- **Network mode**: Shared Network (NAT)
- **Hostname**: leonardoserver
- **User**: leonardo

## 🛠️ Steps Taken After Installation

### 1. Update the System

```bash
sudo apt update && sudo apt upgrade -y

### 2. Set a Static IP with Netplan

Interface was enp0s1. I edited the config:
sudo nano /etc/netplan/00-installer-config.yaml

Replaced contents with:
network:
  version: 2
  ethernets:
    enp0s1:
      dhcp4: no
      addresses: [192.168.100.1/24]
      gateway4: 192.168.100.1
      nameservers:
        addresses: [8.8.8.8]


Saved and applied:
sudo chmod 600 /etc/netplan/00-installer-config.yaml
sudo netplan apply

Cleared old IP:
sudo ip addr flush dev enp0s1

3. Enabled SSH
To allow access from Mac terminal:
sudo apt install openssh-server -y
sudo systemctl enable --now ssh

4. Connected from Mac Terminal
ssh leonardo@<ip-address>

✅ SSH connection successful — now I can work from the Mac Terminal.
