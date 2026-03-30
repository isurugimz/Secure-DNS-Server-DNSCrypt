🔐 Secure DNS Server Configuration
📌 Introduction

This project demonstrates how to configure a secure DNS server using the DNSCrypt protocol. The main goal is to protect DNS queries from threats such as surveillance and spoofing.

The system uses a Linux-based server to:

Provide DNS resolution for a local network
Securely forward queries to an upstream resolver
Ensure privacy and data integrity
🏗️ System Architecture & Environment
Component	Details
Server OS	Kali Linux (Kernel 6.x)
Server IP	192.168.45.82
Client OS	Windows 11
🛠️ Software Components
Unbound → Local DNS resolver with caching and validation
DNSCrypt-proxy → Encrypts DNS queries before sending to the internet
🚀 Implementation Steps
1️⃣ Verify Services

Ensure both services are running:

sudo systemctl status unbound dnscrypt-proxy
2️⃣ Check Listening Ports

Verify correct port usage:

sudo netstat -tulnp | grep -E '53|5353'
Port 53 → Unbound
Port 5353 → DNSCrypt-proxy
3️⃣ Test Local DNS Resolution
nslookup google.com 127.0.0.1
4️⃣ Configure Windows Client

Set the DNS server manually:

netsh interface ip set dns "Wi-Fi" static 192.168.45.82
🛡️ Security Validation

A DNS leak test was performed using:
👉 https://www.dnsleaktest.com/

✅ Results
Traffic Encryption: DNS queries are encrypted using DNSCrypt
Privacy Protection: ISP cannot see requested domains
No DNS Leaks: Client does not fall back to default DNS
📊 Outcome
Secure DNS resolution implemented successfully
Improved privacy and protection against spoofing attacks
Verified encrypted communication with upstream resolver
📚 Future Improvements
Add firewall rules (UFW/iptables)
Implement DNSSEC validation
Monitor traffic using tools like Wireshark
Add logging and alerting
