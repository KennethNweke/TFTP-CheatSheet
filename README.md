# 🛠 Cisco Config Backup & Restore via TFTP

This cheat sheet is a companion to my LinkedIn video on backing up Cisco device configurations using a TFTP server. It’s designed to help network engineers and students quickly recall the commands and setup steps needed to:

- Back up running or startup configurations to a TFTP server
- Restore configurations from TFTP back to a Cisco device
- Troubleshoot common TFTP-related issues
- Understand basic security considerations

TFTP is a lightweight and fast protocol, commonly used in lab and trusted network environments for configuration transfers. This guide walks you through practical, tested examples for real-world use.

> ⚠️ Note: TFTP lacks authentication and encryption — avoid using it in untrusted or production environments without additional security measures.


## 🖥 Sample Topology
Below is a simple network topology used to demonstrate the TFTP configuration backup process.
![image](https://github.com/user-attachments/assets/1e8a1ab8-ea05-4adf-96d9-dde7fdc42e7d)

## 📌 Prerequisites

Before performing backup or restore operations, ensure the following requirements are met:

✅ **TFTP server is installed and running**
  - Examples: [TFTPD32](http://tftpd32.jounin.net/), SolarWinds TFTP (Windows), or `tftp-hpa` (Linux)
- ✅ **TFTP server is reachable** from the Cisco device via IP
- ✅ **Correct folder permissions** are set on the TFTP server's root directory
- ✅ **Firewall rules allow TFTP traffic**
  - **UDP Port 69** must be open
  - Source: Cisco device IP  
  - Destination: TFTP server IP

> 💡 Tip: Test connectivity with `ping <TFTP server IP>` from the Cisco device to verify reachability before initiating any transfer.

##
##
## 🔁 Backing Up Cisco Configuration to TFTP

### 1. Backing up Running Configuration
```bash
copy running-config tftp:
```
Prompts:
 - Address or name of remote host? → 192.168.1.100
 - Destination filename? → rtr1-running-config

### 2. Backing up Startup Configuration
```bash
copy startup-config tftp:
```
##
##
## 🔄 Restoring Configuration from TFTP
### 1. Restoring to Running Configuration
```bash
copy tftp: running-config
```
Prompts:
 - Address or name of remote host? → 192.168.1.100
 - Source filename? → rtr1-running-config
### 2. Restoring to Startup Configuration
```bash
copy tftp: startup-config
```

## 🧰 Example Session
```plaintext
Router# copy running-config tftp:
Address or name of remote host []? 192.168.1.100
Destination filename [running-config]? rtr1-backup
!!
1234 bytes copied in 2.345 secs (526 bytes/sec)
```

## ⚠️ Common Issues & Fixes
| Issue                       | Cause                               | Fix                                      |
|----------------------------|-------------------------------------|------------------------------------------|
| `%Error opening tftp://...` | File not found or permission denied | Check file path, firewall, access rights |
| Timeout                    | Device can’t reach TFTP server      | Check routing, ping the server           |
| Incomplete copy            | Server folder is read-only or full  | Ensure folder permissions and space      |

## 🔐 Security Notes
 - TFTP is insecure (no authentication or encryption).
 - Use SCP or SFTP for secure environments:
```bash
copy running-config scp:
```
