# DNSMasq Ubuntu VM Lab

This is a home lab project to learn how DNSMasq works in a real network environment using two Ubuntu Server VMs.

## 🔧 Project Setup

- **Platform**: macOS with UTM
- **VMs**:
  - `VM1` - DNSMasq server (DHCP + DNS)
  - `VM2` - Client that receives IP and DNS info from VM1
- **Network Mode**: Shared Network (NAT) on both VMs
- **Connection**: SSH from Mac Terminal to VM1 for easier command-line use

## 📁 Directory Structure

dnsmasq-ubuntu-vm-lab/
├── README.md
├── setup/
│ ├── vm1_server_setup.md
│ ├── vm2_client_setup.md
│ └── network_settings.md
├── config/
│ └── dnsmasq.conf
└── notes/
└── ssh_access.md


## 📝 What You'll Learn

- How to assign a static IP to a server using Netplan
- How to configure DNSMasq for DHCP and DNS forwarding
- How to test connectivity between VMs
- How to access and manage servers via SSH

## ✅ Status

- [x] VM1 created
- [x] Static IP assigned
- [x] SSH access working
- [ ] DNSMasq installed and configured
- [ ] VM2 tested as client

## 👨‍💻 Author

[Leonardo Ragazini](https://github.com/leonardoragazini)

