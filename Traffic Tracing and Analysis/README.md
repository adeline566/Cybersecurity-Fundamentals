                                       Traffic Tracing and Analysis



# Overview

This assignment focused on capturing, filtering, and analyzing network traffic using Wireshark. The exercises included examining ICMP and DNS traffic, intercepting FTP credentials transmitted in plaintext, and reconstructing files transferred over the network. The objective was to gain hands-on experience with packet analysis and understand the security implications of unencrypted network communications.



## Task A – Packet Analysis

### 1. Total Packets Captured and Displayed

I captured network traffic using Wireshark and observed that 128 packets were captured and displayed. Since no display filter was applied, Wireshark displayed all captured packets.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/447c9e06-d593-42b4-b214-0084c5193ef6" />



### 2. Analyze ICMP Traffic

I applied the display filter icmp in Wireshark to view only ICMP traffic. After pinging the Ubuntu VM (192.168.10.18), Wireshark showed that 64 packets were captured, while 52 ICMP packets were displayed. The remaining packets belonged to other protocols and were hidden by the filter. This filter allowed me to focus specifically on ICMP communication, making it easier to analyze the ping requests and replies exchanged between the systems.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/24e6a4bd-f35a-43ee-b9c4-5419ea1cbdbe" />




### 3. Examine an ICMP Echo Reply

I selected an ICMP Echo Reply packet and recorded the following information:

* Source IP Address: 192.168.10.18
* Destination IP Address: 192.168.217.3
* Sequence Number:
* Big Endian (BE): 35772 (0x8bbc)
* Little Endian (LE): 48267 (0xbc8b)
* Data Size: 40 bytes
* Response Time: 13.367 ms

This packet confirmed successful communication between the systems.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/6135bed8-c658-416f-bded-13e0980b6998" />


### 4. Analyze DNS Traffic

I applied the DNS display filter in Wireshark to focus on Domain Name System (DNS) traffic. A total of 262 packets were captured, and 256 packets matched the DNS filter and were displayed. Applying this filter allowed me to analyze DNS queries and responses, providing insight into how domain names are resolved into IP addresses during network communication.
Screenshot Required: DNS-filtered packet capture.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/550737f4-757d-4fef-ab5c-5c0ae849d751" />



### 5. Examine a DNS Query

I identified a DNS query packet and observed that the host was attempting to resolve the domain name contile.services.mozilla.com. The query originated from 192.168.217.3:36106 and was sent to the DNS server at 192.168.217.2:53. This packet represents a DNS lookup request in which the client is asking the DNS server to provide the IP address associated with the specified domain name.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/af780165-0135-4c89-8a26-7e9b343f89aa" />



### 6. Examine the Corresponding DNS Response

I located the corresponding DNS response packet and recorded the following information: the source was 192.168.217.2:53, and the destination was 192.168.217.3:36106. The DNS server response was “Refused”, indicating that the server actively rejected the query and did not provide a valid domain name resolution for the requested domain.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/89d73efd-e72e-4b13-8559-5f9005b71589" />





## Task B – Traffic Sniffing


### 1. Sniff ICMP Traffic

#### a. Display Active ICMP Traffic

I configured Wireshark on Internal Kali to capture and display ICMP traffic generated while External Kali pinged both Ubuntu and Internal Kali.

This allowed me to observe ICMP Echo Requests and Echo Replies exchanged between the systems.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/7890c697-79e3-4bc6-9048-f5f5f0703757" />



#### b. Display Only ICMP Requests from External Kali to Ubuntu

I applied the following display filter:

icmp && ip.src == 192.168.217.3 && ip.dst == 192.168.10.18

This filter displayed only ICMP packets originating from External Kali and destined for the Ubuntu virtual machine.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/10b599b7-cc1a-438d-ad33-e97c2ebbab45" />



### 2. Sniff FTP Traffic

#### a. Connect to the FTP Server

Ubuntu was configured as an FTP server on the local area network. From External Kali, I established a connection to the server using the command ftp 192.168.10.18. The login was successful after providing the required credentials, confirming that the FTP service was reachable and properly configured.

<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/b0bb610d-a6d3-450d-b0f0-52e69e3cfa22" />


#### b. Recover FTP Credentials from Captured Traffic

As an attacker using Internal Kali, I monitored network traffic using Wireshark. I applied the display filter: ftp

Because FTP transmits data in plaintext, the username and password were visible within the captured packets. By examining the FTP authentication packets, I was able to identify the credentials used during login.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/0d60f259-271b-4522-ad93-8a19605c55a8" />


#### c. Capture Custom Credentials

I repeated the FTP login attempt using my MIDAS ID as the username and my UIN as the password. Although authentication failed, the credentials were still transmitted over the network. Internal Kali successfully intercepted the packets containing the login information. This demonstrated that attackers can capture sensitive data even when authentication attempts are unsuccessful.

<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/0e75e16e-851e-4049-a70f-bad30ce21fbe" />



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/ba394d74-1c72-4b75-90c0-c603c88b0dc7" />




## Task C – Extra Credit: Stealing Files with Wireshark

#### Create and Transfer a File

I logged into the Ubuntu VM and created a file named after my MIDAS ID. First, I used the echo command to write my name and the current timestamp into the file. I then verified that the file was successfully created using the ls command and confirmed its contents using the cat command. After completing this process, I switched to the External Kali machine and downloaded the file using the FTP protocol. Since I was unsure whether the first transfer was successful, I repeated the download to ensure the file was properly retrieved.

<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/6c404e15-7e6b-4524-a6ba-8287834832e9" />



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/9fe576a2-579b-4204-b1e1-294ee9bb04c8" />




#### 1. Display FTP-DATA Packets

On Internal Kali, I applied the display filter: ftp-data. This displayed only the packets associated with the file transfer between Ubuntu and External Kali.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/8a7e5198-0788-4f37-92a4-6455114b8722" />



#### 2. Follow the TCP Stream

I selected an FTP-DATA packet and used the Follow TCP Stream feature. This allowed me to reconstruct and view the contents of the transferred file directly from the captured network traffic.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/49440931-70ec-4760-a470-b59267098ffc" />




##### 3. Export and View the Transferred File

After reconstructing the transfer, I exported the file from Wireshark and saved it as a text file on Internal Kali. I then used the cat filename.txt command to verify the contents of the recovered file. The output confirmed that the recovered data matched the original file that was transferred from the Ubuntu machine.

<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/69c92f2e-d470-41eb-af99-c85daabf275e" />




# Lessons Learned

This assignment provided valuable experience in capturing and analyzing network traffic using Wireshark. I learned how display filters can be used to isolate specific protocols such as ICMP, DNS, FTP, and FTP-DATA, making packet analysis more efficient. Through the DNS exercises, I gained a better understanding of how domain name resolution works and how DNS responses are communicated between clients and servers.

The FTP exercises demonstrated the dangers of transmitting sensitive information over unencrypted protocols. I observed that usernames and passwords can be easily intercepted by attackers when FTP is used because the protocol sends credentials in plaintext. Additionally, I learned how attackers can reconstruct transferred files by capturing FTP-DATA packets and following TCP streams. This reinforced the importance of using secure alternatives such as SFTP or FTPS to protect sensitive information during transmission.

Overall, this assignment strengthened my understanding of network communications, packet analysis, protocol behavior, and the security risks associated with insecure network services.
