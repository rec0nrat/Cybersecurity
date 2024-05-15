###### Written by Tyler Weiss 20 MAR 2024

#### Exercise 16

##### Task 1
Run the 'cat' command against 'password.txt'. The 'cat' command outputs the contents of a file to the console with no capability to navigate or search the file. 
![[Pasted image 20240327204949.png]]
![[Pasted image 20240327222812.png]]
##### Task 2
Examine the contents of 'passwords.txt' with the 'less' command. Using the less command allows you to navigate and search through the file. Navigation of the file can be done using the arrow keys, other shortcut keys such as 'g' or 'G', page down with space bar or search using the '/' followed by the word or search function. Using 'less' will start you at the beginning of the file. Note that there a many more search and navigation options than what was previously described. To exit 'less' type 'q'.
![[Pasted image 20240327223736.png]]
![[Pasted image 20240327223800.png]]
##### Task 3
Run the command 'fgrep "123456" passwords.txt'. 'fgrep' or 'fixed grep', which is the same as 'grep -F', does not search using special characters in the regular expression but exact strings. The output of this command is any line that contains '123456' weather by itself or included in a string. 
![[Pasted image 20240327225756.png]]
![[Pasted image 20240327225823.png]]
#### Exercise 17

#### Task 1
Using 'vim' add “1234567890_from_first_file” to the end of the file after the zzz not a new line. 'vim' can be navigated using the arrow keys. In order to enter "insert mode" enter 'i'. Once in "insert mode" the file can be edited. Press "escape" to exit "insert mode" and enter ':', type 'wq' and hit enter to save and exit. Use 'tail' to validate that the changes have been made to the end of the file.
![[Pasted image 20240328000608.png]]
![[Pasted image 20240327235345.png]]
![[Pasted image 20240327235432.png]]
#### Task 2
Create a copy of the file 'password.txt' and name it 'passwords2.txt'. Edit the second file by changing the last line to “1234567890_from_second_file”. Use the 'cp' command to make a copy of the first file and store the copy as 'passwords2.txt'. Use 'vim' to edit and save the new file just described in task 1. Tail the file to show to validate the change.
![[Pasted image 20240328000413.png]]
This is the view from within vim
![[Pasted image 20240328000333.png]]
##### Task 3
Run the command 'fgrep 1234567890_ passw*'. Using the 'fgrep' will search for a string literal as previously described. Every instance of '123456789_' in a string will be output along with the name of the file where the string was found preceding it. Multiple files will be searched due to 'passw' being used with wildcard '\*' as the file argument. 
![[Pasted image 20240328001032.png]]
#### Exercise 18
##### Task 1-2
Run the command 'fgrep 1234567890_ passwords.txt > passwords3.txt'. As mentioned before 'fgrep' will search for a string literal and output lines containing that string. Since only a single file is being searched the output will only contain the strings from the file and not the file name. Redirecting the output to 'passwords3.txt' will cause no output to be printed to the console. By using 'tail' we can print the last ten lines of 'password3.txt' thus confirming it's contents.
![[Pasted image 20240328151219.png]]
##### Task 3
Run the command 'fgrep -c 1234567890_ passw*'. The '-c' switch for 'fgrep' stand for count and using 'passw*' will search each text file starting with that string. The output will contain the file name followed by the number of matches, or count, within files.
![[Pasted image 20240328122135.png]]
##### Task 5
Run the command 'fgrep -w 1234567890_ passw*'. The switch '-w' stands for 'word regex' will will cause 'fgrep' to match only whole words. As a side note, the information regarding different switches and options can be found by typing 'grep --help'. The output will contain the file name followed by the lines containing only the word being searched.
![[Pasted image 20240328122330.png]]
##### Task 6
Run the command 'fgrep -n 1234567890_ passw*'. The switch '-n' stands for 'line number' and will output the line number where a match is found. The output will contain the file name, the line number of the match and the matching line itself.
![[Pasted image 20240328122428.png]]
#### Exercise 19
##### Task 1
Run the command 'grep -E "\[0-9\]{10}\_from" passwords.txt'. The '-E' switch tells 'grep' to search using 'extended regex' which the use of more features and negates the need to escape certain characters. The regex in the command uses a class '\[0-9\]' with range of '{10}' to search for 10 numbers preceding the string literal '\_from'. The resulting output will be any line that contains a regex match within it.
![[Pasted image 20240328123004.png]]
##### Task 2
Run the command 'grep -E "\[0-9\]{10}\_from" passwords*.txt'. By using the wild card character '\*' within the file name the 'grep' command will search all password files. Since the regex is the same as the previous task the output should be same except it will also be preceded by the filename of where the match was found.
![[Pasted image 20240328123322.png]]
#### Exercise 20
##### Task 1-3
Using authy.log determine why there was a service interruption on our website.
Using authy.log determine by who was this done?
Using authy.log determine from where was this done from?

The website is run by a using a service. That service can be interrupted using the 'systemctl' command followed by an action (i.e. stop, start, restart, shutdown). Knowing that the service that is interrupted was for a website we may also assume that 'apache2' may be involved. If we grep the 'authy.log' file for any of these key words or commands we can narrow our search. The grep command used to in this example is 'grep systemctl authy.log -n' which will search for any use of the command 'systemctl' and print the line number followed by any matching entries. This produces a single result.
The output show that the command 'systemctl shutdown apache2' was issued by the user 'tara' using 'sudo' permissions. It also show where the command was issued from within the file system because 'PWD', which stands for 'present working directory' is equal to '/home/tara'.
![[Pasted image 20240328125710.png]]


