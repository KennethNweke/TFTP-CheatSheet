# 🛠 Cisco Config Backup & Restore via TFTP

This cheat sheet is a companion to my LinkedIn video on backing up Cisco device configurations using a TFTP server. It’s designed to help network engineers and students quickly recall the commands and setup steps needed to:

- Back up running or startup configurations to a TFTP server
- Restore configurations from TFTP back to a Cisco device
- Troubleshoot common TFTP-related issues
- Understand basic security considerations

TFTP is a lightweight and fast protocol, commonly used in lab and trusted network environments for configuration transfers. This guide walks you through practical, tested examples for real-world use.

> ⚠️ Note: TFTP lacks authentication and encryption — avoid using it in untrusted or production environments without additional security measures.<br>




## 🖥 Sample Topology
Below is a simple network topology used to demonstrate the TFTP configuration backup process:
![image](https://github.com/user-attachments/assets/1e8a1ab8-ea05-4adf-96d9-dde7fdc42e7d)

## 📌 Prerequisites

Before performing backup or restore operations, ensure the following requirements are met:

✅ **TFTP server is installed and running**
  - Examples: [TFTPD32](http://tftpd32.jounin.net/), SolarWinds TFTP (Windows), or `tftp-hpa` (Linux)
✅ **TFTP server is reachable** from the Cisco device via IP
✅ **Correct folder permissions** are set on the TFTP server's root directory
✅ **Firewall rules allow TFTP traffic**
  - **UDP Port 69** must be open
  - Source: Cisco device IP  
  - Destination: TFTP server IP

> 💡 Tip: Test connectivity with `ping <TFTP server IP>` from the Cisco device to verify reachability before initiating any transfer.
