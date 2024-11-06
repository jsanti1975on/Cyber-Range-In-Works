# pfSense Shell Command Interface Project

This project provides a simple web-based interface to execute commands on a **pfSense firewall** via SSH. It includes an authentication challenge, a command execution page, and a Python backend server to handle SSH connections. This setup is ideal for controlled remote access to pfSense command-line operations and demonstrates secure command execution.

---

## Project Overview

The goal of this project is to:

- Set up a web interface that authenticates the user.
- Enable the user to execute a set of commands on pfSense through the interface.
- Use SSH key-based authentication for secure, passwordless command execution on pfSense.
- Implement optional security enhancements, such as command restrictions, logging, and HTTPS.

---

## Prerequisites

- **pfSense Firewall**: Configured with SSH access.
- **Raspberry Pi (or other Linux-based host)**: Used to host the Python server and web interface.
- **Python 3**: Installed on the Raspberry Pi with the `paramiko` library for SSH.
![command execution](https://github.com/user-attachments/assets/62bc355f-19d3-41dd-883c-4ddd1049dbf7)
![PfSense Shell Page](https://github.com/user-attachments/assets/5600413a-3d26-4e3c-8b52-c94602ca1333)
![PiHole-Proper-Config](https://github.com/user-attachments/assets/39278df9-0953-4cfd-8d27-9f780bf18923)
![powershell-shows-server](https://github.com/user-attachments/assets/ea58d043-7881-441a-aa20-a1a3499b781d)
![run a command interface](https://github.com/user-attachments/assets/aa1f8656-9fab-4aca-a778-5e5188a40dc7)
