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

Next, I create a firewall to keep external scanners out from the environment. For the inbound rules type, I select All TCP and set the source to my IP address. I apply the same to the outbound rules for UDP. Afterwards, the VM is ready to be added to the firewall. This is critical because SSH is open to the public. 

<img width="2560" alt="2 5" src="https://github.com/user-attachments/assets/82897600-804b-4d76-9ac9-827db27088d0" />

The Windows VM is configured with the firewall.

<img width="2560" alt="2 6" src="https://github.com/user-attachments/assets/e24465f7-246d-41d7-9286-e699277e5c1e" />

Next, I perform some updates by typing apt-get update && apt-get upgrade.

<img width="2560" alt="2 7" src="https://github.com/user-attachments/assets/1ed3722f-6960-4f32-a9f5-03963a238b2a" />

Afterwards, I install Wazuh by running the command sudo -i curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh && sudo bash ./wazuh-install.sh -a

<img width="2560" alt="2 8" src="https://github.com/user-attachments/assets/ca5e4cb5-a2af-4908-8869-81a72fb54095" />

Next, I take note of the public IP address of Wazuh in Digital Ocean

<img width="2560" alt="2 9" src="https://github.com/user-attachments/assets/239b3cf8-7c3c-4d5d-8d51-4f943fea0ec9" />

I take the IP address that was copied from Digital Ocean and open a new browser tab. I type https://<IP address> and then go to the site. I enter the login credentials from the Wazuh setup a few steps above.

<img width="2560" alt="2 10" src="https://github.com/user-attachments/assets/04cb0c61-333a-48e7-a9a0-e2f8def1cab3" />
<img width="2560" alt="2 11" src="https://github.com/user-attachments/assets/5991da9c-27be-48fc-ab8e-b47352280bd2" />
<img width="2560" alt="2 12" src="https://github.com/user-attachments/assets/959c3798-65e7-4806-8b09-3d26d5d04c3b" />

The next step is to install The Hive. This is a similar setup as done for Wazuh. I go back to Digital Ocean and create a new Droplet. I select the region closest to me, a Linux Ubuntu 22.04 x64 server with 8GB RAM, 2 CPUs, and 160GB SSD storage space.
