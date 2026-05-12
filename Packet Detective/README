#CyberDefenders Packet Detective Lab#
Learn how to inspect a network packet using Wireshark through CyberDefenders' Packet Detective lab.


Packet Detective by CyberDefenders
Wireshark is a powerful tool for inspecting network packets for abnormalities that is widely used in the cybersecurity world. On top of publicly available and FREE resources for learning Wireshark, CyberDefenders features an interactive lab to learn the network packet analyzer called Packet Detective. Navigating three .pcap files (otherwise known as packet capture files), you will learn to utilize various actions in Wireshark, to complete several questions. After you finish this lab, you will have a greater understanding of packet sniffing.

While I encourage searching for the solution on your own, utilizing guides especially as a beginner will speed up your learning process. You can use the Official Walkthrough, or find write-ups by different people to learn alternative solutions.

You may find more information on Wireshark here:

CompTIA’s Article on Wireshark

Wireshark’s User Manual

##Scenario##
In September 2020, your SOC detected suspicious activity from a user device, flagged by unusual SMB protocol usage. Initial analysis indicates a possible compromise of a privileged account and remote access tool usage by an attacker.

Your task is to examine network traffic in the provided PCAP files to identify key indicators of compromise (IOCs) and gain insights into the attacker’s methods, persistence tactics, and goals. Construct a timeline to better understand the progression of the attack by addressing the following questions.

##File: Traffic-1.pcapng##
Q1) The attacker’s activity showed extensive SMB protocol usage, indicating a potential pattern of significant data transfer or file access.
What is the total number of bytes of the SMB protocol?
Your task is to examine network traffic in the provided PCAP files to identify key indicators of compromise (IOCs) and gain insights into the attacker’s methods, persistence tactics, and goals. Construct a timeline to better understand the progression of the attack by addressing the following questions.

On the taskbar, navigate to Statistics -> Protocol Hierarchy

You can easily find the answer under bytes.

Q2) Authentication through SMB was a critical step in gaining access to the targeted system. Identifying the username used for this authentication will help determine if a privileged account was compromised.
Which username was utilized for authentication via SMB?
There are two common types of authentication:

· NTLM (NT LAN Manager)
· Kerberos

In the logs, you will notice a user who is trying to authenticate with NTLM.

Quick way to find out if there is a username associated with NTLM is to use the filter: “ntlmssp.auth.username”

Alternatively, you can easily scroll the packet list to find the first authentication attempt associated with a username.

Q3) During the attack, the adversary accessed certain files. Identifying which files were accessed can reveal the attacker's intent.
What is the name of the file that was opened by the attacker?
Since the files utilize the SMB protocol, use the taskbar and navigate to File -> Export Objects -> SMB

Finds any objects associated with SMB that is being accessed.

Here, you can easily find the file name.

Q4) Clearing event logs is a common tactic to hide malicious actions and evade detection. Pinpointing the timestamp of this action is essential for building a timeline of the attacker’s behavior.
What is the timestamp of the attempt to clear the event log? (24-hour UTC format)
Use “dcerpc.opnum == 0” filter to find the Clear Request. Opnum is an easy way to look for certain events:

· Opnum 0 is for ClearEventLog

· Opnum 7 is for ReadEventLog

· Opnum 1 is for BackupEventLog

· Opnum 4 and 5 are for GetNumberofEventLogRecords and GetOldestEventLogRecord respectively

In the taskbar, go to View -> Time Display Format -> UTC Date and Time of Day

Doing so can easily allow you to find the Date and Time.

##File: Traffic-2.pcapng##
Q5) The attacker used "named pipes" for communication, suggesting they may have utilized Remote Procedure Calls (RPC) for lateral movement across the network. RPC allows one program to request services from another remotely, which could grant the attacker unauthorized access or control.
What is the name of the service that communicated using this named pipe?
Use the following filter: “frame contains 5c:00:50:00:49:00:50:00:45”. These are Unicode for the following:

· 5c:00 is \

· 50:00 is P

· 49:00 is I

· 50:00 is P

· 45:00 is E

You will find one packet.

Investigate the packet details

If you look hard enough for any directories related to “PIPE”, you will find a file called atsvc which indicates an “AT Service/Task Scheduler.”

Alternatively, you may also find the same packet using CTRL+F, changing the search parameter to “Packet bytes” and a “String”, and type in PIPE. It will direct you to the only file with PIPE in its details. Using the same procedure, find the file associated with PIPE.

Q6) Measuring the duration of suspicious communication can reveal how long the attacker maintained unauthorized access, providing insights into the scope and persistence of the attack.
What was the duration of communication between the identified addresses 172.16.66.1 and 172.16.66.36?
Filter by “ip.addr” for both. Alternatively, you can use “ip.dst” and “ip.src” filters if you wanted to be more specific, but “ip.addr” is faster for this exercise.

Under the taskbar, navigate to Statistics -> Conversations

Under Duration, you will find the duration of the conversation between the two IP addresses.

##File: Traffic-3.pcap.ng##
Q7) The attacker used a non-standard username to set up requests, indicating an attempt to maintain covert access. Identifying this username is essential for understanding how persistence was established.
Which username was used to set up these potentially suspicious requests?
Once again, you can use “ntlmssp.auth.username” command to look for any usernames that are trying to do a NTLM authentication.

You will find two files, and you’ll be able to see the username of the first request.

Q8) The attacker leveraged a specific executable file to execute processes remotely on the compromised system. Recognizing this file name can assist in pinpointing the tools used in the attack.
What is the name of the executable file utilized to execute processes remotely?
Once again, use File -> Export Objects to file any files that are involved.

SMB is the only protocol that you need to be concerned with for this exercise if you look at the packets in the log. However, you can try each one to see what you can find. You will notice that there are only executables associated with SMB.

The only executable can be found here.

You can also use CTRL+F and do a String search for packet list including “.exe”

Congratulations! You have completed all of the exercises in Packet Detective!

##Takeaway##
Learning how to use a network packet analyzer like Wireshark is a great way to break into the cybersecurity industry. Now that you are done with these exercises, I encourage you to do more of CyberDefenders’ labs. You can also find more .pcap exercises on malware-traffic-analysis.net. I encourage you to complete these on a virtual environment.

Aside from Wireshark, which is a graphic user interface(GUI)-based packet sniffer, knowing how to use tcpdump, which is a command line interface(CLI)-based packet sniffer, can be beneficial. In the future, I hope to learn more about tcpdump to create a writeup on it.
