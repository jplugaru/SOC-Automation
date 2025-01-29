# SOC-Automation

## Objective

The SOC Automation Lab is aimed to leverage automation in order to provide incident response, accelerate threat detection, and streamline security operations center (SOC) workflows. I set up this lab on Microsoft Azure since my host machine is a MacBook Pro M2 Max. The lab will be conducted in the cloud with a Windows VM and a Wazuh server and a The Hive server.

The primary focus of this lab was to set up a test environment and to go through a security operations center (SOC) workflow of handling alerts and executing on them, mimicking real-world scenarios. This hands-on experience was designed to deepen my understanding of X, Y, and Z. 

### Skills Learned

- Advanced understanding of SOC concepts and practical application
- Proficiency in analyzing and interpreting network logs
- Ability to generate and recognize attack signatures and patterns
- Enhanced knowledge of network protocols and security vulnerabilities
- Development of critical thinking and problem-solving skills in cybersecurity
- Advanced understanding of setting up virtual machine hypervisor
- Installation of Microsoft Windows 11 client and Kali Linux client
- Network configuration to enable the virtual machines to communicate

### Tools Used

- Security Information and Event Management (SIEM) system for log ingestion and analysis
- Penetration testing tools (such as Metasploit) to conduct security vulnerability tests
- Telemetry generation tools to create realistic network traffic and attack scenarios
- Microsoft Azure for virtual machine hosting
- Wazuh for the SIEM and XDR
- The Hive for case management
- Shuffle for SOAR capabilities

## Steps

![SOC Automations](https://github.com/user-attachments/assets/81cd1083-7ed4-472e-974e-5b905dcc6d2d)

The above image is a diagram that shows the architecture of what the SOC Automation lab looks like. This also depicts how data flows through the system.

<img width="2560" alt="2 1" src="https://github.com/user-attachments/assets/2e5ed852-209a-48e0-a585-e6cbc0272b3f" />
<img width="2560" alt="2 2" src="https://github.com/user-attachments/assets/068e9ec4-7e35-46fe-8e71-41b08ec507bf" />
<img width="2560" alt="2 3" src="https://github.com/user-attachments/assets/09fac7cc-0229-4194-9da2-bf5547ceb448" />

Next, I set up Wazuh using Digital Ocean as the cloud provider. The screenshots above show how I configured the server for Wazuh. The server is a Linux Ubuntu 22.04 x64 server. The server also has 8GB RAM, 2 CPUs, and 160GB SSD storage space.

<img width="2560" alt="2 4" src="https://github.com/user-attachments/assets/33108190-8536-4c59-b156-188049d56807" />

Next, I create a firewall to keep external scanners out from the environment. 
