# Wazuh SIEM Installation (All-in-One)

This README documents the complete end-to-end installation and configuration of
Wazuh SIEM (Manager, Indexer, Dashboard) and agent setup on Ubuntu Server.
The process is written in the exact order it must be executed, with each step
explained inline while keeping everything in a single continuous document.

---

STEP 1 – System preparation  
The first step is to ensure the operating system is fully updated so that the
Wazuh installer does not fail due to missing packages or outdated dependencies.

sudo apt update && sudo apt upgrade -y

---

STEP 2 – Downloading the Wazuh installer  
In this step, we download the official Wazuh all-in-one installer script and make
it executable. This script installs the manager, indexer, and dashboard together.

curl -L -o wazuh-install.sh https://packages.wazuh.com/4.7/wazuh-install.sh
chmod +x wazuh-install.sh

---

STEP 3 – Installing Wazuh (All-in-One)  
Now we run the installer to deploy Wazuh Manager, Indexer, and Dashboard on the
same server.

sudo ./wazuh-install.sh -a

If the system is running Ubuntu 24.04, the installer may show an unsupported OS
warning. This is only a version check and does not indicate a real failure.
In that case, continue the installation using the command below.

sudo ./wazuh-install.sh -a --ignore-check

After this step, Wazuh Manager, Indexer, and Dashboard should be installed.

---

STEP 4 – Verifying services  
This step confirms that all Wazuh components are running correctly after
installation.

sudo systemctl status wazuh-manager
sudo systemctl status wazuh-indexer
sudo systemctl status wazuh-dashboard

---

STEP 5 – Dashboard memory issue explanation and fix  
After installation, the Wazuh dashboard may fail to start on low or medium RAM
virtual machines. This happens because the dashboard is built on Node.js and
exceeds default memory limits.

To fix this, edit the dashboard environment configuration file.

sudo nano /etc/default/wazuh-dashboard

Add the following line to increase Node.js memory allocation.

NODE_OPTIONS="--max-old-space-size=2048"

Apply the changes by reloading systemd and restarting the dashboard service.

sudo systemctl daemon-reload
sudo systemctl restart wazuh-dashboard

After this fix, the dashboard should start successfully and remain stable.

---

STEP 6 – Wazuh agent installation  
This step installs the Wazuh agent on a client system that will report logs and
security events to the Wazuh manager.

sudo apt update
sudo apt install wazuh-agent -y

---

STEP 7 – Agent configuration and enrollment  
The agent must be configured to communicate with the Wazuh manager. Edit the
agent configuration file and set the manager IP address.

sudo nano /var/ossec/etc/ossec.conf

Configure the manager address as shown below.

<client>
  <server>
    <address>192.168.56.50</address>
  </server>
</client>

Enroll the agent with the manager so it becomes a trusted endpoint.

sudo /var/ossec/bin/agent-auth -m 192.168.56.50 -A agent1

Enable and start the agent service.

sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent

Verify that the agent is successfully connected to the manager.

sudo /var/ossec/bin/agent_control -lc

---

STEP 8 – Common issues and resolutions  
Agent ID duplication can occur when an agent is reinstalled without removing the
previous entry on the manager. In this case, remove the old agent from the manager
and re-enroll it.

Version mismatch occurs when the agent version is newer than the manager version.
Resolve this by reinstalling the agent with the correct version and locking it.

sudo apt remove wazuh-agent -y
sudo apt install wazuh-agent=4.7.5-1 -y
sudo apt-mark hold wazuh-agent

---

STEP 9 – Final notes  
Always ensure that agent and manager versions match. Use static IP addresses for
the manager and agents. Installation credentials can be found in
/var/log/wazuh-install.log. Useful logs include /var/ossec/logs/ossec.log and
/var/log/wazuh-dashboard/.

Wazuh SIEM installation and configuration is now complete.
