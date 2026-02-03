## Enrolling Wazuh Agent with Manager

### Objective
Register the agent with the Wazuh manager so it can
send security events.

### Step 1 – Configure manager address
Edit the agent configuration file and specify the
Wazuh manager IP address.

```bash
sudo nano /var/ossec/etc/ossec.conf
```
### Step 2 – Enroll the agent
```bash 
sudo /var/ossec/bin/agent-auth -m <manager-ip> -A <agent-name>
```
---
### Step 3 – Start the agent service
```bash
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```
### Step 4 – Verify agent status
```bash
sudo /var/ossec/bin/agent_control -lc
```
Once enrolled successfully, the agent will appear
as active in the Wazuh dashboard.
