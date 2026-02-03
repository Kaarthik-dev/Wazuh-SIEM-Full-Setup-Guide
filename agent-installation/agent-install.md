## Installing Wazuh Agent on Linux

### Prerequisites
- Linux system (Ubuntu)
- Network connectivity to the Wazuh manager
- Root or sudo privileges

### Step 1 – Add Wazuh repository
```bash
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo apt-key add -
echo "deb https://packages.wazuh.com/4.x/apt stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list
```
---
### Step 2 – Install the agent
```bash
sudo apt update
sudo apt install wazuh-agent -y
```
---
### Step 3 – Verify installation
```bashsudo systemctl status wazuh-agent```
