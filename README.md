# Automated Security Operations Center (SOC)

# Overview

The primary objective of this lab is to create an automated Security Operations Center (SOC) environment that closely mirrors real-world incident detection, analysis, and response scenarios. Using open-source software, this lab can be deployed at no cost, either fully on-premises or partially in the cloud via a trial Digital Ocean account.

This lab serves as a practical learning environment for security professionals, students, and researchers interested in cybersecurity operations, providing hands-on experience with security monitoring, incident response, and automation workflows.

# Key Components

This lab incorporates several free and open-source tools to replicate a real-world SOC:

Wazuh – A comprehensive SIEM and XDR solution used for event collection, log analysis, and threat detection.

Shuffle – A Security Orchestration, Automation, and Response (SOAR) platform that enhances operational efficiency by automating incident response workflows.

TheHive – A case management platform designed for efficient documentation, collaboration, and structured response to security incidents.

By leveraging automation and integrating these tools, this lab aims to accelerate threat detection, optimize SOC workflows, and provide a deeper understanding of security operations in an enterprise environment.

# Architecture Diagram


![soc-automation-diagram](https://github.com/user-attachments/assets/641accf0-b792-4111-9c8e-fcb63530b276)

                          Data Flow through the SOC environment

 # Prerequisites

Before proceeding with the setup, ensure that you have the following prerequisites in place:

 System Requirements

Hypervisor: Oracle VirtualBox (recommended) for creating virtual machines.

Operating System Images:

Windows 10 ISO: Required for setting up the Client PC.

Ubuntu 22.04.3 LTS ISO: Needed for on-premises installation.

Cloud Deployment Alternative: A Digital Ocean account with access to their $200 free trial for cloud-based deployment.

# Understanding the Components

  Wazuh Agent
  The Wazuh agent, installed on the Windows 10 Client endpoint, continuously monitors system       activities, collects security events, and securely transmits this data to the Wazuh Manager.     It plays a crucial role in endpoint security by detecting anomalies, unauthorized access, and    suspicious behaviors in real-time.

  Wazuh Manager
  Deployed either in the cloud or on-premises, the Wazuh Manager serves as the centralized hub     for receiving, processing, and analyzing security events. It applies predefined rules, machine   learning algorithms, and threat intelligence feeds to identify security threats. Upon            detection, it generates alerts and initiates predefined mitigation strategies to contain         threats promptly.

  Shuffle (SOAR Platform)
  
Shuffle plays a critical role in automating SOC workflows and improving response efficiency.     It performs the following key functions:

Threat Intelligence Enrichment – Leverages OSINT (Open-Source Intelligence) to enhance detected Indicators of Compromise (IOCs).

Automated Case Management – Integrates with TheHive to create structured security incident cases for efficient investigation and response.

Alerting & Notifications – Automates email notifications and escalation workflows to ensure rapid analyst response.

# The Hive
A cloud-based incident response and case management platform, TheHive provides SOC teams with a structured environment to analyze threats, coordinate response efforts, and document investigations. It enhances collaboration among analysts and ensures consistency in handling security incidents.
  




 




