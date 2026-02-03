# Wazuh SIEM Installation

This README documents the complete end-to-end installation and configuration of
Wazuh SIEM (Manager, Indexer, Dashboard) and agent setup on Ubuntu Server.
The process is written in the exact order it must be executed, with each step
explained inline.

---

## STEP 1 – System preparation

The first step is to ensure the operating system is fully updated so that the
Wazuh installer does not fail due to missing packages or outdated dependencies.

---

## STEP 2 – Downloading the Wazuh installer

In this step, we download the official Wazuh all-in-one installer script and make
it executable. This script installs the manager, indexer, and dashboard together.

---

## STEP 3 – Installing Wazuh (All-in-One)

Now we run the installer to deploy Wazuh Manager, Indexer, and Dashboard on the
same server.

If the system is running Ubuntu 24.04, the installer may show an unsupported OS
warning. This is only a version check and does not indicate a real failure.

---

## STEP 4 – Verifying services

This step confirms that all Wazuh components are running correctly after
installation.

---

## STEP 5 – Dashboard memory issue explanation and fix

After installation, the Wazuh dashboard may fail to start on low or medium RAM
virtual machines. This happens because the dashboard is built on Node.js and
exceeds default memory limits.

---

## STEP 6 – Wazuh agent installation

This step installs the Wazuh agent on a client system that will report logs and
security events to the Wazuh manager.

---

## STEP 7 – Agent configuration and enrollment

The agent must be configured to communicate with the Wazuh manager and enrolled
so it becomes a trusted endpoint.

---

## STEP 8 – Common issues and resolutions

Agent ID duplication can occur when an agent is reinstalled without removing the
previous entry on the manager.

Version mismatch occurs when the agent version is newer than the manager version.

---

## STEP 9 – Final notes

Always ensure that agent and manager versions match. Use static IP addresses for
the manager and agents. Installation credentials can be found in
`/var/log/wazuh-install.log`.

---

## Commands (execute in order)

```bash
sudo apt update && sudo apt upgrade -y

curl -L -o wazuh-install.sh https://packages.wazuh.com/4.7/wazuh-install.sh
chmod +x wazuh-install.sh

sudo ./wazuh-install.sh -a
sudo ./wazuh-install.sh -a --ignore-check

sudo systemctl status wazuh-manager
sudo systemctl status wazuh-indexer
sudo systemctl status wazuh-dashboard

sudo nano /etc/default/wazuh-dashboard
# add: NODE_OPTIONS="--max-old-space-size=2048"

sudo systemctl daemon-reload
sudo systemctl restart wazuh-dashboard

sudo apt update
sudo apt install wazuh-agent -y

sudo nano /var/ossec/etc/ossec.conf
# set manager IP:
# <client>
#   <server>
#     <address>192.168.56.50</address>
#   </server>
# </client>

sudo /var/ossec/bin/agent-auth -m 192.168.56.50 -A agent1

sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent

sudo /var/ossec/bin/agent_control -lc

sudo apt remove wazuh-agent -y
sudo apt install wazuh-agent=4.7.5-1 -y
sudo apt-mark hold wazuh-agent
