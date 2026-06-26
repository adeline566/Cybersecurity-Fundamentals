                                       Steganography




# Overview

In this lab, I explored the concept of digital steganography, which is the practice of concealing secret information inside digital media such as images, audio files, or videos. Using the Steghide utility in Kali Linux, I embedded a text file containing personal information into a bitmap image, encrypted the hidden data with a password, extracted the concealed message, and verified that the extraction was successful. This exercise demonstrated how steganography can be used to securely hide information while keeping the existence of the message unobvious.



## Step 1: Create the Secret Text File

I created a text file containing answers to the required questions:

* My name
* The current date and timestamp
* My expected grade in the course

The text file served as the secret message that would later be embedded into the cover image.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/be5517c3-a215-4d78-94e3-19a21d28530d" />



## Step 2: Hide the Secret File Using Steghide

Using the provided "Monarch.bmp" image as the cover file, I embedded the text file into the image with the Steghide utility.

I used my assigned UIN as the encryption password and selected one of the available encryption algorithms. The output stego image was saved using my lowercase MIDAS ID as the filename.

* steghide embed -ef private.txt -cf Monarch.bmp -sf dharr003.bmp

During execution, Steghide prompted me to: Enter the encryption password (my UIN)

After completion, a new bitmap image containing the hidden message was successfully created.

<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/927bd987-5beb-403e-a913-20d5d9bd17c2" />


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/1ab8f92d-f0c7-4454-87d0-afa0042b2b6c" />



## Step 3: Extract the Hidden Message

Next, I extracted the hidden information from the stego image using Steghide. The extracted data was saved as the required output file.

* steghide extract -sf dharr003.bmp -xf extracted_Adeline.bmp

When prompted, I entered the same password (my UIN) that was used during the embedding process. The extraction completed successfully, revealing the original hidden text file.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/f35f70e9-968a-4334-ad03-d5cfe08af93a" />


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/f706b042-49d4-4338-9ee1-a89bc9bee2ed" />



## Step 4: Verify the Extracted File

After extracting the hidden message, I listed the contents of the current directory to verify that the secret text file had been recovered successfully. The directory listing confirmed that the extracted text file appeared after the extraction process.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/a07fb654-fff6-41aa-ac5c-86651d691e25" />


## Step 5: Display the Secret Message

Finally, I displayed the contents of the extracted file to verify that the hidden information remained intact.

* type private.txt

The output displayed the original information exactly as it was before it was hidden inside the bitmap image. This confirmed that the embedding and extraction processes were both successful and that the data was not modified during encryption or recovery.

<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/e8c0ca29-c765-4f0b-bd82-195b6a187b45" />






# Lessons Learned

This lab helped me understand how steganography differs from encryption by focusing on hiding the existence of information rather than simply protecting its contents. I learned how to use Steghide to securely embed a text file inside an image and encrypt the hidden data with a password to provide an additional layer of security. I also learned that successful extraction requires the correct password, demonstrating the importance of proper key management. Finally, this exercise showed how digital steganography can be used for secure communication while also highlighting why security professionals need to be aware of steganography as a technique that can potentially be abused to conceal malicious or sensitive data.
