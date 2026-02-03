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
