# Secure DNS Server Configuration

## 📌 Introduction
[cite_start]This project focuses on configuring a DNS server with the DNSCrypt protocol[cite: 12]. [cite_start]The primary goal is to alleviate threats like surveillance and spoofing that exist in traditional plaintext DNS queries[cite: 11]. [cite_start]The Linux-based server provides DNS responses to a local network, safely redirects them to an upstream resolver, and ensures privacy and data integrity[cite: 13].

## 🏗️ System Architecture & Environment
* [cite_start]**Server Environment:** Kali Linux (Kernel 6.x) [cite: 15]
* [cite_start]**Server IP Address:** `192.168.45.82` [cite: 16]
* [cite_start]**Client Environment:** Windows 11 [cite: 20]

## 🛠️ Software Components
* [cite_start]**Unbound:** Handles local caching and validation[cite: 18].
* [cite_start]**DNSCrypt-proxy:** Encrypts queries before sending them to the internet[cite: 19].

## 🚀 Implementation & Configuration Steps

### 1. Service Status Verification
[cite_start]Verified that both the `unbound.service` and `dnscrypt-proxy.service` are active and running[cite: 23]. [cite_start]The handshake with the upstream resolver (Cloudflare) was successful[cite: 24].
```bash
sudo systemctl status unbound dnscrypt-proxy
2. Port Listening ConfigurationConfirmed that Unbound is listening on standard DNS port 53, and DNSCrypt-proxy is listening on the local port 5353.Bashsudo netstat -tulnp | grep -E '53|5353'
3. Local Server Resolution TestPerformed a loopback test on the server to confirm the local resolver stack was functioning correctly.Bashnslookup google.com 127.0.0.1
4. Client-Side Configuration (Windows)Configured the Windows 11 client to bypass the default ISP DNS and use the custom Kali Linux server.DOSnetsh interface ip set dns "Wi-Fi" static 192.168.45.82
🛡️ Security Validation & ResultsA standard lookup confirmed the server was reachable from the client (nslookup google.com). Crucially, a browser-based DNS Leak Test was performed via dnsleaktest.com to validate encryption.Although the physical internet connection belongs to a local ISP, the leak test successfully identified the ISP as Cloudflare. This confirms:Traffic Encryption: The local ISP cannot view the requested domain names; it only observes encrypted traffic to the DNSCrypt server.No Leaks: The Windows machine did not revert to default DNS servers, indicating a strong configuration.
