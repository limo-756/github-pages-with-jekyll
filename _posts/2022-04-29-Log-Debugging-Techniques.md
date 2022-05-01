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

#### Useful Concepts
1. 'actionsToPerform' - Anything that comes in single quotes is an action, all the actions should be listed in singlw unit separated by spaces.  Eg: ls -l \| awk '{print $9}' \| awk -F "_" '/^java/ {print{$4}}'
2. '{print $0}' - Print action is to print a column in a text.  $0 - complete line  $i - ith column (where i is an integer)  $NF - last column
3. -F ":" - You can specify a field seperator this way. Default field separator is space.  Eg: ps \| awk -F "." 'print{$1}'
4. FilePath - File path can be included after action.  Eg: awk '{print $1 $2 $3}' filePath
5. uniq - It filter put the duplicate lines.  Eg. ls -l \| awk '{print$9}' \| awk -F "_" '/^java/ {print $4"abc"}' \| uniq
6. sort - To sort the output. Eg: ls -l \| awk '{print$9}' \| sort
7. Simple Arithmetic - We can do (+, *, -, \/) on integer columns.  Eg: df | awk '/\/dev\// {print $1 "\t" $3 + $4}'
8. length() function - We can use conditions on length of line.  Eg: awk 'length($0) < 10' /etc/shells
9. If condition - We can add if condition in the awk.  Eg: ps -ef \| awk '{if($NF == "-bash") print $0}'

##### Credits :  
1. [Geeksforgeeks: AWK command in Unix/Linux with examples](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)
2. [Man page: AWK](https://man7.org/linux/man-pages/man1/awk.1p.html)
3. [how search log files and extract data](https://www.sentinelone.com/blog/how-search-log-files-extract-data/)
4. [Youtube: Learning Awk Is Essential For Linux Users](https://www.youtube.com/watch?v=9YOZmI-zWok)
