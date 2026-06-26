                                                  Basic Linux Commands


# Overview

This lab introduced fundamental Linux command-line operations used for navigating the file system, displaying system information, creating files, and working with directories. These commands are essential for system administration, cybersecurity, and general Linux usage. Throughout the lab, I practiced basic terminal commands that are frequently used in Linux environments.


## Task A: Practice with Basic Linux Commands


### Step 1: Find the IP Address of the Linux Machine

To determine the IP address of my Linux machine, I used the following command: ifconfig

The command displayed the network interfaces and their assigned IP addresses, allowing me to identify the IP address of my Linux system.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/48deda55-5503-491e-babe-14bd97c81aed" />



### Step 2: Display the Current Working Directory

To display my current location in the file system, I used: pwd

The pwd command displays the full path of the directory I am currently working in.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/9680179e-c074-4770-9df3-70d2fe13e9a1" />



### Step 3: Print My Name to the Console

To display my name in the terminal, I used the following command: echo "Adeline Harris"

The echo command prints text directly to the terminal.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/0e60559f-1820-4076-9fec-78047c23d979" />



### Step 4: Display First and Last Name on Separate Lines

To print my first and last names on separate lines using a single command, I used: echo -e "Adeline\nHarris"

The -e option enables the interpretation of escape characters, while \n inserts a new line between the first and last names.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/b87eca05-0c89-4b28-87bc-5810c7ddd1d2" />



### Step 5: Change to the Home Directory

To navigate to my home directory using an absolute pathname, I used: cd /home/Adeline

This command changed my current working directory to my home directory.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/cf80d263-2af2-4ba8-bade-6d3f067dc07b" />



### Step 6: Create a New File and Display Directory Contents

I created a new text file named dharr003.txt. Next, I displayed the contents of my home directory using the long listing format: ls -l

The long listing displayed file permissions, ownership, modification date, and file size. Since the file was newly created using the touch command, its size was 0 bytes.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/c519fd61-2483-4a15-9c50-3c0a240efba0" />



# Lessons Learned

This lab helped me become more comfortable using the Linux command line to perform basic system administration tasks. I learned how to identify my system's IP address, determine my current working directory, navigate the Linux file system, and create new files from the terminal. I also learned how the echo command can display text and interpret escape characters to format output. Finally, I gained experience using the ls -l command to view detailed file information, including permissions, ownership, and file size. These basic Linux commands provide a strong foundation for more advanced system administration and cybersecurity tasks.
