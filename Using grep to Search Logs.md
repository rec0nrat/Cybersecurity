###### Written by Tyler Weiss, 06 MAR 2024

grep for 'user1' in log 'windows_activity_logs.txt'. No output is printed to the console because Linux and the grep command are both case sensitive and no line in the file contains 'user1'.
![[Pasted image 20240306102435.png]]
grep for 'User1' in log 'windows_activity_logs.txt'.
![[Pasted image 20240306102304.png]]

Output from grep is printed to the console showing the argument 'User1' highlighted in red. 
- The argument 'user1' and 'User1' are different due to capitalization.
- grep outputs all lines in the file containing the argument.

grep for 'User3' in log 'windows_activity_logs.txt'. The output should output all lines containing the word string 'User3' from the searched log. 
![[Pasted image 20240306104640.png]]

grep for 'Document1' in log 'windows_activity_logs.txt'.
![[Pasted image 20240306102912.png]]

grep for 'Document1.docx' in log 'windows_activity_logs.txt'.
![[Pasted image 20240306102959.png]]

Notice that searching for 'Document1' and 'Document1.docx' yields different results.
- Observe that the highlighting is different in both grep searches.
- The argument being search for is highlighted in red.

Copy 'windows_activity_logs.txt' to 'windows_activity_logs.txt2'.
- Validate that both text documents exist and are the same using 'md5sum' and 'diff'.
![[Pasted image 20240306103928.png]]
![[Pasted image 20240327194716.png]]
Notice that the hash values are a match showing that there is no difference between the files.
- Note that using the wild card character allows for both files to be processed by 'md5sum' at the same time creating and easier comparison of the hash values.
- 'diff windows_activity_logs*.txt ' has no output because the files being compared have no differences between them. The files are exactly the same except for the file name.

grep for 'Spreadsheet.xls' in both 'windows_activity_logs.txt' and 'windows_activity_logs2.txt'.
- Use the wild card character in the grep command to reference both files.
![[Pasted image 20240306104131.png]]
![[Pasted image 20240306104212.png]]

Observe that the console output prints all lines containing the argument 'Spreadsheet.xls' in both files.
- The name file being searched is highlighted in purple.
- The line from the file is printed to the right of the file name which is separated by a colon ':'.

grep for the string 'User2' or 'open file' in 'windows_activity_logs.txt'. Use the '|' character,  that represents the logical OR to search the logs for either string.
![[Pasted image 20240327195614.png]]
The output of from grep displays all lines in log that contain contain either string or both strings.

grep for the string 'User1' and 'failed' in 'windows_activity_logs.txt' and append the result to 'log1.txt'. In order to grep for both strings grep for the first string and then pipe the result into grep searching for the second string. The result should be the output of searching for the first string refined by the search for the second string. That output will then be appended to 'log1.txt' using the characters '>>' and can be verified by using 'cat' to show the contents of that file. 
![[Pasted image 20240327201326.png]]

grep for the string 'User1' and 'failed' in both files starting with 'windows_activity_logs' and redirect the output to 'log2.txt'. In order to grep for both strings grep for the first string and then pipe the result into grep searching for the second string. The result should be the output of searching for the first string refined by the search for the second string. That output will then be redirected to 'log2.txt' using the characters '>' and can be verified by using 'cat' to show the contents of that file. The lines in the log file will begin with the name of the file the line was found in because multiple files were searched. 
![[Pasted image 20240327201722.png]]
![[Pasted image 20240327201805.png]]



