###### Written by Tyler Weiss
### Exercise 1 - Encoding
#### Task 1-2
1. Encode the following message using base64 encoder. 
2. Take the the encoded string and decode it using the base64 encoder. 
The output of echo is piped to the base64 program as input allowing us to encode the echoed string. Since the original message was produced by decoding the encoded string this proves that the encoder worked properly. 
```
echo "You guys are AWESOME!" | base64
echo "WW91IGd1eXMgYXJlIEFXRVNPTUUhCg==" | base64 --decode
```
![[Pasted image 20240414000120.png]]
#### Task 3
1. Append the string 'This is evil naughty naughty malware' to a file called 'malware.txt'. 
2. Cat the contents of 'malware.txt' to show that it contains the string. 
3. Cat the contents of 'malware.txt' and redirect the output to the base64 encoder appending the encoded string to 'notmalwarenoreally.txt'.
4. Cat 'notmalwarenoreally.txt' to prove the contents of the file and show the encoded string.
5. Cat 'notmalwarenoreally.txt' and redirect the output to the base64 decoder as input.
This series of actions proves that the encoded value in 'notmalwarenoreally.txt' is the base64 equivalent of the string 'This is evil naughty naughty malware' that is stored in 'malware.txt'.
![[Pasted image 20240414000622.png]]
#### Task 4
1. Produce an md5 hash of 'malware.txt' using 'md5sum'
2. Produce an md5 hash of 'notmalwarenoreally.txt' using 'md5sum'
Even though the contents of 'notmalwarenoreally.txt' is the base64 encoded version of the contents of 'malware.txt' the hashes are different because the contents of the files are different. This illustrates a method of evading anti-virus software by obfuscating the the file contents thus changing the digital signature of the original file.
![[Pasted image 20240414001208.png]]
### Exercise 2 - Hashing
#### Task 1
1. Echo 'hello world' and redirect the output to 'file1.txt'
2. Echo 'hello world' and redirect the output to 'file2.txt'
3. Cat the contents of both files.
4. Compare the md5 hash of the files using 'md5sum'.
![[Pasted image 20240414005322.png]]
Please note that the MD5 hash of the outputs are identical to each other. That means when you created the files, they were identical, so were their hashes. This proves the deterministic nature of using the same hash function, which in this case was md5.
#### Task 2
1. Echo 'hello world!' and redirect the output to 'file3.txt'
2. Cat 'file3.txt'. 
3. Compare the md5 hash of the previous files with that of 'file3.txt' using 'md5sum'
![[Pasted image 20240414005600.png]]
Please note that by inputting different text into file3, that the hash is wildly different that the files in Task 1. This is due to the Avalanche effect in Hashing.
#### Task 3
1. Run the following command to download 'catpicturess.jpg' using 'wget'.
```
wget https://github.com/ajay63/BlackTowerAcademy/blob/main/catpicturess.jpg
```
2. Get the md5 hash of 'catpicturess.jpg' using 'md5sum'.
![[Pasted image 20240414005844.png]]
3. Browse to virus total: https://www.virustotal.com/gui/home/search 
4. Copy the hash above for catpicturess.jpg and paste it into the search field in virustotal. 
5. No matches were found meaning that 'catpicturess.jpg' was not a virus.
![[Pasted image 20240414005937.png]]
![[Pasted image 20240414010001.png]]
#### Task 4
1. Open a browser to https://www.virustotal.com.
2. Create an account.
3. Navigate to the API key.
![[Pasted image 20240414010420.png]]
![[Pasted image 20240414010434.png]]
![[Pasted image 20240414010541.png]]
4. We have to download the pre-compiled VirusTotal Application to the Linux server. Use the following command to download the zipped file. 
5. List the directory to check that the file exists.
```
wget https://github.com/VirusTotal/vt-cli/releases/download/1.0.0/Linux64.zip
```
![[Pasted image 20240414010655.png]]
![[Pasted image 20240414011039.png]]
6. Install 'unzip'.
7. Unzip the file 'Linux64.zip'
8. List the directory to prove the virustotal 'vt' executable exists. 
9. Initialize the program by running './vt init'.
10. Input the API key from the virustotal website.
![[Pasted image 20240414011802.png]]
![[Pasted image 20240414011855.png]]
11. Get the md5 hash of 'catpicture.jpg'.
12. Check the hash to see if it is malware using the 'vt' program and the 'file' option.
Since the searched returned 'File \<hash\> not found' we can assume it is not a virus and has no listing on virustotal.
![[Pasted image 20240414012325.png]]
Let’s use a known bad hash now.
13. Pull up our Virus Total Web page, and paste in the following known bad hash: 00434c7dabe90c49dfcb78038e7595e1cfb87851
![[Pasted image 20240414012540.png]]
![[Pasted image 20240414012625.png]]
![[Pasted image 20240414012656.png]]
14. Check the same file hash using the 'vt' program.
![[Pasted image 20240414012922.png]]
15. Redirect the output to a file named 'ebil.txt'.
16. Use one of the Linux text readers to read 'ebil.txt'
![[Pasted image 20240414013346.png]]
![[Pasted image 20240414013417.png]]
Now by using the command line interface text connection to virus total, I can bring in automatable log enrichment and information that can be used with other code to provide good threat intelligence and way to populate cybersecurity systems.
### Exercise 3 - Encryption
Encrypting and Decrypting Files with GPG. 
Objective: Learn how to encrypt and decrypt files using GnuPG (GPG) on a Linux system. 
Prerequisites 
- Access to a Linux system 
- Install GnuPG installed. 
- Basic knowledge of navigating the Linux command line interface.
#### Task 1
Installation: Ensure that GnuPG is installed on your system. You can install it using the package manager of your Linux distribution. For example, on Ubuntu or Debian, you would use: 
```
sudo apt install gnupg -y
```
#### Task 2
1. To encrypt the file 'malware.txt' symmetrically (using a passphrase), run: 
```
gpg --symmetric malware.txt
```
 2. GPG will prompt you to enter a passphrase. Choose a strong, memorable passphrase. Confirm the passphrase when prompted. 
 3. After encryption, a new file with the extension '.gpg' will be created (in this case, malware.txt.gpg). 
 4. You can see this new file by listing the contents of the directory with ls.
![[Pasted image 20240414014210.png]]
![[Pasted image 20240414014244.png]]
![[Pasted image 20240414014324.png]]
![[Pasted image 20240414014357.png]]
5. Attempt to view the encrypted file's contents using cat 'malware.txt.gpg'. You'll see that the output is garbled, indicating the content is encrypted.
![[Pasted image 20240414014511.png]]
Keep in mind if you are decrypting locally, during the encryption process earlier you should have seen: 
```
gpg: directory '/home/ajay/.gnupg' created 
gpg: keybox '/home/ajay/.gnupg/pubring.kbx' created 
```
This means there is a pubring, is a local file that is keeping your symmetric keys for you. When you go to decrypt locally, you won’t be prompted to provide the password. If you provide it to another person, you will need to provide the symmetric private key.
6. To decrypt the 'malware.txt.gpg' file, run: 
```
gpg --decrypt malware.txt.gpg > decrypted.malware.txt
```
7. View the contents of the decrypted file using 'cat decrypted.malware.txt'. 
8. The output should match the original malware.txt file, in this case, displaying "This is evil naughty naughty malware"
![[Pasted image 20240414015155.png]]
Remember, the security of encrypted files depends on the strength of the passphrase and the security of the system used for encryption and decryption. 
