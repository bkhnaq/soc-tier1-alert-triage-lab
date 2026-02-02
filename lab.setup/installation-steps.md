---

# 🛠️ Installation Guide: Wazuh All-in-One Lab

This guide provides reproducible steps to set up a **Wazuh All-in-One** environment on Ubuntu 22.04 LTS and connect a Windows 10 endpoint.

**Tested Version:** Wazuh `4.14.2` (February 2026).

---

## 📋 Prerequisites

* **Wazuh Server:** Ubuntu Server 22.04 LTS VM.
* **Endpoint:** Windows 10 VM (Pro recommended).
* **Connectivity:** Both VMs must be on the same network (Host-only or NAT) and capable of pinging each other.
* **Privileges:** Root/sudo access on Ubuntu; Administrator access on Windows.

---

## 🚀 Step 1: Install Wazuh All-in-One (Server)

1. **Update System Packages:**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install curl lsb-release gnupg -y

```


2. **Run the Assisted Installation Script:**
Download and execute the script in **all-in-one** mode. This process takes approximately 10–15 minutes.
```bash
curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
sudo bash ./wazuh-install.sh -a

```


3. **Important Outputs:**
* **Admin Password:** The script will display a generated password for the `admin` user. **Save this immediately.**
* **Credential Backup:** A file named `wazuh-install-files.tar` is created. To retrieve passwords later, use:
```bash
sudo tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt

```




4. **Verify Services:**
Ensure all components are active and running:
```bash
sudo systemctl status wazuh-manager
sudo systemctl status wazuh-indexer
sudo systemctl status filebeat
sudo systemctl status wazuh-dashboard

```



---

## 🌐 Step 2: Access Wazuh Dashboard

1. **URL:** Open a browser and go to `https://<wazuh-server-ip>` (e.g., `https://192.168.56.10`).
2. **SSL Warning:** Accept the self-signed certificate warning to proceed.
3. **Login:**
* **Username:** `admin`
* **Password:** (The one generated in Step 1).



---

## 💻 Step 3: Install Wazuh Agent (Windows 10)

1. **Download Installer:**
Fetch the matching agent version: [Wazuh Agent 4.14.2 MSI](https://packages.wazuh.com/4.14/windows/wazuh-agent-4.14.2-1.msi).
2. **Deployment (Choose one method):**
* **GUI:** Run the MSI, enter the **Manager IP** (e.g., `192.168.56.10`), and leave the registration password blank.
* **CLI (Recommended):** Open PowerShell as Administrator and run:
```powershell
msiexec.exe /i wazuh-agent-4.14.2-1.msi /q WAZUH_MANAGER="192.168.56.10" WAZUH_AGENT_NAME="win10-endpoint"

```




3. **Start Service:**
Open `services.msc`, locate **Wazuh**, and ensure the status is **Running**.

---

## ✅ Step 4: Verify Connection

1. **Dashboard Check:** Navigate to **Agents** -> **Summary**.
2. **Status:** The agent `win10-endpoint` should appear with an **Active** (green) status.
3. **Troubleshooting (If not active):**
* **Check Windows Logs:** `C:\Program Files (x86)\ossec-agent\ossec.log`
* **Check Server Logs:** `sudo tail -f /var/ossec/logs/ossec.log`
* **Firewall:** Ensure ports `1514/UDP` and `1515/TCP` are open on the Ubuntu server.



---

> [!NOTE]
> Your lab is now ready for security monitoring. You can proceed to generate alerts such as brute-force simulations or suspicious PowerShell executions.

---
