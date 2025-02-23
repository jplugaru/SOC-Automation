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

<img width="2560" alt="2 13" src="https://github.com/user-attachments/assets/8141e5f0-7794-432a-874c-6fa1328960dc" />

After The Hive is created, I add it to the firewall that was created earlier.

<img width="1473" alt="2 14" src="https://github.com/user-attachments/assets/0056f6bf-faa8-4d51-a66e-8d105cbccac6" />

The next step is to install Java, Cassandra, ElasticSearch, and TheHive. All of these programs are installed via Terminal on my local machine by connecting to the Linux Ubuntu server via SSH.

<img width="1018" alt="2 15" src="https://github.com/user-attachments/assets/b2fe6962-3319-4169-a0ce-60b8c5913f28" />

Afterwards, the next step is to configure The Hive. I type nano /etc/cassandra/cassandra.yaml to customoze the cluster name. I changed it to Jonathan Lab

<img width="1018" alt="2 16" src="https://github.com/user-attachments/assets/4960b581-e33a-45d5-be5d-ff4c38d7b6a5" />

Next, I change the IP address of the listen_address to match that of The Hive's address. The same IP address is applied to the rpc_address. Lastly, the seeds IP address is also changed to match The Hive's address.

<img width="1018" alt="2 17" src="https://github.com/user-attachments/assets/7571a457-6358-45b6-be47-ebabe416968c" />
<img width="1018" alt="2 18" src="https://github.com/user-attachments/assets/1c6b7863-d2ff-4457-8a96-2215d473fa52" />

Next, the Cassandra service must be stopped and redundant files are cleaned out using rm -rf /var/lib/cassandra/*. Afterwards, Cassandra is restarted by typing systemctl start cassandra.service.

<img width="1018" alt="2 19" src="https://github.com/user-attachments/assets/f88a9582-1da0-44e6-adfd-2c73e0d05c48" />
<img width="1018" alt="2 20" src="https://github.com/user-attachments/assets/e85beb3f-64f6-49af-863d-a43e021c2117" />

Next, elastic search needs to be set up which allows us to query data. The cluster.name, node.attr.rack, network.host, and cluster.initial_master_nodes all need to be changed to reflect The Hive.

<img width="1018" alt="2 21" src="https://github.com/user-attachments/assets/ffcb5a10-0532-41e2-a29d-91a046a06bf6" />
<img width="1018" alt="2 22" src="https://github.com/user-attachments/assets/d828a8bf-c784-495b-99e4-597ec2ad06b4" />

Next, I want to double check to see if The Hive user end group has access to to a specific file path. I type ls -la /opt/thp and have the results shown on the screen which show me that the root account has access to the directory. This will need to be changed. I type chown -R thehive:thehive /opt/thp in order to change the permissions.

<img width="1018" alt="2 23" src="https://github.com/user-attachments/assets/bb5dc7dd-b98c-4191-beab-b59f7bf21f77" />
<img width="1018" alt="2 24" src="https://github.com/user-attachments/assets/53f2fae8-1b5d-47f8-9c13-e76508b3209e" />

Afterwards, I go into the The Hive's configuration file and configure it. I type nano /etc/thehive/application.conf to go into the configuration file. Here, I change the hostname for the database to the IP address for The Hive that I created. The cluster name is also changed to TheHive since that is what was changed for Cassandra. Below that, the host name is changed again to match that of my Hive instance. Further down, the storage path is changed to http://64.225.62.147:9000 which is the public IP of my Hive instance. 

<img width="1018" alt="2 25" src="https://github.com/user-attachments/assets/fde1f808-1e99-40aa-b48f-0d8e3a12b129" />

Afterwards, I save the configuration file and start thehive service, enable thehive service, and then check on its status by typing status thehive. This confirms that all three services (Cassandra, elasticservice, and TheHive) are running otherwise The Hive will not start.

<img width="2560" alt="2 26" src="https://github.com/user-attachments/assets/c05ffd2b-c5e3-4700-97e2-0013073f1f81" />

Afterwards, I copy the IP address of The Hive instance and put it in a web browser to verify that it is accessable.

<img width="2560" alt="2 27" src="https://github.com/user-attachments/assets/15ad687f-4b1a-41e8-8f00-0e29a939ce39" />
<img width="2560" alt="2 28" src="https://github.com/user-attachments/assets/68378901-8ad9-47ba-8de5-f1acb8019ae9" />

The next step is to log into Wazuh and add an agent. I select Windows as the machine, the IP address of my Wazuh instance for the server address, and an agent name of Jonathan.

<img width="1500" alt="2 29" src="https://github.com/user-attachments/assets/83a608c5-05c6-4fcb-bbde-bd8f959da001" />

Afterwards, the command on the Wazuh agent setup page is copied and executed in a Windows PowerShell terminal to install Wazuh. Afterwards, I run the command net start wazuhsvc to start Wazuh.

<img width="2560" alt="2 30" src="https://github.com/user-attachments/assets/f5e9a9cd-2f8a-4642-bc5b-b77c9bace410" />
<img width="2560" alt="2 31" src="https://github.com/user-attachments/assets/f32df94f-029e-4115-afee-1b7ad1f777da" />

On the Wazuh dashboard page, I see the agent on the screen as active and can click on it to start querying for events. This will allow telemetry to be captured.

<img width="2560" alt="2 32" src="https://github.com/user-attachments/assets/a91ffde7-4836-4c8c-a215-e82dc6a494fc" />
<img width="2560" alt="2 33" src="https://github.com/user-attachments/assets/1337c0da-556e-4948-b193-73b3c6f1ef97" />
<img width="1500" alt="2 34" src="https://github.com/user-attachments/assets/44124f2d-5d96-4654-ae67-922b5d992d55" />

Next, I go into the configuration file for Wazuh which is located at C:\Program Files (x86)\ossec. Afterwards, I need to edit the file so it can ingest Sysmon logs. The Sysmon channel name is obtained by opening Windows Event Viewer and navigating to Applications and Service Logs>Microsoft>Windows>Sysmon>Operational. I right click on the file and selected Properties to copy the name. After that is done, I restart the Wazuh service.

<img width="1500" alt="2 35" src="https://github.com/user-attachments/assets/ea90264e-789b-4872-9035-a82e97591e70" />
<img width="1500" alt="2 36" src="https://github.com/user-attachments/assets/e53cc893-9737-4439-a535-b853dde780f8" />

Next, Mimikatz is installed onto the Windows machine. Windows Defender will need to be disabled to install the program, which is used by red teamers and attackers to extract credentials from the machine. To install Mimikatz, an exclusion is made in Windows Defender to the Downloads folder so that the Mimikatz installer is not automatically deleted. Once the file is downloaded, I launch a PowerShell terminal and change the directory to navigate to the folder where I downloaded Mimikatz. After that, I run the command to install Mimikatz.

<img width="2560" alt="2 37" src="https://github.com/user-attachments/assets/f1ad2989-cf3d-4612-9c45-03cf97e27023" />
<img width="1018" alt="2 38" src="https://github.com/user-attachments/assets/1caa5881-3df9-4817-9bbb-ee8f034fa7bd" />

The next thing I did is go to the Wazuh dashboard to see if any events related to Mimikatz were generated. In this case, nothing was generated and this could be because the Sysmon events did not trigger anything, or rules from Wazuh, since by default Wazuh does not log events from Mimikatz. This could be changed by going into the Wazuh manager and configuring the ossec.conf file so that it can log everything. Before making any changes, I copied the ossec.conf file as a backup in case I need to revert back to it.

<img width="1018" alt="2 39" src="https://github.com/user-attachments/assets/c9eb9201-a12c-477d-8f68-60369c905292" />
<img width="1018" alt="2 40" src="https://github.com/user-attachments/assets/5f1d4e39-d9d8-46c4-b399-055f612987b4" />

In the configuration, I changed <logall> to yes as well as <logall_json>. Afterwards, I restart the Wazuh manager because I want to force Wazuh to begin archiving all the logs and put them into a file called Archives, located at /var/ossec/logs/archive. 

<img width="1018" alt="2 41" src="https://github.com/user-attachments/assets/c6ed2b63-a148-482d-b1ab-9c131865db26" />

For Wazuh to ingest the logs, I need to change the config and filebeat. This is done by typing nano etc/filebeat/filebeat.yml. In the configuration, I change archives enabled from false to true. Afterwards, I save the config file and restart the filebeat service.

<img width="2560" alt="2 42" src="https://github.com/user-attachments/assets/741748d6-6c64-4d29-8db9-4cafa99a8691" />
<img width="2560" alt="2 43" src="https://github.com/user-attachments/assets/14716bcf-034e-497a-b869-c424d4e6263c" />

Next, back on the Wazuh dashboard, I create a new index. The index is created for all of the archives in order to search the logs.

<img width="1018" alt="2 45" src="https://github.com/user-attachments/assets/af695999-d7f4-47f8-b35f-649473a8f5a2" />
<img width="2560" alt="2 46" src="https://github.com/user-attachments/assets/e4919564-57fd-4c9a-8103-d42ce0ac3bee" />

In the Wazuh Manager CLI, I type cat archives.json | grep -i to see if Mimikatz events have populated. In the Wazuh dashboard, I see the alerts generating as well.

<img width="2560" alt="2 47" src="https://github.com/user-attachments/assets/7ea24c07-dc3c-43c7-a143-2a89cf0ab36e" />
<img width="2560" alt="2 48" src="https://github.com/user-attachments/assets/282c030f-dca1-4104-b060-83b09ec0720c" />

The next step is to create an alert. Wazuh has built in rules that can be used as a reference. On the dashboard, I navigate to Management > Rules > Manage Rule Files. In the box, I type sysmon to look for event ID 1. On the screen, 0800-sysmon_id_1.xml. The page then loads with sysmon rules that are built into Wazuh, specifically targeting ID 1. One of the rules will be copied to be built out as a custom rule to detect Mimikatz.

<img width="2560" alt="2 49" src="https://github.com/user-attachments/assets/eb045d03-443c-412e-95a4-2b5adc93462a" />
<img width="2560" alt="2 50" src="https://github.com/user-attachments/assets/f63fd800-1e25-430f-a77b-3ceba03c571f" />
<img width="2560" alt="2 51" src="https://github.com/user-attachments/assets/62050cbe-2fe7-437d-87f7-ecdb766faa63" />

Next, I go back to the previous page and click Custom Rules. Afterwards, I click on local_rules.xml and edit it. I paste the rule code that was copied into the local rule that alreay exists. I change the rule ID, level, field name, description, and mitre ID fields. I save the changes and then restart the manager. 

<img width="1500" alt="2 52" src="https://github.com/user-attachments/assets/54af75aa-7b15-4042-8c01-daa2ecb1f739" />
<img width="2560" alt="2 53" src="https://github.com/user-attachments/assets/36e90d56-da06-45e0-b524-cca8aa0f325d" />

Back in the Windows machine, I rename the mimikatz.exe file to youareawesome so that the new alerts can be distinguishable from the old ones. Next, in PowerShell, I run the command to launch youareawesome.exe. Back in the Wazuh dashboard, I refresh the page and can see the alert generated for the action.

<img width="2560" alt="2 54" src="https://github.com/user-attachments/assets/9e8c006b-3509-4294-8eee-8cfc4a76ad44" />

The next step is to go to Shuffle.io and create an account. Shuffle will be used to create workflows. The new workflow I created is called SOC Automation Project. The use case selected is EDR to Ticket.

<img width="2560" alt="2 55" src="https://github.com/user-attachments/assets/b73ec2ee-4823-4f8f-85a4-a3b0668a172b" />

Next, on the screen, a webhook element is dropped and renamed to Wazuh-Alerts. I then select the webhook URI that will be inputted into the Wazuh Manager.

<img width="974" alt="2 56" src="https://github.com/user-attachments/assets/4385dd4c-8b34-4ad5-bbf1-9f283b0b7c33" />

Next, the ossec.conf configuration file is modified in the Wazuh Manager. Here, an integration tag is added and the hook URL is updated with that from Shuffle. 

<img width="1500" alt="2 57" src="https://github.com/user-attachments/assets/43855a35-ce23-44b2-83c8-aae9b6dca17a" />

After that is complete, I go back into the Windows machine and run the youareawesome.exe file again to generate telemetry 
