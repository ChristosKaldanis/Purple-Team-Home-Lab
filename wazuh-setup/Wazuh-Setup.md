```bash
WAZUH COMPLETE SETUP GUIDE


SECTION Α — Reset Wazuh SERVER (Ubuntu VM 192.168.106.130)
Step 1 — Uninstall
# Stop all the Services
sudo systemctl stop wazuh-manager
sudo systemctl stop wazuh-indexer
sudo systemctl stop wazuh-dashboard

# Uninstall Packages
sudo apt-get remove --purge wazuh-manager wazuh-indexer wazuh-dashboard -y
sudo apt-get autoremove -y

# Delete all the Files 
sudo rm -rf /var/ossec
sudo rm -rf /etc/wazuh-*
sudo rm -rf /usr/share/wazuh-*
sudo rm -rf /var/lib/wazuh-*
sudo rm -rf /var/log/wazuh-*
sudo rm -rf /tmp/wazuh-*

# Delete install Files
rm -f ~/wazuh-install.sh
rm -f ~/wazuh-install-files.tar

Step 2 — Clean repo
bashsudo rm -f /etc/apt/sources.list.d/wazuh.list
sudo apt-get update

Step 3 — Clean Installation
# Download Fresh Install Script
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh

# Install (with -i για Ubuntu 24.04)
sudo bash wazuh-install.sh -a -i
Please wait 10-15 minutes. The output should be:

INFO: --- Summary ---
INFO: You can access the web interface https://YOUR_IP
User: admin
Password: XXXXXXXXXX  ← TAKE A NOTE

Step 4 — Confirmation
sudo systemctl status wazuh-manager
sudo systemctl status wazuh-indexer
sudo systemctl status wazuh-dashboard
Και στο browser: https://192.168.xxx.xxx

Section Β — Reset Wazuh AGENT (Ubuntu Agent 192.168.xxx.xxx)
Step 1 — Uninstall
sudo systemctl stop wazuh-agent
sudo apt-get remove --purge wazuh-agent -y
sudo rm -rf /var/ossec
sudo rm -rf /etc/wazuh-*

Step 2 — Clean Installation
# Download the Agent
curl -sO https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.7.0-1_amd64.deb

# Install with the IP of the Server
sudo WAZUH_MANAGER='192.168.xxx.xxx' dpkg -i wazuh-agent_4.7.0-1_amd64.deb

# Start
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent


Section C — Confirm that Everything Works Fine
1. Manager Runs
sudo systemctl status wazuh-manager | grep Active

# 2. Agents Connected
sudo /var/ossec/bin/agent_control -l

# 3. Alerts Arriving
sudo tail -f /var/ossec/logs/alerts/alerts.log

# 4. Custom Rules (if necessary)
sudo grep "100001\|100002\|100003" /var/ossec/logs/ossec.log | tail -5

# 5. Test Rule with Logtest
sudo /var/ossec/bin/wazuh-logtest
# Type: Dec 25 10:00:00 ubuntu sshd[1]: Failed password for root
# Expected Output: Rule: xxxx

Section D — Auto-start after the Reboot
# Wazuh Server
sudo systemctl enable wazuh-manager
sudo systemctl enable wazuh-indexer
sudo systemctl enable wazuh-dashboard

# Ubuntu Agent
sudo systemctl enable wazuh-agent

```
