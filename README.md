
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

<img src="screenshots/Screenshot 2024-08-21 at 19.55.40.png">

At the macro level this information is interesting. However, blocking IP addresses is like playing whack-a-mole. David Bianco’s Pyramid of Pain identifies that it is trivial for a malicious actor to overcome blocking IP addresses. The value of Dionaea and other honeypot tools is the ability to collect malware samples. This will allow us to conduct malware analysis and build rules and detections/alerts on the malware behavior. 

To retrieve the malware we need to ssh into the T-Pot server over port 64295. The path to the malware samples is /tpotce/data/dionaea/binaries.

As seen below there was only one unique malware samples collected. To quickly triage the sample we can run the hashe in VirusTotal. As seen below it was identified as being malicious. In fact, it was WannaCry, which should not be surprising considering that the majority of the attacks were attempting to abuse SMB. WannaCry uses the leaked NSA exploit EternalBlue to abuse SMB.

<img src="screenshots/Screenshot 2024-08-21 at 21.34.56.png">

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
