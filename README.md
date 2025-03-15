# Automated Security Operations Center (SOC)

# 1. Introduction

# 1.1 Overview

The SOC Automation Project is designed to create an automated Security Operations Center (SOC) workflow that enhances event monitoring, alerting, and incident response. By leveraging open-source tools such as Wazuh, Shuffle, and TheHive, this project optimizes SOC operations by automating repetitive tasks, reducing the workload on security analysts, and improving the overall efficiency of security monitoring.

# 1.2 Purpose and Goals

- Automate Event Collection and Analysis – Ensures security events are collected, logged, and analyzed in real-time, reducing manual intervention.

- Streamline the Alerting Process – Automates the process of generating, forwarding, and triaging alerts to minimize response times.

- Enhance Incident Response Capabilities – Introduces automated response actions for security incidents, ensuring a swift and structured response.

- Improve SOC Efficiency – Reduces analyst workload by automating log analysis, threat correlation, and case management.

# 1.3 SOC Automation Diagram
![image](https://github.com/user-attachments/assets/5069b97c-b5a0-446f-abcb-299211eec822)

# 2. Prerequisites

# 2.1 Hardware Requirements

To successfully set up the SOC Automation Lab, ensure your system meets the following hardware requirements:

- A host machine capable of running multiple virtual machines.

- Minimum 16GB RAM and 4 vCPUs (recommended 32GB RAM for smoother performance).

- 500GB+ disk space to store log files and system images.

# 2.2 Software Requirements

- VMware Workstation/Fusion or VirtualBox – Used for virtualization.

- Windows 10 ISO – Acts as the client machine for security event generation.

- Ubuntu 22.04 ISO – Serves as the operating system for Wazuh and TheHive.

- Sysmon – Provides detailed Windows event logging for threat detection.

# 2.3 Tools and Platforms

- Wazuh – A powerful open-source SIEM and XDR platform for log collection and analysis.

- Shuffle – A SOAR tool that automates security workflows, reducing manual intervention.

- TheHive – A Security Incident Response Platform (SIRP) for managing investigations and response actions.

- VirusTotal – A cloud-based malware scanning and intelligence platform for file and URL analysis.

# 2.4 Prior Knowledge

Familiarity with Virtual Machines (VMs) and virtualization platforms.

- Basic Linux command-line experience (file manipulation, installing packages, and editing config files).

- Understanding of SOC operations, log analysis, and threat detection.

# 3. Setup

# 3.1 Install and Configure Windows 10 with Sysmon

# 3.1.1 Install Windows 10 on VMware/VirtualBox

1. Download and install VMware Workstation/VirtualBox.

2. Create a new virtual machine and allocate 4GB RAM, 2 vCPUs, and 50GB storage.

3. Attach the Windows 10 ISO and complete the installation.

# 3.1.2 Install Sysmon for Advanced Logging

1. Download Sysmon from the Sysinternals website.

2. Obtain a Sysmon configuration file (from GitHub or DFIR resources).

3. Extract the Sysmon archive and navigate to the extracted folder in PowerShell.

4. Install Sysmon using:

       .\Sysmon64.exe -i .\sysmonconfig.xml
   ![image](https://github.com/user-attachments/assets/c76a414e-2c4c-4f83-bf52-7de8bdcab229)


6. Verify Sysmon installation:

 - Open Services.msc and check for Sysmon64.

 - Open Event Viewer > Applications and Services Logs > Microsoft > Windows > Sysmon.
   ![image](https://github.com/user-attachments/assets/861c32a5-a6a2-4b97-9d58-ebbc07c7a094)


# 3.2 Set Up Wazuh Server

# 3.2.1 Deploy Wazuh on a Cloud Server (DigitalOcean)

1. Create a DigitalOcean Droplet with Ubuntu 22.04.
   ![image](https://github.com/user-attachments/assets/f008dd23-0a0a-44ff-a669-117a1324e308)


3. Set a strong root password and name the droplet Wazuh.

4. Configure a firewall:

 - Navigate to Networking > Firewalls.

 - Restrict inbound traffic and allow only trusted IPs.
![image](https://github.com/user-attachments/assets/ef505ffe-38b6-4f08-a799-b84a75341465)


4. Connect to the server via SSH:

       ssh root@[WAZUH-SERVER-IP]

5. Update and upgrade packages:

       sudo apt-get update && sudo apt-get upgrade -y
   ![image](https://github.com/user-attachments/assets/54bad6e0-e1c7-4877-9493-9020963d9424)


7. Install Wazuh:

       curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh && sudo bash ./wazuh-install.sh -a

 8. Access the Wazuh Web Interface at:

        https://[WAZUH-SERVER-IP]/
    ![image](https://github.com/user-attachments/assets/95145f3c-b555-4a53-a3aa-ed43ab50cbcb)


# 3.2.2 Deploy Wazuh Locally (On-Premises)

- Install Ubuntu 22.04.

- Allocate 8GB RAM, 4 vCPUs, and 50GB Storage.

- Follow the Wazuh Quickstart Guide for installation.
  ![image](https://github.com/user-attachments/assets/d2516b19-6223-4b8b-9260-96c1c9f69ca8)


# 3.3 Install TheHive

# 3.3.1 Deploy TheHive on a Cloud Server (DigitalOcean)

1. Create a DigitalOcean Droplet for TheHive (Ubuntu 22.04).
![image](https://github.com/user-attachments/assets/3ccaaf22-1c90-4ccc-b267-b807c96c1882)


3. Install dependencies:

       sudo apt install wget gnupg apt-transport-https git ca-certificates curl -y

4. Install Java, Cassandra, and Elasticsearch.

5. Install TheHive:

       sudo apt-get install -y thehive

6. Access TheHive Web Interface at:

       http://[THEHIVE-SERVER-IP]:9000

# 4. Automation with Shuffle

# 4.1 Integrate Wazuh with Shuffle

1. Create a Webhook in Shuffle and copy the URL.
   ![image](https://github.com/user-attachments/assets/ef8551d2-b553-450e-875f-c08bd99d9c47)


3. Modify Wazuh Configuration:

       <integration>
         <name>shuffle</name>
         <hook_url>https://shuffler.io/api/v1/hooks/webhook</hook_url>
         <level>3</level>
         <alert_format>json</alert_format>
       </integration>

4. Restart Wazuh:

       systemctl restart wazuh-manager.service
   ![image](https://github.com/user-attachments/assets/13db983c-b1c8-4688-905a-aa8da3887da5)


# 4.2 Automate Incident Handling with TheHive

1. Extract SHA256 hash from alerts.

2. Query VirusTotal for threat intelligence.

3. Forward alerts to TheHive for investigation.
   ![image](https://github.com/user-attachments/assets/e4c53492-54b7-4b2f-a0b9-bc2aed42c55d)

   ![image](https://github.com/user-attachments/assets/519a41ec-06ed-4603-a711-94cdc81612f2)

5. Send Email Notifications to SOC Analysts.

![image](https://github.com/user-attachments/assets/4a88baa8-a1e6-4fb7-9d32-e283ab31d6b1)

![image](https://github.com/user-attachments/assets/64b44344-3395-4033-bd3e-27d0300b3ab4)

# 5. Conclusion

This project successfully integrates Wazuh, TheHive, and Shuffle to create an automated SOC environment. The implementation ensures:

- Real-time event monitoring and automated alerting.

- Seamless integration between security tools for automation.

- Incident response workflows using SOAR capabilities.

Future improvements can include advanced correlation rules, integrating additional threat intelligence sources, and refining automation workflows.

7. References
   https://www.mydfir.com/








 




