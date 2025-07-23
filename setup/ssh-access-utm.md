Perfect — here’s the **plain text** for your new file `ssh-access-utm.md`, ready to be copied directly into your terminal editor (like `nano` or `vim`):

---

````markdown
# SSH Access to UTM VM (Bridged Networking Mode)

This guide documents how I configured SSH access from my macOS host to the DNSMasq Ubuntu Server VM (VM1) using Bridged Networking in UTM.

---

## 🛠️ Steps Taken

### 1. Switched to Bridged Mode in UTM
- Opened UTM and selected the VM (VM1).
- Went to `Settings > Network`.
- Set:
  - **Network Mode**: `Bridged (Advanced)`
  - **Bridged Interface**: `en0` (my Wi-Fi adapter)
  - **Emulated Network Card**: `virtio-net-pci`
- Saved the changes and **restarted the VM**.

---

### 2. Removed Static IP Configuration from Netplan
Edited `/etc/netplan/00-installer-config.yaml` on the VM to use DHCP:

```yaml
network:
  version: 2
  ethernets:
    enp0s1:
      dhcp4: true
````

Applied changes:

```bash
sudo netplan apply
```

---

### 3. Verified the New IP

Checked the new IP assigned via DHCP:

```bash
ip a
```

Got: `192.168.64.2` (back in the UTM NAT range — ideal for this config)

---

### 4. Confirmed SSH Service

Checked if SSH was running:

```bash
sudo systemctl status ssh
```

It was already **active (running)**.

---

### 5. Connected from Host (macOS)

From my Mac terminal, I ran:

```bash
ssh leonardo@192.168.64.2
```

And successfully logged in 🎉

---

## ✅ Notes

* Make sure firewall rules are set to allow SSH.
* If anything fails, restarting the VM after netplan changes often helps.
* This configuration avoids setting a static IP, letting UTM handle the subnet.
