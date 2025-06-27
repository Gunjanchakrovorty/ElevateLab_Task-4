# 🔥 Cyber Security Internship – Task 4

## 🛡️ Configure and Use a Firewall on Windows/Linux

This task focuses on learning how to configure a firewall using either **UFW (Linux)** or **Windows Defender Firewall**. The goal is to understand how firewalls work, how to allow/deny traffic on ports like **22 (SSH)** and **23 (Telnet)**, and to build the skills to analyze, document, and secure system traffic rules.

---

## 🎯 Objective

- Block and allow traffic on selected ports.
- Test firewall effectiveness using telnet/SSH.
- Learn rule syntax and GUI workflows.
- Demonstrate configuration with screenshots.
- Understand real-world firewall scenarios.

---

## 📘 Key Concepts

- **Inbound & Outbound Rules**
- **Port Blocking & Allowing**
- **Stateless vs Stateful Firewalls**
- **UFW for Linux**
- **Windows Defender Firewall GUI & PowerShell**
- **Network Attack Surface Reduction**

---

## 🛠 Tools Used

| Tool | Platform | Purpose |
|------|----------|---------|
| **UFW (Uncomplicated Firewall)** | Linux | Easy firewall control |
| **Windows Defender Firewall** | Windows | GUI & PowerShell for firewall config |
| **Telnet / Netcat / SSH** | Both | Port testing |
| **Event Viewer / Logs** | Windows | Firewall diagnostics |
| **UFW Logs** | Linux | `/var/log/ufw.log` to track activity |

---

## 🧱 Setup Steps

### 🔹 On Linux (UFW)

```bash
# Enable the firewall
sudo ufw enable

# Block inbound traffic on port 23 (Telnet)
sudo ufw deny 23

# Allow SSH on port 22
sudo ufw allow 22

# Check rules
sudo ufw status verbose

# Remove test block
sudo ufw delete deny 23

# Block an IP address
sudo ufw deny from 203.0.113.5

# Enable logging
sudo ufw logging on


🪟 On Windows (PowerShell)
powershell
Copy
Edit
# Block port 23
New-NetFirewallRule -DisplayName "Block Telnet" -Direction Inbound -Protocol TCP -LocalPort 23 -Action Block

# Allow port 22 (SSH)
New-NetFirewallRule -DisplayName "Allow SSH" -Direction Inbound -Protocol TCP -LocalPort 22 -Action Allow

# View rules
Get-NetFirewallRule | Where-Object {$_.DisplayName -like "*Telnet*"}

# Remove rule
Remove-NetFirewallRule -DisplayName "Block Telnet"


🧪 Testing the Firewall

| Test              | Command               | Expected Result                     |
| ----------------- | --------------------- | ----------------------------------- |
| Telnet on port 23 | `telnet localhost 23` | ❌ Connection refused                |
| SSH on port 22    | `ssh user@localhost`  | ✅ Connection allowed                |
| Ping blocked IP   | `ping 203.0.113.5`    | ❌ Request timed out (if IP blocked) |

🔁 Real-World Use Cases
| Use Case                     | Rule                                       |
| ---------------------------- | ------------------------------------------ |
| Block insecure remote access | Deny port 23 (Telnet)                      |
| Secure SSH access            | Allow port 22                              |
| Block known malicious IP     | Deny from IP                               |
| Log access attempts          | `ufw logging on` or enable Windows logging |
