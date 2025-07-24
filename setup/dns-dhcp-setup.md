
---

````markdown
# DNSMasq Project – Setup Details

This file documents the step-by-step setup used to configure two Ubuntu Server VMs in UTM for local DHCP and DNS services using `dnsmasq`.

---

## 🖥️ VM Roles

- **leonardoserver** (`192.168.64.2`) – acts as the DNS and DHCP server
- **ildikoserver** – acts as the DHCP client, receiving IP and DNS from leonardoserver

---

## 🔧 Network Configuration

### Server (`leonardoserver`)
- Static IP set to `192.168.64.2` via Netplan:
  ```yaml
  network:
    version: 2
    renderer: networkd
    ethernets:
      enp0s1:
        dhcp4: no
        addresses:
          - 192.168.64.2/24
        gateway4: 192.168.64.1
        nameservers:
          addresses:
            - 1.1.1.1
            - 8.8.8.8
````

### Client (`ildikoserver`)

* Configured for DHCP via Netplan:

  ```yaml
  network:
    version: 2
    renderer: networkd
    ethernets:
      enp0s1:
        dhcp4: yes
  ```

---

## 📦 DNSMasq Configuration (on Server)

Located at `/etc/dnsmasq.conf`:

```ini
interface=enp0s1
dhcp-range=192.168.64.50,192.168.64.100,12h
domain=lab.local
dhcp-option=3,192.168.64.2       # Default gateway
dhcp-option=6,192.168.64.2       # DNS server
```

> `dnsmasq` listens on `enp0s1`, serves IPs in the 64.50–64.100 range, and acts as both gateway and DNS for the client.

---

## ✅ Results

* Client VM received IP from the server
* Client was able to resolve DNS (e.g., `ping google.com`)
* Server confirmed running `dnsmasq` successfully after resolving port conflict

---

## 📁 File Index

* `server-netplan.yaml` – Server’s Netplan file
* `client-netplan.yaml` – Client’s Netplan file
* `dnsmasq.conf` – dnsmasq configuration
* `README.md` – This file

```

---

```
