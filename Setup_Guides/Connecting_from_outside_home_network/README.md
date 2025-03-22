## 1. Map the Network

* Start with the home router:
  * Access your home router's admin panel to check its WAN IP. This will confirm the IP assigned to your router by your cousin’s network.
  * Note the local IP of your Proxmox server on your home network.

* Trace the connection to your cousin's router:
  * Use a tool like tracert (Windows) or traceroute (Linux/Mac) to see the network path between your home and the internet.
  * Identify the intermediate hops, one of which should be your cousin's router.
 
---

## 2. Assess Port Forwarding

* Check if there are any existing open ports:
  * Use tools like Nmap or online scanners (e.g., "YouGetSignal") to see if ports on your WAN IP (provided by your cousin’s router) are open.
  * If Proxmox's default port (8006) is already open, test it directly in your browser with your WAN IP, e.g., `https://<WAN_IP>:8006`.

* If no ports are open:
  * You’ll need access to your home router’s admin panel to forward a port (e.g., 8006) to your Proxmox server's local IP.
  * Without direct access to your cousin’s router, you'll rely on scanning for open ports or exploring alternative access methods.
 
---

## 3. Use Dynamic DNS (if available)

* If your cousin's WAN IP changes frequently (dynamic IP), you’ll need a consistent hostname to access it externally.

* Check if your home router or Proxmox server supports a DDNS service (e.g., No-IP, DynDNS). If not, you can manually track the WAN IP until you’re ready for a more advanced setup.

---

## 4. Consider Secure Alternatives

* If port forwarding proves challenging:
  * Set up a reverse SSH tunnel or use a cloud tunneling service like ngrok or Cloudflare Tunnel to expose your Proxmox server securely to the internet.
  * These options bypass the need for direct port forwarding but require initial configuration from your home network.

---

## 5. Test Your Setup

* Once you identify an accessible path, use a browser or tool like `curl` to connect to your Proxmox Web GUI from outside your network.
* Ensure security by enabling HTTPS, using strong passwords, and limiting access via firewall rules.







