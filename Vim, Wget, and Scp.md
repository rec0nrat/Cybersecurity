###### Written by Tyler Weiss
#### Exercise 1 - Open a File in Vim
Objective: Open an existing file named example.txt in the current directory using Vim. 
Instructions: 
1. Navigate to the directory containing example.txt. 
2. Use the Vim command to open the file by typing vim example.txt. 
3. Once open, navigate through the file using the arrow keys. 
4. Exit Vim without making changes by pressing :q! and then Enter.
![[Pasted image 20240413165015.png]]
![[Pasted image 20240413165102.png]]
#### Exercise 2 - Editing and Saving Changes
Objective: Edit document.txt by adding a new line of text and save the changes. 
Instructions: 
1. Open document.txt with Vim by typing vim document.txt. 
2. Enter insert mode by pressing i. 
3. Move to the end of the file and add the following line: "This is a new line of text." 
4. Save the changes and exit Vim by pressing Esc to leave insert mode, then type :wq and press Enter.
![[Pasted image 20240413165202.png]]
![[Pasted image 20240413165325.png]]
#### Exercise 3 - Search for Text within a File
Objective: Open report.txt, search for the word "summary", and navigate to the first occurrence. 
Instructions: 
1. Open report.txt in Vim by typing vim report.txt. 
2. To search for "summary", type :/summary and press Enter. 
3. Once the first occurrence is highlighted, you can press n to move to the next occurrence or N to move to the previous one. 
4. Exit Vim by typing :q! and press Enter.
![[Pasted image 20240413165412.png]]
![[Pasted image 20240413165501.png]]
![[Pasted image 20240413165536.png]]
#### Exercise 4 - Download and Open a file from the Gutenberg Project
Objective: Download, and then open an existing file named pg25973.txt in the current directory using Vim. 
Instructions: 
1. wget https://www.gutenberg.org/cache/epub/25973/pg25973.txt 
2. Validate that the file pg25973.txt is in your working directory. 
3. Use the Vim command to open the file pg25973.txt. 
4. Once open, navigate through the file using the arrow keys. 
5. Exit Vim without making changes by pressing :q! and then Enter
![[Pasted image 20240413165717.png]]
![[Pasted image 20240413165842.png]]
#### Exercise 5 - Edit a file from the Gutenberg Project
Objective: Open and edit an existing file named pg25973.txt in the current directory using Vim. 
Instructions: 
1. Use the Vim command to open the file pg25973.txt. 
2. Once open, navigate through the file using the arrow keys. 
3. Navigate to where it states, “Title: Birds of the Rockies” 
4. Switch from NORMAL MODE to INSERT MODE 
5. Modify, “Title: Birds of the Rockies” to “Title: Birds of the Coasts” 
6. Exit vim without making changes by pressing :q! and then Enter. 
7. Use the Vim command to open the file pg25973.txt. 
8. Once open, navigate through the file using the arrow keys. 
9. Navigate to where it states, “Title: Birds of the Rockies”, validate that if you exit without making changes, it indeed abandons your changes. 
10. Switch from NORMAL MODE to INSERT MODE 
11. Modify, “Title: Birds of the Rockies” to “Title: Birds of the Coasts” and exit INSERT MODE 
12. While in NORMAL MODE, save your changes via vim by switching to COMMAND MODE 
13. While in COMMAND MODE, save by typing :w 
14. Re-enter COMMAND MODE, and exit vim by typing :q 
15. Validate your changes by using the head -n 15 pg25973.txt command.
![[Pasted image 20240413170058.png]]
![[Pasted image 20240413170226.png]]
![[Pasted image 20240413170308.png]]
![[Pasted image 20240413170333.png]]
![[Pasted image 20240413170435.png]]
![[Pasted image 20240413170549.png]]
![[Pasted image 20240413170619.png]]
![[Pasted image 20240413170636.png]]
![[Pasted image 20240413170653.png]]
![[Pasted image 20240413170728.png]]
#### Exercise 6 - Download and Open a file from the Gutenberg Project v2
Objective: Download, and then open an existing file named pg100.txt in the current directory using Vim. This is the “Complete Works of William Shakespeare” 
https://www.gutenberg.org/cache/epub/100/pg100.txt
Instructions:
1. Open it in vim, edit it, and abandon your changes. 
2. Validate your changes didn’t get saved. 
3. Open it in vim, edit it, and save your changes. 
4. Validate your changes did get saved.
![[Pasted image 20240413171008.png]]
![[Pasted image 20240413171055.png]]
![[Pasted image 20240413171123.png]]
![[Pasted image 20240413171157.png]]
![[Pasted image 20240413171258.png]]
![[Pasted image 20240413171356.png]]
#### Exercise 7 - Download and Copy a file from the Gutenberg Project to Linux
Objective: Download pg100.txt in Windows and then copy it out to your Linux server via scp.
![[Pasted image 20240413171853.png]]
![[Pasted image 20240413171946.png]]
![[Pasted image 20240413174749.png]]
![[Pasted image 20240413174846.png]]
#### Exercise 8 - Create a text file and then copy it to Windows
Objective: Create a file via vim and then copy it out to your Windows workstation via scp.
![[Pasted image 20240413180013.png]]
![[Pasted image 20240413183813.png]]
#### Exercise 9 - Create a text file and then copy it to Windows
Objective: Ensure you have 3 or more text files in your Linux home folder, and then copy it to Windows workstation via scp with one command.
![[Pasted image 20240413234528.png]]
![[Pasted image 20240413234718.png]]
