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

1. `'actionsToPerform'` </> <br> Anything that comes in single quotes is an action, all the actions should be listed in single
   unit separated by spaces. <br> Eg: `ls -l | awk '{print $9}' | awk -F "_" '/^java/ {print{$4}}'`
2. `'{print $0}'` <br> Print action is to print a column in a text. <br> $0 - complete line <br> $i - ith column (where i
   is an integer) <br> $NF - last column
3. `-F ":"` <br> You can specify a field separator this way. Default field separator is space. <br> Eg: `ps | awk -F "." '
   print{$1}'`
4. FilePath <br> File path can be included after action <br> Eg: `awk '{print $1 $2 $3}' filePath`
5. `uniq` <br> It filters out the duplicate lines. <br> Eg. `ls -l | awk '{print$9}' | awk -F "_" '/^java/ {print $4"abc"
   }' | uniq`
6. `sort` <br> To sort the output. <br> Eg: `ls -l | awk '{print$9}' | sort`
7. Simple Arithmetic <br> We can do (+, *, -, \/) on integer columns. <br> Eg: `df | awk '/\/dev\// {print $1 "\t" $3 +
   $4}'`
8. `length()` function <br> We can use conditions on length of line <br> Eg: `awk 'length($0) < 10' /etc/shells`
9. If condition <br> We can add if condition in the awk <br> Eg: `ps -ef | awk '{if($NF == "-bash") print $0}'`
10. For loop <br> We can add for loop in awk <br> Eg: `awk 'BEGIN { for(i=1;i<10;i++) print "square of ", i, "is", i*i}'`
11. Put matching on ith column <br> Eg: `ls -l | awk '$9 ~ /^[j]/ {print $0}'`
12. Match function <br> Match function is used to match something. <br> Eg: `ls -l | awk 'match($9, /p/) {print{0}}'`
13. Process only the range of lines <br> `ls -l | awk 'NR == 10, NR == 20 {print NR, $0}' <br> awk 'NR < 16' .bashrc`
14. Print number of lines in the file <br> `ls -l | awk 'END {print NR}'`

### grep command

#### Useful Concepts and Operations

<ol> <li> <details> <summary> How to grep using result of previous grep <br> Question. Grep the status codes for ids with xyz occurred event <br> Sample Input 
<pre><code> 
ID 1000 xyz occured 
ID 1001 misc content 
ID 1000 misc content 
ID 1000 status code: 26348931276572174 
ID 1000 misc content 
ID 1001 misc content 
ID 1001 xyz occured 
ID 1001 status code: 122312321 
ID 1002 xyz occured 
ID 1002 status code: 974783
 </code></pre> <br> Sample output 
<pre><code> 
ID 1000 status code: 26348931276572174 
ID 1001 status code: 122312321 
ID 1002 status code: 974783 
</code></pre> </summary> <p> Solution <br> for x in `grep 'xyz occured' xyz.txt | awk '{print $2}'`; do grep "$x status code" xyz.txt; done <br> <a href="https://stackoverflow.com/a/18179401/6744037">Reference</a> </p> </details>
</li>
</ol>

### SED Command (stream editor)

#### Uses

1. It is used for editing the file.
2. It supports find-replace, delete operations

#### Useful Concepts and Operations

1. basic structure of sed <br> `sed 's/string_to_be_replaced/new_string/'` <br> Eg: `echo "The Emac file manager is dired"
   \| sed 's/red/green'` <br> This command will replace only 1 occurance of *red* with *green*
2. `/g` <br> It tells the sed command to substitule all the occurances <br> Eg: `echo "Jungles are green" | sed 's/[a,g]
   /A/g'`
3. `-i` flag <br> This command is used to read the file and edit it <br> Eg: `sed -i 's/a/A/' filePath`
4. Trim trailing spaces <br> `sed -i 's/ *$//' filename`
5. Remove trailing tabs <br> `sed -i 's/[[:space:]]*$//' filename`
6. Remove empty lines <br> `sed 's/^$/d' filename`
7. Convert lower case letters to upper case <br> `sed -i 's/[a-z]/\U&/g' filename`
8. Convert upper case letters to lower case <br> `sed -i 's/[A-Z]/\L&/g' filename`

### WC command (word, line, character, and byte count)

#### Uses

1. `wc` <br> Displays number of lines, number of words and number of characters <br> eg: `echo "I am feeing awesome" | wc`
2. `wc -l` <br> Displays number of lines
3. `wc -w` <br> Displays number of words
4. `wc -c` <br> Displays number of characters

### HEAD (display first lines of a file)

#### Uses

1. `head -n` <br> displays specified number of lines from the file <br> Eg: `head -10`

### CUT (Divide a file into several parts or columns)

#### Important points

1. Cut treats Tabs and backspaces as a character
2. N the Nth field, byte or character, starting from 1.
3. N- from the Nth field, byte or character, to the end of the line. 
4. N-M from the Nth to the Mth field, byte, or character.
5. -M from the first to the Mth field, byte, or character

#### Uses

<ol>
 <li> 
   <code> cut -c startIndex-endIndex </code> <br>
   Displays the characters inclusive of startIndex and endIndex. Refer to important points for more details. <br>
   Eg: <code> echo "You are best" | cut -c 5- </code> <br> Output: are best <br>
   Eg: <code> echo "You are best" | cut -c -5 </code> <br> Output: You a <br>
   Eg: <code> echo "You are best" | cut -c 5-7 </code> <br> Output: are <br>
</li>
<li>
   <code> cut -c [a1,a2,a3...] </code> <br> 
   Displays the characters in the list. <br>
   Eg: <code> echo "You are best" | cut -c 2,5,7 </code> <br> Output: oae
</li>
<li>
   <code> cut -d "delimiter" -f (field number) file.txt </code> <br>
   cuts the line based on a delimiter <br>
   <b> Note: </b> cut uses tab as a default field delimiter but can also work with other delimiter by using -d option. <br>
   Eg: <code> echo "Y-o-u a-r-e b-e-s-t" | cut -d "-" -f 1 </code> <br> Output: Y <br>
   Eg: <code> echo "Y-o-u a-r-e b-e-s-t" | cut -d "-" -f 1,2,3 </code> <br> Output: Y-o-u a <br>
   Eg: <code> echo "Y-o-u a-r-e b-e-s-t" | cut -d "-" -f 2-5 </code> <br> Output: o-u a-r-e b <br>
</li>
</ol>

##### Credits :

1. [Geeksforgeeks: AWK command in Unix/Linux with examples](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)
2. [Man page: AWK](https://man7.org/linux/man-pages/man1/awk.1p.html)
3. [how search log files and extract data](https://www.sentinelone.com/blog/how-search-log-files-extract-data/)
4. [Youtube: Learning Awk Is Essential For Linux Users](https://www.youtube.com/watch?v=9YOZmI-zWok)
5. [GNU: All Awk functions](https://www.gnu.org/software/gawk/manual/html_node/Functions.html)
6. [Youtube: Learning Sed Is Beneficial For Linux Users](https://www.youtube.com/watch?v=EACe7aiGczw)
7. [Cut command documentation](https://ss64.com/bash/cut.html)
8. [GeekForGeeks: cut command](https://www.geeksforgeeks.org/cut-command-linux-examples/)
9. [Baeldung: Cut command](https://www.baeldung.com/linux/cut-command)
