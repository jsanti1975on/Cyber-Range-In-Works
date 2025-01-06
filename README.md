![work-in-progress](https://github.com/user-attachments/assets/b8b88426-cb0e-419d-9c8a-20fcc47d4c5a)
```
!!! Works In Progress - I am taking my 2nd Linux course along with Information Security this spring semester 2025.
- From cyber labs to cyber ranges to cyber stadiums - I plan on the range {^_^} LOOKEY_Flag.
```
# CyberLab Dashboard - Raspberry Pi 4 Project

## Overview

This repository hosts the source code and configuration files for the **CyberLab Dashboard**, which runs on a **Raspberry Pi 4** with **Debian Bookworm 12** installed. The Raspberry Pi also runs **Pi-hole** to act as a web application, integrating network security and file automation features. Note: The Dashboard is now part of a larger project!

## Project Structure

The project includes a dashboard designed to combine **Pi-hole** data with trace tools to enhance network analysis and security visualization capabilities. Additionally, the dashboard supports file uploads and organizes specific types of files into designated directories for further processing.

### Key Features:
- **Pi-hole integration**: Provides DNS-level ad blocking and network monitoring.
- **File Automation**: Automates sorting and moving of files based on extensions or prefixes.
- **RSS Feed Display**: Fetches and displays the latest cybersecurity news.
- **Authentication Challenge**: A simple challenge that users must solve to access restricted pages.
- **Custom HTTP Server**: Built-in HTTP server for handling file uploads and serving the dashboard.

## Project Files

- `index.html`: The main dashboard interface for the CyberLab project.
- `server.py`: A custom Python HTTP server handling file uploads and providing a web interface.
- **Directories**:
    - `css/`: CSS files for styling the dashboard.
    - `images/`: Images used on the dashboard.
    - `scripts/`: Script files, auto-organized from uploads.
    - `uploads/`: Directory for uploaded files.
    - `CompTIA/`, `Cisco/`, `Windows-Server/`, `vSphere/`, `CyberOperations/`, `Code-Blocks/`, `Music-files/`: Special directories to organize educational resources and media files.

![cyberlab-dashboard](https://github.com/user-attachments/assets/0c5bede4-7544-4fa2-922c-63d60871b664)
