                              Password Cracking and Wireless Traffic Decryption


# Overview

This lab focused on password security and wireless network analysis using both Linux and Windows environments. The objectives were to create user accounts, generate password hashes, perform dictionary and brute-force password cracking attacks, and analyze encrypted wireless traffic. Throughout the lab, I used tools including John the Ripper, Meterpreter, Cain & Abel, Wireshark, and Aircrack-ng to better understand password security, password recovery techniques, and wireless encryption.



## Task A: Linux Password Cracking


### Step 1: Create Linux Groups

I created two Linux groups:

* cyse301
* My MIDAS ID group

After creating the groups, I displayed their corresponding Group IDs (GIDs) to verify that both groups had been successfully created.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/caf71176-c17a-4969-8573-3621f46cb159" />



### Step 2: Create User Accounts

I created three Linux user accounts and assigned each user to one of the newly created groups. I then verified each user's User ID (UID), Group ID (GID), and group membership.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/dfcc4699-1417-4b9f-9e97-39cda1b13f9e" />



### Step 3: Assign Passwords

I assigned different passwords with varying levels of complexity to the users.


<img width="468" height="219" alt="image" src="https://github.com/user-attachments/assets/c66d03ed-4a6d-4a2a-bf8b-5a1beab85546" />
These passwords were created specifically for the lab and were not real-world passwords.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/6135f7dd-9a93-4824-8cd8-5607989b277c" />



### Step 4: Export Password Hashes and Crack Passwords

I exported the password hashes for the three users into a file named:dharr003-hash

Next, I used John the Ripper to perform a dictionary attack against the password hash file. The attack successfully recovered at least one password, demonstrating how weak passwords can be cracked quickly using wordlists.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/b6a4a9f9-b3e7-455f-b84f-18e203b00d35" />



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/8a53734c-2870-466e-98db-7232320e7044" />




## Task B: Windows Password Cracking


### Step 1: Dump Windows Password Hashes

After creating three Windows user accounts with different passwords, I established a Meterpreter session with administrative privileges.

Using the Meterpreter command below, I extracted the Windows password hashes.

hashdump

The hashes were successfully displayed for the local Windows accounts.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/51ee6c81-9e3b-4eac-b8be-8d2bbdc4bf8f" />



### Step 2: Crack Windows Passwords with John the Ripper

The extracted password hashes were saved into a file named: dharr003.WinHASH

I then executed John the Ripper against the hash file for approximately ten minutes. At least one password was successfully recovered during the dictionary attack.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/9e6c8b10-c81f-44f1-b094-40ceafb1ad1d" />



### Step 3: Password Cracking with Cain & Abel

Using Remote Desktop, I opened Cain & Abel on the Windows 7 virtual machine.

Two password recovery techniques were tested:

* Dictionary Attack
* Brute Force Attack

At least one password was successfully cracked using these methods. The dictionary attack completed much faster because it compared passwords against an existing wordlist, while the brute-force attack systematically tested every possible character combination until a matching password was found.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/42139e6f-7d09-45cf-bbde-3c7b77710d81" />


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/395e11dd-fcb7-4407-9dcd-27812a1872e8" />



### Extra Credit: MD5 Password Cracking

Using John the Ripper, I identified the appropriate hash format by listing the supported formats and then attempted to crack the following MD5 hashes.

5f4dcc3b5aa765d61d8327deb882cf99
63a9f0ea7bb98050796b649e85481845

The appropriate hash format was selected before running the password cracking process.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/9d3db88b-c66c-4738-9ab7-c23c449ca333" />



## Task C: Wireless Traffic Decryption


### Step 1: Decrypt WEP Capture

The lab5wep-demo.cap capture file was successfully decrypted before being analyzed in Wireshark.

#### Traffic Analysis

The capture contained 142,415 packets.

Protocol distribution included:

<img width="468" height="183" alt="image" src="https://github.com/user-attachments/assets/5b72b82c-5400-4d06-95ce-e6da672b5670" />

The overwhelming majority of packets were ARP requests. Although ARP traffic is expected on local networks, the unusually high number observed in this capture suggests abnormal behavior. Such activity may indicate continuous ARP broadcasts, aggressive network scanning, ARP spoofing attacks, or a misconfigured device repeatedly issuing ARP requests. The capture clearly demonstrated how excessive ARP traffic can become a useful indicator of suspicious network activity.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/c36ec129-eb48-4de5-82c3-6494358c7fa8" />



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/14918f79-36c8-49ab-ae1b-4de8819899b7" />


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/22531dfa-d46b-4448-8e55-4e96d14534e9" />


### Step 2: Decrypt WPA2 Capture

The lab5wpa2-demo.cap file was successfully decrypted and analyzed.


#### Traffic Analysis

The capture contained 2,228 packets.

Protocol distribution included:

<img width="468" height="183" alt="image" src="https://github.com/user-attachments/assets/a2821b9d-ec19-41d2-bfcf-0365c56497e5" />

Compared to the WEP capture, the WPA2 capture contained significantly fewer packets and exhibited a much more balanced protocol distribution. The ARP traffic remained at a normal level, indicating typical network behavior rather than suspicious activity. Unlike the WEP capture, no excessive broadcast traffic was observed. Overall, the WPA2 traffic appeared representative of a healthy wireless network with standard communication between connected devices.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/f0d1df49-a53d-4951-ad3b-6b8507ad881a" />


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/c0cafd62-ba49-4cb0-815d-b5b3377aaf0c" />



## Task D: WPA2 Dictionary Attack


### Step 1: Perform a Dictionary Attack

Based on my assigned capture file (WPA2-P1-01.cap), I performed a dictionary attack to recover the WPA2 pre-shared key. Once the correct passphrase was identified, I used it to decrypt the wireless traffic successfully.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/fa9df1b6-67b9-4534-aac6-d3f0123190a7" />



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/7ab9a417-4121-459f-979b-aa00a33aad72" />


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/49e2b728-96df-4b72-b505-4e507928b8fb" />


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/909e98f5-c54e-4dbb-b0fa-c558b1aed4bf" />







### Step 2: Analyze the Decrypted Traffic

After decrypting the capture, I analyzed the wireless traffic using Wireshark.

A total of 2,660 packets were captured during the session. The traffic reflected normal wireless communication between several client devices, including Apple, Microsoft, and Xiaomi devices communicating through a Cisco Linksys wireless access point.

Several IEEE 802.11 management and control frames were observed, including:

* Request-to-Send (RTS)
* Clear-to-Send (CTS)
* Probe Responses
* Acknowledgements (ACK)
* QoS Null frames

Multiple Probe Response frames advertised the wireless network named CyberPHY, indicating that client devices were actively discovering and joining the network. The packet capture also contained EAPOL Key Messages 1 and 2 of the WPA2 four-way handshake. These packets were essential because they enabled the dictionary attack used to recover the wireless pre-shared key. Additionally, a Deauthentication frame was captured, showing the termination of one client's wireless connection.

Overall, the decrypted capture demonstrated how wireless authentication and communication occur within a WPA2-protected network and highlighted the importance of capturing the four-way handshake during wireless security assessments.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/f94c48b5-9873-4642-ae40-3b7e01ed1c9c" />






# Lessons Learned

This lab gave me practical experience with password security and demonstrated how attackers can recover weak passwords using both dictionary and brute-force attacks. I learned how Linux and Windows systems store password hashes and how tools such as John the Ripper, Meterpreter, and Cain & Abel can be used to extract and crack those hashes when passwords are not sufficiently complex. The exercises reinforced the importance of using strong, unique passwords and modern password hashing techniques to reduce the risk of password compromise.

The wireless security portion of the lab improved my understanding of WEP and WPA2 encryption. I learned how encrypted wireless traffic can be decrypted when the appropriate keys or handshakes are available and how Wireshark can be used to analyze wireless communication after decryption. Comparing the WEP and WPA2 captures demonstrated the differences in network behavior and reinforced why WPA2 provides significantly stronger protection than WEP. Overall, this lab strengthened my understanding of password security, wireless encryption, and the defensive measures organizations should implement to protect their systems and networks.
