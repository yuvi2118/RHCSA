# RHCSA
RHCSA Zero To Hero
# Linux Exam Guide

## Overview
This repository contains a comprehensive guide for configuring and managing a Linux system as per the exam requirements. It includes steps for setting up a YUM repository, configuring SELinux, managing users and groups, setting up containers, configuring NTP, and more.

## Contents
- **Primary Machine Configuration**
  - YUM repository setup
  - Debugging SELinux for HTTP service
  - Configuring cron jobs
  - Managing users and groups
  - Configuring NTP
  - Finding and copying files
  - Setting default permissions
  - Writing automation scripts
  
- **Secondary Machine Configuration**
  - Resetting root password
  - Setting up performance tuning profiles
  - Creating backups
  - Enforcing password policies
  - Setting up containers and services
  
## How to Use
1. Clone the repository:
   ```sh
   git clone https://github.com/yourusername/linux-exam-setup.git
   cd linux-exam-setup
   ```
2. Follow the instructions in `linux_exam_setup.md` for step-by-step guidance.
3. Modify configurations as needed for your specific exam setup.

## Notes
- Ensure you have `root` or `sudo` privileges before running administrative commands.
- For container-based tasks, ensure `podman` or `docker` is installed.
- The repository assumes an AlmaLinux-based system but can be adapted for other distributions.

## Contributing
If you find any improvements or updates needed, feel free to open a pull request.

## License
This project is licensed under the MIT License - see the LICENSE file for details.

