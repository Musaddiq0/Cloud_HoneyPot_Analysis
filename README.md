
# Setting-Up and Analysis of Cloud-based Honey Pot

## Why a Honey Pot?

1. **Threat Intelligence Gathering**: Honeypots capture detailed information about attack patterns and help identify new threats.
   
2. **Malware Collection and Analysis**: They collect and analyze malware samples, allowing for reverse engineering to understand their behavior and impact.

3. **Understanding Attacker Behavior**: Researchers can observe attacker techniques and credential use, gaining insights into their methods and decision-making.

4. **Improving Defensive Measures**: Data from honeypots enhances intrusion detection systems (IDS/IPS) and aids in developing security policies and countermeasures.

5. **Training and Education**: Honeypots provide real-world scenarios for hands-on learning without risking actual systems.

6. **Forensic Analysis**: They offer valuable forensic data for incident response and can sometimes serve as legal evidence.

7. **Vulnerability Research**: Honeypots help identify system weaknesses and capture zero-day exploits.

8. **Enhancing Threat Sharing**: Honeypot data can be shared with the cybersecurity community, contributing to collaborative defense and threat intelligence feeds.

### Bottom Line:
Honeypots are essential tools that provide researchers with real-world data on cyber threats, enhancing their ability to defend against attacks and share knowledge across the cybersecurity ecosystem.

For this project i decided to use Tpot as the honeypot platform tool which was set up on a cloud server which i will be discussion in the follwing discussion.

**T-Pot** is a comprehensive honeypot platform that collects a wide range of data to analyze cyber threats:

1. **Network Traffic**: Logs IP addresses, targeted ports, and network protocols (e.g., TCP, UDP).
2. **Attack Signatures**: Captures payloads, malicious code, and specific exploits used against the honeypot.
3. **Intrusion Attempts**: Records brute force attacks, port scans, and other reconnaissance activities.
4. **Malware Samples**: Collects binaries, scripts, and records their execution behavior.
5. **Session Data**: Logs commands and interactive sessions used by attackers on services like SSH or web servers.
6. **Files and Artifacts**: Tracks uploaded and modified files by attackers.
7. **Credential Usage**: Records usernames, passwords, and authentication attempts.
8. **Exfiltration Attempts**: Monitors attempts to exfiltrate data from the honeypot.

## Setting up a Linode linux server

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

### Installation of T-pot 

1. Once you have changed users, change the directory to the $HOME directory.

```go
cd $HOME
```

2. Run the following command:

```go
env bash -c "$(curl -sL https://github.com/telekom-security/tpotce/raw/master/install.sh)"
```
3. When completed you should receive the message seen below that asks you to reboot the system.
   <img src="screenshots/t-pot_installation.png>
  
   Note the port number. 

The next time you ssh to the server use that port number (64295) instead of port 22.

## Connect to T-POT Dashboard

Navigate to your dashboard (https://<your server IP>:64297) 

<img src="screenshots/Tpot interface.png">

You are now connected and the honeypot is online and is likely already being attacked.

Select the Attack Map for a pew pew map view.

<img src="screenshots/attack_map.png>

The Kibana menu will be the most used menu item. It is where the various dashboards are located.
<img src="">

### Specific T-Pot Tool Dashboards and Their Data

T-Pot integrates several honeypot tools, each designed to capture specific types of data:

- **Dionaea**: Captures malware and exploits for various services.

<img src="screenshots/Dionaea dashboard.png">
- **Cowrie**: An SSH and Telnet honeypot that logs commands and sessions.

<img src="screenshots/ciscoasa dashboard.png">
- **Conpot**: An ICS/SCADA honeypot that emulates industrial control systems.
<img src="screenshots/conpotDashboard.png">

- **Elasticpot**: Mimics Elasticsearch to capture attacks targeting this service.
<img src="screenshots/elasticpot_dashboard.png">
- **Mailoney**: Collects data from email-based attacks.
<img src="screenshots/mailoneyDashboard.png">

**Surricata**: Network Traffic
<img src="screenshots/SurricateDashboard.png">

