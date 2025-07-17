# VM2 - DHCP Client Setup

This file documents the full setup process for VM2, which acts as a DHCP and DNS client in the DNSMasq test lab.

## 🔧 Virtual Machine Configuration

- **VM software**: UTM on macOS
- **OS**: Ubuntu Server 22.04 LTS (ARM64)
- **Network mode**: Shared Network (NAT)
- **Hostname**: ubuntu-client
- **User**: leonardo

## 🛠️ Steps Taken After Installation

### 1. System Update

Updated all packages:

```bash
sudo apt update && sudo apt upgrade -y
```

### 2. DHCP Networking (Default)

The interface was left on automatic (DHCP), which is the default in Ubuntu Server. No changes were made to Netplan.

To confirm DHCP assignment:

```bash
ip a
```

If no IP in the `192.168.100.x` range was shown, I manually requested one:

```bash
sudo dhclient
```

### 3. Testing DHCP and DNS

Once VM1 was running `dnsmasq`, I confirmed that VM2 received an IP and could resolve domain names:

```bash
ping 192.168.100.1      # Tests connection to VM1
ping google.com         # Tests DNS resolution
```

Both commands worked as expected, confirming successful DHCP and DNS setup.

### 4. Optional: Enable SSH

```bash
sudo apt install openssh-server -y
sudo systemctl enable --now ssh
```

This allows remote login from my Mac if needed.

