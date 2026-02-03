# Wazuh SIEM Installation

This README documents the complete end-to-end installation and configuration of
Wazuh SIEM (Manager, Indexer, Dashboard) and agent setup on Ubuntu Server.
The process is written in the exact order it must be executed.

---

## STEP 1 – System preparation

Ensure the operating system is fully updated so that the Wazuh installer does not
fail due to missing packages or outdated dependencies.

```bash
sudo apt update && sudo apt upgrade -y
```
---

## STEP 2 – Downloading the Wazuh installer

Download the official Wazuh all-in-one installer script and make it executable.

```bash
curl -L -o wazuh-install.sh https://packages.wazuh.com/4.7/wazuh-install.sh
chmod +x wazuh-install.sh
