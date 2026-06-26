                         Ethical Hacking: Exploiting Windows Systems with Metasploit


# Overview

In this lab, I explored post-exploitation techniques using the Metasploit Framework against vulnerable Windows systems in a controlled lab environment. The objectives included identifying SMB vulnerabilities, exploiting the MS08-067 vulnerability on Windows XP, testing the EternalBlue exploit against Windows Server 2022, creating and deploying a custom payload to Windows 7, performing post-exploitation tasks with Meterpreter, and observing why certain exploitation attempts failed on systems that were not vulnerable.



## Task A: Exploit SMB on Windows XP with Metasploit


### Step 1: Perform Network Scanning

I began by scanning the Windows XP target using Nmap to identify open ports, running services, operating system information, and potential SMB vulnerabilities.

The scan confirmed that TCP port 445 (SMB) was open and available for exploitation.

nmap -sS -sV -O <Windows-XP-IP>



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/e27e757c-6a9f-40ba-bdbf-d4929236b7a5" />





### Step 2: Launch Metasploit

After confirming that SMB was accessible, I launched the Metasploit Framework and searched for the MS08-067 NetAPI exploit module.

* searched for: ms08_067_netapi

The search returned the exploit module targeting the Microsoft Server Service vulnerability.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/2c473eb4-ecf9-42b8-9d23-a1e089319464" />



### Step 3: Configure the Exploit

I selected the ms08_067_netapi exploit and configured it to use the Meterpreter reverse TCP payload.

The listener was configured to use port 5525, and the remaining parameters, including the target IP address and local host address, were configured appropriately before launching the exploit.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/90fe08dd-5ad7-4b5a-866c-923d1c399e8d" />



### Step 4: Establish a Meterpreter Session

After launching the exploit, a Meterpreter reverse shell was successfully established with the Windows XP target. This provided remote access to the compromised system and allowed post-exploitation activities to be performed.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/ab1a81d0-f06a-49ff-bc84-6914e11f6fef" />


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/9e62d81d-5307-466d-8df2-710b5571078b" />



### Step 5: Capture the Target Screen

Using the Meterpreter shell, I executed the screenshot command to capture the desktop of the compromised Windows XP machine. This demonstrated that the exploit provided interactive access to the target system.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/1e8f7c67-3801-4cd7-88f0-9303a4161a0e" />



### Step 6: Display the System Date and Time

Within the Meterpreter session, I displayed the target system's local date and time. This verified successful interaction with the operating system.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/d1e335c8-a7f2-4797-82b6-6ba2dac9bdb0" />



### Step 7: Retrieve the User SID

Next, I obtained the Security Identifier (SID) associated with the current user. The SID uniquely identifies user accounts within Windows and is commonly referenced during privilege escalation and account enumeration.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/c2f8caaa-97c6-4532-b1b2-ae8b0a3731a1" />



### Step 8: Display the Current Process ID

I retrieved the Process Identifier (PID) of the active Meterpreter process. This information helps identify which process is hosting the Meterpreter session.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/63901f29-0150-4324-96aa-95e8124d4791" />




### Step 9: Gather System Information

Finally, I collected system information from the compromised Windows XP machine, including operating system details, architecture, hostname, and other identifying information.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/a80c9243-707d-464c-9aab-b44c05a5e505" />




## Task B: Test the EternalBlue Exploit on Windows Server 2022

Following the same procedure used in Task A, I attempted to exploit the Windows Server 2022 virtual machine using the EternalBlue exploit.

The exploit module successfully launched, and a TCP reverse shell attempt was initiated. However, the Meterpreter session was never established because the target system was not vulnerable to the exploit.


#### Metasploit reported:

"Exploit completed, but no session was created."

This message indicates that the exploit executed and the payload was delivered, but the target system did not establish a reverse connection. Since Windows Server 2022 includes modern security protections and is not affected by the MS17-010 vulnerability, the exploitation attempt failed as expected.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/01d0fb25-ac22-4b63-aac3-f4c2c95ed8a2" />



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/e197624c-cb92-4f5a-8175-8c8162338d88" />



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/0e1653c5-7e60-4881-8c95-84fd9f38cc35" />




## Task C: Deliver a Custom Payload to Windows 7

### Step 1: Create and Deploy the Payload

I generated a custom executable payload using MSFVenom.

The payload was configured with:

* Payload filename: YourMIDASID.exe
* Reverse shell listener port: 4444 (or 5525)

The executable was uploaded to the Kali web server, downloaded from the Windows 7 virtual machine, and executed to establish a reverse Meterpreter session. Before executing the payload, the Metasploit handler was configured to listen for incoming reverse connections.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/a25d9d5b-d3cc-44e8-b450-0fa8fc18050f" />


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/a25b60ee-a5c6-4d7f-8e35-d6233aa2f314" />


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/2e556c09-f089-46cb-800e-4fba1b43f6a8" />


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/3c322069-8d77-493d-9df1-ff51c01cff35" />




### Step 2: Capture a Screenshot

Once the reverse shell was established, I captured the Windows 7 desktop using the Meterpreter screenshot command.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/30d0f5b9-baec-455f-a62a-a26852c11a3d" />



### Step 3: Upload a File to the Target

I created a text file named using my MIDAS ID containing the current timestamp. The file was uploaded from the Kali attacker machine to the Windows 7 desktop using Meterpreter's upload command. After logging into Windows 7, I confirmed that the uploaded file existed on the desktop.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/952a63cc-3a7b-4fe4-9568-ef3bd271e236" />



### Step 4: Extra Credit – Password Hash Extraction

Using the hashdump command, I extracted password hashes from the compromised Windows 7 machine and saved the output to a file named hash.txt. This demonstrated how credential material can be obtained after administrative privileges are acquired.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/cbcf44d5-1315-4602-8253-dd4f74662d99" />




### Step 5: Privilege Escalation

After backgrounding the initial Meterpreter session, I performed privilege escalation to obtain administrator-level access. Once elevated privileges were obtained, I confirmed that the session had SYSTEM or Administrator privileges before continuing with post-exploitation tasks.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/efd507a8-f09e-49a2-a80c-f2c5a4608de1" />


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/eb750d8e-97bc-4b1c-a0aa-270955251d92" />




### Step 6: Create a New Administrator Account

Using the elevated Meterpreter session, I created a new user account and added it to the local Administrators group. This demonstrated how attackers can establish persistent administrative access after compromising a system.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/be7f54f9-f62b-49f9-a212-a330cc2c5ced" />



### Step 7: Remote Desktop Access

Finally, I remotely logged into the newly created administrator account using Remote Desktop Protocol (RDP). After logging in successfully, I browsed the files belonging to the Windows 7 user to verify access to the compromised system.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/3ba85a3c-a10a-4081-9fd7-9da858a1416e" />


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/236fb159-c76f-4e52-bba2-2c2bbb2ec265" />




## Task D: Extra Credit – Windows 10 Exploitation Attempt

An additional attempt was made to establish a reverse Meterpreter shell against a Windows 10 virtual machine. 

Although the exploit module executed, Metasploit displayed the following message: "Exploit completed, but no session was created." 

This indicates that the payload was delivered but the Windows 10 system did not establish a reverse connection. The most likely explanation is that the operating system had been patched or included security mechanisms that prevented the exploit from succeeding. This result demonstrates an important aspect of penetration testing: not every exploit succeeds. Successful exploitation depends on the target operating system version, patch level, enabled security features, and vulnerability status.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/3bf4ed49-e3e9-4ca8-beec-30a14becd6c7" />


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/9f0d91e1-02da-4339-ba7f-d191fc20a43d" />





# Lessons Learned

This lab provided valuable hands-on experience with exploitation and post-exploitation techniques using the Metasploit Framework. I learned how to identify SMB services through network scanning and use Metasploit to exploit known vulnerabilities such as MS08-067 on vulnerable Windows systems. I also gained practical experience interacting with compromised hosts through Meterpreter by capturing screenshots, gathering system information, retrieving user SIDs, uploading files, extracting password hashes, and performing privilege escalation.

Additionally, I learned that exploitation attempts do not always succeed. When testing EternalBlue against Windows Server 2022 and attempting to compromise Windows 10, Metasploit reported that the exploit completed without creating a session because the targets were not vulnerable. This reinforced the importance of verifying system versions, patch levels, and vulnerability status before attempting exploitation. Overall, this lab strengthened my understanding of both offensive security techniques and the defensive value of regularly patching systems to protect against known exploits.
