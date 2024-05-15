###### Written by Tyler Weiss
### Exercise 1
Create an Alternate Data Stream in command prompt.
#### Task 1
Create a simple text file using this echo command: echo Normal File > file_normal.txt
![[Pasted image 20240420110050.png]]

#### Task 2
Using the above method generate a hidden message as an alternate data stream. 
```
echo Evil Malware > badfile.txt:hiddenfile.txt
```

![[Pasted image 20240420110110.png]]

#### Task 3
While in the directory that you created the file with the ADS, run the following command: 
```
dir /r *.txt
```
![[Pasted image 20240420110333.png]]

The '/r' command will list all alternate data streams attached to files and '\*.txt* will narrow the listing to only text documents. The '$Data' tells us that this is a data type stream.
#### Task 4
What was the output of that dir command, what did that output mean?
![[Pasted image 20240420112915.png]]
![[Pasted image 20240420122437.png]]

The output shows that there is an alternate data stream attached to 'stream_public.txt' and that this stream is called 'stream_private.txt'. 
### Exercise 2
Prerequisite fciv must be in the system path. (protip, save it to your nmap folder, it is already in your path. C:\\\Program Files (x86)\\Nmap)

Create an Alternate Data Stream and check the MD5 hash of the streams.
#### Task 1
Create a simple text file using this echo command: 
```
echo Normal File > file2.txt
```
![[Pasted image 20240420123137.png]]
The above screen shot show the file creation. Use 'dir' and 'type' to verify its existence and contents.
#### Task 2
Obtain a hash of file2.txt
![[Pasted image 20240420123328.png]]

Should be: 27d306fd5ac51bee8414d5d3ecbcc481 (MD5)
I used 'fciv.exe' with the '-both' to obtain the hash for both MD5 and SHA1 algorithms.
#### Task 3
Add an alternate data stream to the file. 
```
echo Evil Malware > file2.txt:evil.txt
```
![[Pasted image 20240420123620.png]]

Use 'dir /r' to verify the ADS was created. Use 'more < \<file\>:\<fileADS\>' to print the contents of the ADS to the console.
#### Task 4
Where are your data integrity gods now? 
RE- Obtain a hash of file2.txt 
![[Pasted image 20240420123910.png]]

It is STILL: 27d306fd5ac51bee8414d5d3ecbcc481 (MD5)
Alternate Data Streams (ADS) were originally created to be compatible with Mac HFS+ file systems. This was used to attach related data to a file. It also be used to hide files, attach executables, and check file integrity. There are two types of ADS, the associated and isolated ADS. Isolated ADS does not attach itself to an existing file stream (ex. `echo "put malware here" > :evil.txt`).

![[Pasted image 20240420124826.png]]
Notice that the hash is different from the above example. This proves that the data streams are separate. ADS was created this way to not interfere with integrity checks of the original file stream.
### Exercise 3
Use the 'Get-Item' cmdlet in powershell to retrieve the file information. We will tdisplay the information for the file we creaated previously 'file2.txt'. Specify the file using '-Path' parameter. If you do not specify the file exactly (ie `Get-Item -Path ./`) the cmdlet will produce information on the current directory instead. Use this cmdlet with the '-Stream \*' parameter to print both Original Data Stream and ADS object information to the console.
![[Pasted image 20240420125754.png]]
Notice that the two data stream objects are printed out separately with their own property values displayed.

You could also use the command in this way without explicitly using the '-Path' parameter. The following commands show the object output of all text files in the directory.
![[Pasted image 20240420132728.png]]

The below command can be used to search this directory and all parent directories for a '.txt' objects and their ADS. 
```
Get-ChildItem -Path "C:\path\to" -Recurse | ForEach-Object { Get-Item -Path $_.FullName -Stream * }
```
![[Pasted image 20240420133132.png]]
![[Pasted image 20240420133145.png]]

