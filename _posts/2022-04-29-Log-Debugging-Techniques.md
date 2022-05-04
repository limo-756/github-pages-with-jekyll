---
title: "Log Debugging Techniques"
date: 2022-04-29
---

### AWK Command (pattern-directed scanning and processing language)
#### Uses
1. Scans a file line by line 
2. Splits each input line into fields 
3. Compares input line/fields to pattern 
4. Performs action(s) on matched lines 

#### Useful Concepts and Operations
1. 'actionsToPerform' <br> Anything that comes in single quotes is an action, all the actions should be listed in single unit separated by spaces. <br> Eg: ls -l \| awk '{print $9}' \| awk -F "_" '/^java/ {print{$4}}'
2. '{print $0}' <br> Print action is to print a column in a text. <br> $0 - complete line  $i - ith column (where i is an integer)  $NF - last column
3. -F ":" <br> You can specify a field seperator this way. Default field separator is space. <br> Eg: ps \| awk -F "." 'print{$1}'
4. FilePath <br> File path can be included after action <br> Eg: awk '{print $1 $2 $3}' filePath
5. uniq <br> It filter out the duplicate lines. <br> Eg. ls -l \| awk '{print$9}' \| awk -F "_" '/^java/ {print $4"abc"}' \| uniq
6. sort <br> To sort the output. <br> Eg: ls -l \| awk '{print$9}' \| sort
7. Simple Arithmetic <br> We can do (+, *, -, \/) on integer columns. <br> Eg: df \| awk '/\/dev\// {print $1 "\t" $3 + $4}'
8. length() function <br> We can use conditions on length of line <br> Eg: awk 'length($0) < 10' /etc/shells
9. If condition <br> We can add if condition in the awk <br> Eg: ps -ef \| awk '{if($NF == "-bash") print $0}'
10. For loop <br> We can add for loop in awk <br> Eg: awk 'BEGIN { for(i=1;i<10;i++) print "square of ", i, "is", i*i}'
11. Put matching on ith column <br> Eg: ls -l \| awk '$9 ~ /^[j]/ {print $0}'
12. Match function <br> Match function is used to match something. <br> Eg: ls -l \| awk 'match($9, /p/) {print{0}}'
13. Process only the number of lines <br> ls -l \| awk 'NR == 10, NR == 20 {print NR, $0}'
14. Print number of lines in the file <br> ls -l \| awk 'END {print NR}'

### SED Command (stream editor)

#### Uses
1. It is used for editing the file.
2. It supports find-replace, delete operations

#### Useful Concepts and Operations
1. basic structure of sed <br> sed 's/string_to_be_replaced/new_string/' <br> Eg: echo "The Emac file manager is dired" | sed 's/red/green' <br> This command will replace only 1 occurance of *red* with *green*
2. /g <br> It tells the sed command to substitule all the occurances <br> Eg: echo "Jungles are green" | sed 's/[a,g]/A/g'
3. -i flag <br> This command is used to read the file and edit it <br> Eg: sed 's/a/A/' filePath

##### Credits :  
1. [Geeksforgeeks: AWK command in Unix/Linux with examples](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)
2. [Man page: AWK](https://man7.org/linux/man-pages/man1/awk.1p.html)
3. [how search log files and extract data](https://www.sentinelone.com/blog/how-search-log-files-extract-data/)
4. [Youtube: Learning Awk Is Essential For Linux Users](https://www.youtube.com/watch?v=9YOZmI-zWok)
5. [GNU: All Awk functions](https://www.gnu.org/software/gawk/manual/html_node/Functions.html)
6. [Youtube: Learning Sed Is Beneficial For Linux Users](https://www.youtube.com/watch?v=EACe7aiGczw)

