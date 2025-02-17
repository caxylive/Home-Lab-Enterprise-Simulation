# Troubleshooting ProxMox WiFi Connectivity
- ProxMox is intentionally designed to connect to your router via an Ethernet Cable.
- Therefore, ProxMox does not come with any WiFi connectivity.
- However, some of us may find that running an Ethernet Cable in our room may not be feasible.
- That being said, please connect ProxMox to your router via Ethernet whenever you can and avoid using WiFi connection.
- So let's get started troubleshooting.

## Step-by-Step Configuration
### 1) Edit Network Configuration File:
- Open the /etc/network/interface file with a text editor:
```bash
nano /etc/network/interfaces
```

### 2) Add/Modify Configuration:
- Add or modify the configuration to look like this:
```Plaintext
auto lo
iface lo inet loopback

auto wlx54c57a381134
iface wlx54c57a381134 inet manual

auto vmbr0
iface vmbr0 inet static
  address 192.168.101.99/24
  bridge-ports none
  bridge-stp off
  bridge-fd 0
  post-up   echo 1 > /proc/sys/net/ipv4/ip_forward
  post-up   iptables -t nat -A POSTROUTING -s '192.168.101.0/24' -o wlx54c57a381134 -j MASQUERADE
  post-down iptables -t nat -D POSTROUTING -s '192.168.101.0/24' -o wlx54c57a381134 -j MASQUERADE
  post-up   iptables -t raw -I PREROUTING -i fwbr+ -j CT --zone 1
  post-down iptables -t raw -D PREROUTING -i fwbr+ -j CT --zone 1

source /etc/network/interfaces.d/*
```

### 3) Configure Wi-Fi Using ```wpa_supplicant```:
- Create or edit the /etc/wpa_supplicant/wpa_supplicant.conf file:
```bash
nano /etc/wpa_supplicant/wpa_supplicant.conf
```
- Add your WiFi network details:
```Plaintext
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
    ssid="your_SSID"
    psk="your_password"
}
```

### 4) Start the WiFi Connection:
```bash
ip link set dev wlx54c57a381134 up
wpa_supplicant -B -i wlx54c57a381134 -c /etc/wpa_supplicant/wpa_supplicant.conf
dhclient wlx54c57a381134
```

### 5) Apply the Configuration:
- Restart the network service:
  ```bash
  systemctl restart networking
  ```

# Reference:
1) https://forum.proxmox.com/threads/proxmox-over-wifi-wlan.123805/

