
# Setting-Up and Analysis of Cloud-based Honey Pot

## Why a Honey Pot?

A cybersecurity researcher might set up a honeypot for several key reasons, which all contribute to improving security measures, gaining insights into threat actors, and enhancing overall cybersecurity knowledge. Here’s a detailed look at why a cybersecurity researcher would deploy a honeypot:

### 1. **Threat Intelligence Gathering**

- **Understanding Attack Patterns**: Honeypots can capture detailed information about attack methods, tools, and tactics used by threat actors. This data helps researchers understand how attacks are executed and evolve over time.
- **Identifying New Threats**: By attracting and logging malicious activity, honeypots can identify new or emerging threats that might not yet be widely known or documented.

### 2. **Malware Collection and Analysis**

- **Capturing Malware Samples**: Honeypots can collect various types of malware, including viruses, worms, ransomware, and other malicious software. Researchers can analyze these samples to understand their behavior, propagation methods, and potential impacts.
- **Reverse Engineering**: Analyzing the malware's code can provide insights into its functionality and objectives, helping develop detection and mitigation strategies.

### 3. **Understanding Attacker Behavior**

- **Behavioral Analysis**: By observing how attackers interact with the honeypot, researchers can gain insights into their motives, techniques, and decision-making processes.
- **Credential Use**: Logging attempts to use stolen or guessed credentials can provide information on common password patterns and the effectiveness of different authentication mechanisms.

### 4. **Improving Defensive Measures**

- **Enhancing Detection Systems**: Data collected from honeypots can be used to improve intrusion detection and prevention systems (IDS/IPS) by creating more accurate and comprehensive signatures.
- **Developing Countermeasures**: Insights gained from honeypot activity can inform the development of security policies, patches, and other countermeasures to protect real systems.

### 5. **Training and Education**

- **Real-World Scenarios**: Honeypots provide a controlled environment for security professionals and students to observe and analyze real-world attacks without risking actual systems.
- **Hands-On Experience**: Working with honeypots allows researchers and security teams to gain hands-on experience in detecting, analyzing, and responding to cyber threats.

### 6. **Forensic Analysis**

- **Incident Response**: Honeypots can be used to study the aftermath of an attack, providing valuable forensic data that can be used to reconstruct the attack timeline and understand the attacker’s methods.
- **Legal Evidence**: In some cases, data from honeypots can be used as evidence in legal proceedings against cybercriminals.

### 7. **Vulnerability Research**

- **Identifying Weaknesses**: Honeypots can be configured to mimic specific systems or applications to identify and analyze vulnerabilities that attackers are exploiting.
- **Zero-Day Exploits**: By attracting advanced attackers, honeypots can sometimes capture zero-day exploits that are not yet known to the public or vendors.

### 8. **Enhancing Threat Sharing**

- **Collaborative Defense**: Data and insights from honeypots can be shared with the broader cybersecurity community, enhancing collective defense efforts against common threats.
- **Threat Feeds**: Honeypot data can be integrated into threat intelligence feeds, providing up-to-date information on malicious IP addresses, domains, and attack patterns.

### Bottom Line

Honeypots are valuable tools for cybersecurity threat researchers, providing rich, real-world data on cyber threats and attacker behaviors. By deploying honeypots, researchers can enhance their understanding of the threat landscape, improve defensive measures, and contribute to the broader cybersecurity community.

For this project is decided to use Linode as the cloud service provider to setup a server to host the Honey-pot on. 

### Step 1: Create a Linode Account

1. Go to the [Linode website](https://www.linode.com/) and sign up for an account. Find a free offer on-line. Below is a link to a current offer from Network Chuck’s YouTube channel.
https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbThUdHJxVV9NaUozVjd1NTRWNXU1X1FodzlVQXxBQ3Jtc0trc1JheXdCd3ZBeE9sZi1nUVE0Rkc4UUt5b1NKMzZ2Y1ZzbnBiMHd4YWJhM3FUenRZZ21lNVpfS1hobmFtNTUxQTZvYjQyMktqVXc1WlhyUDExWGY3QWM1ZDFtdGE5RV9RR1lRSEVyYWhNc3VCZlF3OA&q=https://ntck.co/linode&v=nTqu6w2wc68

2. Complete the registration process and log in to your Linode account.

### Step 2: Create a New Linode

Linode calls its VMs “Linodes”

1. Once logged in, navigate to the Linode dashboard.
2. Click on the "Create" button and select "Linode" from the dropdown menu.

### Step 3: Configure Your Linode

1. **Choose a Distribution**: Select "Ubuntu" as your operating system. You can choose the latest LTS version available.
2. **Region**: Select the data center region closest to you or your target audience for better latency.
3. **Linode Plan**: Choose a plan that fits your needs. The Shared CPU plans are usually sufficient for most use cases. T-Pot documentation recommends at least 8-16 GB RAM, 128 GB free disk space.
4. **Linode Label**: Enter a label to identify your Linode.
5. **Root Password**: Set a strong root password for your server.

### Step 4: Deploy Your Linode

1. Review your configuration and click the "Create Linode" button.
2. Wait for Linode to provision your server. This may take a few minutes.

### Step 5: Access Your Linode

1. Once your Linode is running, you will see it listed on the dashboard.
2. Click on your Linode to access its details.
3. Note the public IP address assigned to your Linode.

### Step 6: Connect to Your Linode

1. SSH to the server. If you are on a Windows machine I recommend using putty. If you are on a Mac or Linux you can use the terminal.

2. Login as root and use the password you set up when creating the Linode.

3. Once logged in, create a new user. This step is necessary because the T-Pot installation script cannot be run as the root user. Use the command below to create a new user:
```go
adduser <your user name>
```

You will be prompted to create a password.

1. Add the new user to the sudoer group by using the command below:

```go
usermod -aG sudo <you user name>
```

2. Switch to the new user using the command below:

```go
su <your user name>
```

## Install T-Pot

1. Once you have changed users, change the directory to the $HOME directory.

```go
cd $HOME
```

1. Run the following command:

```go
env bash -c "$(curl -sL https://github.com/telekom-security/tpotce/raw/master/install.sh)"
```

2. When completed you should receive the message seen below that asks you to reboot the system.

Note the port number. 

The next time you ssh to the server use that port number (64295) instead of port 22.

## Connect to T-POT Dashboard

Navigate to your dashboard (https://<your server IP>:64297)

##  Analyzing Honey Pot Data 

### Honeypot Tools and Their Data

As a review, there T-Pot integrates several honeypot tools, each designed to capture specific types of data. Below are just a few examples.

- **Dionaea**: Captures malware and exploits for various services.
- **Cowrie**: An SSH and Telnet honeypot that logs commands and sessions.
- **Conpot**: An ICS/SCADA honeypot that emulates industrial control systems.
- **Elasticpot**: Mimics Elasticsearch to capture attacks targeting this service.
- **Heralding**: Captures login attempts and credentials for various network services.
- **Mailoney**: Collects data from email-based attacks.
- **Surricata**: Network Traffic

## **Dionaea**

Since I am interested in malware, the first honeypot tool we will analyze is from Dionaea. Dionaea is an open-source honeypot designed to trap and analyze malicious activities by emulating a range of vulnerable services. Here’s a detailed overview of Dionaea:

### Features and Capabilities:

1. **Service Emulation**:
    - **SMB**: Server Message Block protocol used primarily for providing shared access to files, printers, and serial ports.
    - **HTTP/HTTPS**: Web services to capture web-based attacks.
    - **FTP**: File Transfer Protocol services.
    - **MySQL**: Database services.
    - **TFTP**: Trivial File Transfer Protocol services, often targeted by certain malware.
    - **MS-SQL**: Microsoft SQL Server services.
    - **SIP**: Session Initiation Protocol for voice over IP services.
    - **MQTT**: Message Queuing Telemetry Transport protocol often used in IoT devices.
    - **RDP**: Remote Desktop Protocol services.
2. **Malware Capture**:
    - Dionaea is capable of capturing malware that exploits vulnerabilities in the emulated services.
    - It saves the binaries of the malware for further analysis.
3. **Exploitation Detection**:
    - The tool logs the exploitation attempts, providing details about the source of the attack and the nature of the exploitation.
4. **Protocol Emulation**:
    - Dionaea can emulate different protocols to attract diverse types of attacks, making it versatile in capturing a wide range of malware and exploit attempts.
5. **Logging and Reporting**:
    - It logs various details about the attacks, including the IP address, timestamp, and the type of exploit used.
    - Logs can be stored in multiple formats, including SQLite and JSON.
6. **Modularity**:
    - The tool is designed to be modular, allowing for the easy addition of new protocols and features through its plugin architecture.

## Analysis

Starting with the dashboard we can see that the vast majority of attacks picked up by Dionaea are abusing the SMB protocol. The majority of the attacks originated within the United States and were from known attackers.

<img src="screenshots/Dionaea dashboard.png">

At the macro level this information is interesting. However, blocking IP addresses is like playing whack-a-mole. David Bianco’s Pyramid of Pain identifies that it is trivial for a malicious actor to overcome blocking IP addresses. The value of Dionaea and other honeypot tools is the ability to collect malware samples. This will allow us to conduct malware analysis and build rules and detections/alerts on the malware behavior. 

To retrieve the malware we need to ssh into the T-Pot server over port 64295. The path to the malware samples is /tpotce/data/dionaea/binaries.

As seen below there was only one unique malware samples collected. To quickly triage the sample we can run the hashe in VirusTotal. As seen below it was identified as being malicious. In fact, it was WannaCry, which should not be surprising considering that the majority of the attacks were attempting to abuse SMB. WannaCry uses the leaked NSA exploit EternalBlue to abuse SMB.

<img src="screenshots/virustotal check.png">

We can recover the malware samples by using the SCP protocol. If we are using Linux or a Mac we can run SCP from the terminal. On a Windows system you can use the GUI tool WinSCP. However, the most secure way to move the malware samples is to zip and password protect them. This can be done via ssh, but you must install zip on the T-Pot server with the command below:

```go
sudo apt install zip
```
You can zip and password protect the file by using the command below:

```go
sudo zip -e archive_name.zip file_to_zip
```

Replace archive_name.zip with the desired name for your zip file and file_to_zip with the name of the file you want to zip and protect. You will be prompted to enter and verify a password.

After zipping both files you can safely move them to your malware analysis machine using WinSCP.


You can now conduct malware analysis on the two malware samples.
<img src="screenshots/malware hash analysis.png">

The next important data from this honeypot is Cowrie is explain above. 

# Cowrie

Cowrie is a well-known open-source honeypot designed to emulate SSH and Telnet services, allowing researchers and security professionals to capture and analyze unauthorized access attempts.

### Features and Capabilities

1. **SSH and Telnet Emulation**:
    - **SSH**: Secure Shell protocol emulation, capturing login attempts and commands executed by attackers.
    - **Telnet**: Emulates Telnet services, which are still used in some legacy systems, attracting a different set of attackers.
2. **Session Logging**:
    - **Command Logging**: Records all commands entered by attackers, providing insights into their actions and intentions.
    - **Interactive Session Logging**: Captures entire interactive sessions, which can be replayed for analysis.
3. **File System Emulation**:
    - **Virtual File System**: Emulates a fake file system that attackers can interact with, containing fake files and directories.
    - **File Download and Upload**: Captures files downloaded and uploaded by attackers, aiding in malware analysis.
4. **Credential Harvesting**:
    - Logs all credentials (usernames and passwords) used in login attempts, which can be useful for understanding commonly used credentials and attack patterns.

### Bottom Line

Cowrie is a powerful tool in the cybersecurity toolkit, offering detailed insights into unauthorized access attempts and attacker behavior. It helps security professionals and researchers enhance their understanding of threats and improve overall security posture.

## Analysis

The Cowrie dashboard provides a macro-level characterization of the SSH and Telnet attacks. This includes the number and type of attacks, as well as where the attacks are coming from.

<img src="screenshots/cowrie dashboard.png">

Additionally, it includes the top user names and passwords attempted during the attacks, as well as the command line inputs used during the attack.

<img src="screenshots/cowrie data.png">

Once again, the dashboard provides a high level view of activity. We can dig deeper by using the Discover and Visualization features of Kibana.

In the Discover feature we can filter for Cowrie logs and the input field, which includes the command line inputs. The results show what commands the attacker ran from the CLI.

<img src="screenshots/kibana cowrie attack .png">

By using the Visualization feature we can build a table that shows the unique commands that were ran and the number of times they were ran.

<img src="screenshots/cowrie attack table.png">

### Downloaded Malware

Additionally, if any files were downloaded to the honeypot, we can retrieve those by using SSH to the server, similar to the way we previously did with Dionaea. The path to the Cowrie downloads is tpotce/data/cowrie/downloads.

<img src="screenshots/malware downlaod evidences.png">

# Heralding

Heralding is a unique and specialized open-source honeypot designed primarily to act as a credentials logging service for various protocols. It is particularly effective for capturing and analyzing login attempts across multiple services.

### Features and Capabilities

1. **Protocol Emulation**:
    - **SSH**: Secure Shell protocol, capturing credentials used in SSH login attempts.
    - **Telnet**: Captures login attempts and credentials used with the Telnet protocol.
    - **FTP**: File Transfer Protocol, logging login attempts and credentials.
    - **HTTP/HTTPS**: Captures credentials submitted through basic and digest authentication methods.
    - **SMTP**: Simple Mail Transfer Protocol, logging login attempts for email servers.
    - **POP3**: Post Office Protocol, capturing email access credentials.
    - **IMAP**: Internet Message Access Protocol, capturing credentials used for accessing email.
    - **VNC**: Virtual Network Computing, capturing login attempts and credentials.

2. **Credential Logging**:
    - Logs all credentials (usernames and passwords) attempted across various protocols.
    - Provides detailed information about the source of the login attempts, including IP addresses and timestamps.

### Use Cases

1. **Credential Harvesting**:
    - Ideal for environments where capturing and analyzing login attempts and credentials is crucial.
    - Helps in understanding common credentials used by attackers and identifying weak passwords.
2. **Threat Intelligence**:
    - Provides valuable data on login attempts, helping to identify patterns in attacks and common sources of credential-based attacks.
    - Useful for developing threat intelligence and improving defensive measures against credential stuffing and brute force attacks.

3. **Network Security Monitoring**:
    - Deployed in networks to detect and log unauthorized access attempts.
    - Acts as an early warning system by capturing credentials used in attempted logins, allowing for proactive responses.
    
    Heralding is a powerful and specialized honeypot tool that offers focused logging of credentials across multiple protocols. Its lightweight design and detailed logging capabilities make it an excellent choice for organizations looking to improve their understanding of credential-based attacks and enhance their overall security posture.

## Analysis

The dashboard provides the number of attacks and where they originated.

<img src="screenshots/Heralding dashboard.png">

Additionally, it shows the protocol, username and password attempted. 

<img src="screenshots/heralding protocol.png">

# Ciscoasa

The Cisco ASA (Adaptive Security Appliance) module in T-Pot is designed to emulate a Cisco ASA firewall, providing a high-interaction honeypot environment to attract and analyze attacks targeting this specific type of network device. T-Pot is a comprehensive honeypot platform that integrates multiple honeypot technologies, and the inclusion of the Cisco ASA module enhances its capability to mimic real-world enterprise environments.

### Features and Capabilities

1. **Emulation of Cisco ASA Firewall**:
    - **Command Execution**: Emulates the command-line interface (CLI) of a Cisco ASA firewall, allowing attackers to interact with it as they would with a real device.
    - **Configuration Simulation**: Provides a realistic environment where attackers can attempt to view or modify firewall configurations.
2. **Logging and Analysis**:
    - **Command Logging**: Records all commands entered by attackers, capturing their actions and methodologies.
    - **Session Logging**: Logs entire interactive sessions, which can be replayed for detailed analysis.
3. **Credential Capture**:
    - Captures credentials (usernames and passwords) used in login attempts, providing insights into common passwords and credential-based attack patterns.
4. **High-Interaction Environment**:
    - Offers a high-interaction environment that closely mimics a real Cisco ASA firewall, increasing the likelihood of capturing sophisticated attack techniques and behaviors.
5. **Integration with T-Pot**:
    - Seamlessly integrates with the T-Pot platform, benefiting from its centralized logging, analysis, and visualization capabilities.
    - Contributes to the overall threat intelligence gathered by the T-Pot ecosystem, enriching the data available for analysis.

### Use Cases

1. **Research and Analysis**:
    - Security researchers use the Cisco ASA module to study attack techniques and tactics targeting Cisco ASA firewalls.
    - Provides a platform for analyzing how attackers attempt to exploit firewall vulnerabilities or misconfigurations.
2. **Threat Intelligence**:
    - Contributes valuable data to threat intelligence efforts by capturing and analyzing real-world attacks.
    - Helps in identifying emerging threats and attack trends targeting enterprise network security devices.
3. **Network Security Monitoring**:
    - Deployed within enterprise networks to detect and log unauthorized access attempts on firewall devices.
    - Acts as a decoy to divert attackers from actual critical infrastructure, reducing the risk of successful breaches.


### Benefits

- **Realistic Emulation**: Provides a realistic simulation of a Cisco ASA firewall, increasing the attractiveness to attackers and the quality of captured data.
- **Comprehensive Logging**: Offers detailed logging of attacker interactions, aiding in the thorough analysis of attack techniques and behaviors.
- **Enhanced Security Posture**: By attracting and analyzing attacks on emulated firewalls, organizations can improve their understanding of threats and enhance their defensive measures.

The Cisco ASA module in T-Pot is a valuable tool for security researchers and organizations aiming to study and defend against attacks targeting Cisco ASA firewalls. Its realistic emulation and integration with the T-Pot platform make it a powerful component in a comprehensive honeypot strategy.

## Analysis

The dashboard provides the same type of information as previously discussed dashboards, with the major exception that these attacks are targeting Cisco ASA firewalls.

<img src="screenshots/ciscoasa dashboard.png">

### HoneyTrap

The honeytrap module of T-Pot is designed to detect, monitor, and analyze malicious activities and intrusions. Here’s a detailed overview of what the honeytrap module does:

### Functionality

1. **Network Traffic Capture**: The honeytrap module listens to network traffic directed at the honeypot, capturing data packets that interact with the system.
2. **Service Emulation**: It emulates various services and protocols to appear as a legitimate system, thereby attracting attackers. This can include common services like SSH, HTTP, FTP, etc.
3. **Logging and Alerting**: The module logs all interactions, including connection attempts and the types of attacks. Alerts can be generated based on predefined rules or behaviors.
4. **Behavioral Analysis**: It analyzes the behavior of the attackers, such as commands executed, tools used, and methods of exploitation.
5. **Data Collection**: The collected data can be used for further forensic analysis, helping security professionals understand attack patterns and techniques.
6. **Deception**: By providing a false environment, it misleads attackers into thinking they have found a real target, which helps in identifying and analyzing their methods without compromising actual systems.

### Benefits

- **Threat Intelligence**: Provides insights into current attack trends and techniques.
- **Early Detection**: Helps in early detection of malicious activities targeting the network.
- **Research and Development**: Aids in developing better security measures by understanding attacker behavior.
- **Incident Response**: Improves incident response strategies through detailed logs and analysis.

In summary, the honeytrap module of T-Pot serves as a proactive defense mechanism, luring attackers into a controlled environment to gather valuable intelligence and improve overall network security.
