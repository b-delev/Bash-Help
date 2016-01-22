# Bash-Help

## Short manual for working with bash

```bash
// Shortcuts
CTRL L = Clear the terminal
CTRL D = Logout
SHIFT Page Up/Down = Go up/down the terminal
CTRL A = Cursor to start of line
CTRL E = Cursor the end of line
CTRL U = Delete left of the cursor 
CTRL K = Delete right of the cursor
CTRL W = Delete word on the left
CTRL Y = Paste (after CTRL U,K or W)
TAB = auto completion of file or command 
CTRL R = reverse search history
!! = repeat last command
CTRL Z = stops the current command (resume with fg in foreground or bg in background)
```

##Navigation

```bash
ls -a = list all files and folders
ls <folderName> = list files in folder
ls -lh = Detailed list, Human readable
ls -l *.jpg = list jpeg files only
ls -lh <fileName> = Result for file only

cd <folderName> = change directory - if folder name has spaces use “ “
cd / = go to root
cd .. = go up one folder, tip: ../../../ 

du -h: Disk usage of folders, human readable 
du -ah: “ “ “ files & folders, Human readable
du -sh: only show disc usage of folders

pwd = print working directory

man <command> = shows manual (RTFM) 

cat <fileName> = show content of file || use less <fileName> or more <fileName>

tail -- display the last part of a file 
tail -f <fileName> = Very useful for tracking log file in real time.

// Create directory
mkdir = create new folder
mkdir myStuff ..
mkdir myStuff/pictures/ ..

// Coping file and folders
cp image.jpg newimage.jpg = copy and rename a file
cp image.jpg <folderName>/ = copy to folder
cp image.jpg folder/sameImageNewName.jpg
cp -R stuff otherStuff = copy and rename a folder
cp *.txt stuff/ = copy all of *<file type> to folder

//Moving files and folders
mv file.txt Documents/ = move file to a folder
mv <folderName> <folderName2> = move folder in folder
mv filename.txt filename2.txt = rename file
mv <fileName> stuff/newfileName
mv <folderName>/ .. = move folder up in hierarchy 


// Delete files and directories
rm <fileName> .. = delete file (s)
rm -i <fileName> .. = ask for confirmation each file
rm -f <fileName> = force deletion of a file
rm -r <foldername>/ = delete folder -r means Recursively

// Create file
touch <fileName> = create or update a file

// Linking files
ln file1 file2 = physical link <sourceFile> <targetFile>
ln -s file1 file2 = symbolic link <sourceFile> <targetFile>

```

##Searching

```bash
sudo updatedb = update database of files
locate <text> = search the content of all the files 
locate <fileName> = search for a file

find = the best file search tool (fast)
find -name “<fileName>”
find -name “text” = search for files who start with the word text 

```


## Extract, Sort, Filter data

```bash

// Extract
grep <someText> <fileName> = search for text in file
	-i = Doesn't consider uppercase words
	-I = exclude binary files

// Sort 
sort = sort the content of files
sort <fileName> = sort alphabetically
sort -o <file> <outputFile> = write result to a file
sort -r <fileName> = sort in reverse
sort -R <fileName> = sort randomly
sort -n <fileName> = sort numbers

wc = word count
```


## Time settings


```bash
date = view & modify time (on your computer)

// Modify
date MMDDhhmmYYYY
sudo date 031423421997 = March 14th 1997, 23:42
```

## Execute command at another time

```bash
at now +5 minutes (hours, days, weeks, months, years)
<command> enter
<another command> enter
CTRL+D 

atq = show a list of jobs waiting to be executed
atrm 42  -  delete a job 42
```

```bash
crontab = execute a command regularly 
	-e = modify the crontab
	-l = view current crontab
	-r = delete you crontab

<Minutes> <Hours> <Day of month> <Day of week (0-6,0 = Sunday)> <COMMAND>

// Example:
47 15 * * * touch /home/bob/movies.txt * * * * * --> every minute
//create the file movies.txt every day at 15:47

//Execute program in the background add & at the end
cp bigMovieFile.mp4 &

jobs = know what is running in the background
fg = put a background process to foreground
example: fg (process 1)
```

## Process Management 

```bash
w = who is logged on and what they are doing

tload = graphic representation of system load average
(quit with CTRL C)

ps = Static process list 
	-ef --> ex: ps -ef | less
	-ejH --> show process hierarchy
	-u --> process's from current user

top = Dynamic process list
	in top
		q to close top
		h to show the help
		k to kill a process
(quit with CTRL C)


// Kill application
ps -u <AccountName> | grep <Application> - find PID of the application
kill <PID> - Kill the application based on a PID
kill -9 <PID> = violent kill 
killall = kill multiple process's
killall locate

sudo halt <-- to close computer
sudo reboot <-- to reboot
```

## User Accounts

```bash
sudo adduser bob = root creates new user
sudo passwd <AccountName> = change a user's password
sudo deluser <AccountName> = delete an account

addgroup friends = create a new user group
delgroup friends = delete a user group

usermod -g friends <Account> = add user to a group
usermod -g bob boby = change account name
usermod -aG friends bob = add groups to a user without loosing the ones he's already in
```

Execute programm or script as another user
edit visudo

```bash
sudo visudo

user1 ALL=(user2) NOPASSWD: /home/user2/script.sh
```



## File Permissions

```bash
chown = change the owner of a file

chown user:bob report.txt = changes the user owning report.txt to 'user' and the group owning it to 'bob'
	-R = recursively affect all the sub folders
	// chown -R bob:bob /home/Daniel 

chmod = modify user access/permission – simple way
	u = user
	g = group
	o = other

	d = directory (if element is a directory) 
	l = link (if element is a file link)

	r = read (read permissions)
	w = write (write permissions)
	x = eXecute (only useful for scripts and programs)

	'+' means add a right 
	'-' means delete a right
	'=' means affect a right 

	// Syntax: 
	chmod guo+rwx <fileName>
```

## Flow redirection
```bash
'>' at the end of a command to redirect the result to a file

'>>' to redirect the result to the end of a file
```

## Chain Commands
```bash
'|' at the end of a command to enter another one

la -la | grep <fileName>
```

## Archive and Compress data
```bash

// to compress
tar -cvf my_archive.tar folder/
	-c : creates a .tar archive
	-v : tells you what is happening (verbose)
	-f : assembles the archive into one file
gzip my_archive.tar

	to decompress: gunzip my_archive.tar.gz

bzip2 my_archive.tar

	to decompress: bunzip2 my_archive.tar.bz2


// decompress the .tar file:
tar -xvf archive.tar archive.tar


// Fast way 
gzip: tar -zcvf my_archive.tar.gz folder/
decompress: tar -zcvf my_archive.tar.gz Documents/ 

bzip2: tar -jcvf my_archive.tar.gz folder/
decompress: tar -jxvf archive.tar.bz2 Documents/

// Show the content of .tar, .gz or .bz2 without decompressing it:

// gzip: 
gzip -ztf archive.tar.gz

// bzip2:
bzip2 -jtf archive.tar.bz2

// tar
tar -tf archive.tar

tar -rvf archive.tar file.txt = add a file to the .tar

// use gzip to compress a file
gzip numbers.txt

// view the file without decompressing it
zcat = view the entire file in the console (same as cat)
zmore = view one screen at a time the content of the file (same as more)
zless = view one line of the file at a time (same as less)
```

## Instaling Software
```bash
sudo apt-get install <nameOfSoftware>
```

// If you have source code

// Decompress the file in a directory. If you have INSTALL, read the instructions

	• execute ./configure <-- creates a makefile

	• run make <-- builds application binaries

	• switch to root --> su
	
	• make install <-- installs the software


## Bash Programming

```bash
// Finds where bash binary is
which bash
```

Start every bash script with
```bash
#!/bin/bash
# the rest of the script ....
```

Every script after creation should be make executable
```bash
$ chmod +x bash_script.sh
./bash_script.sh
```

Decalring variable
```bash
#!/bin/bash
VAR="TEST"
echo $VAR
```

Local and Global Variables
```bash
#!/bin/bash
VAR="GLOBAL"
function func { // The space between the name of the function and the opening parenthesis is important
	local VAR="LOCAL"
	echo $VAR
}

echo $VAR
func()
```

Arguments passing to a bash script
```bash
#!/bin/bash

echo $1 // This is the first argument passed to the script
echo $2 // This is the second argument passed to the script
echo $3 // This is the third argument passed to the script
...

// You can assing all the arguiments to an array
args=("$@")

// And than use the arguments
echo ${args[0]}
echo ${args[1]}
echo ${args[2]}

// This will print all the arguments
echo $@

// Or you can print the number of the arguments passed
echo $#;
```

Executing bash commands from a bash script
```bash
echo `list -lA` // with backticks
echo list -lA // without backticks
```

Reading input from the user
```bash
#!/bin/bash

echo "Please, type a command: \c " 
read word
echo $word

// The other way is by reading the input and store it into build-in variable $REPLY
read 
echo $REPLY;
```

Bash Trap Command - used to prevent user to cancel script execution with Ctrl+C
```bash
#!/bin/bash
trap bashtrap INT

clear;

# bash trap function is executed when CTRL-C is pressed:
bashtrap()
{
    echo "CTRL+C Detected !...executing bash trap !"
}

# for loop from 1/10 to 10/10
for a in `seq 1 10`; do
    echo "$a/10 to Exit." 
    sleep 1;
done
echo "Exit Bash Trap Example!!!" 
```

Arrays
Declare array
```bash
#!/bin/bash

ARRAY=( 'Debian Linux' 'Redhat Linux' Ubuntu Linux )

ELEMENTS=${#ARRAY[@]}

for (( i=0;i<$ELEMENTS;i++)); do
    echo ${ARRAY[${i}]}
done 

```

Read file into bash Array
```bash
#!/bin/bash
declare -a ARRAY

# Link filedescriptor 10 with stdin
exec 10<&0

exec < $1
let count=0

while read LINE; do

    ARRAY[$count]=$LINE
    ((count++))
done

echo Number of elements: ${#ARRAY[@]}
echo ${ARRAY[@]}
exec 0<&10 10<&-
```

Bash if/else
```bash
#!/bin/bash

directory="./BashDirectory"

if [ -d $directory ]; then
	echo "Directory exists"
else 
	echo "Directory does not exists"
fi 
```

Nested if/else
```bash
#!/bin/bash

directory="./BashDirectory"

if [ -d $directory ]; then
	echo "Directory exists"
	if [ $choice -eq 2 ] ; then
		echo "You have chosen word: Scripting"
    else
		echo "You have chosen word: Bash"
    fi
else
	echo "Directory does not exists"
fi
```

Arithmetic Comparisons

-lt	<
-gt	>
-le	<=
-ge	>=
-eq	==
-ne	!=

```bash
#!/bin/bash
NUM1=2
NUM2=2

if   [ $NUM1 -eq $NUM2 ]; then
	echo "Both Values are equal"
elif [ $NUM1 -gt $NUM2 ]; then
	echo "NUM1 is greater then NUM2"
else 
	echo "NUM2 is greater then NUM1"
fi 

```

String Comparisons
=		equal
!=		not equal
<		less then
>		greater then
-n s1	string s1 is not empty
-z s1	string s1 is empty

```bash
#!/bin/bash

```

Bash File Testing

-b filename	Block special file
-c filename	Special character file
-d directoryname	Check for directory existence
-e filename	Check for file existence
-f filename	Check for regular file existence not a directory
-G filename	Check if file exists and is owned by effective group ID.
-g filename	true if file exists and is set-group-id.
-k filename	Sticky bit
-L filename	Symbolic link
-O filename	True if file exists and is owned by the effective user id.
-r filename	Check if file is a readable
-S filename	Check if file is socket
-s filename	Check if file is nonzero size
-u filename	Check if file set-ser-id bit is set
-w filename	Check if file is writable
-x filename	Check if file is executable

```bash
#!/bin/bash
file="./file"
if [ -e $file ]; then
	echo "File exists"
else 
	echo "File does not exists"
fi 
```

Bash FOR loop
```bash
#!/bin/bash
for f in $( ls /var/ ); do
	echo $f
done 
```

Bash WHILE loop
```bash
#!/bin/bash
COUNT=6

while [ $COUNT -gt 0 ]; do
	echo Value of count is: $COUNT
	let COUNT=COUNT-1
done 
```

Bash UNTIL loop
```bash
#!/bin/bash
COUNT=0

until [ $COUNT -gt 5 ]; do
        echo Value of count is: $COUNT
        let COUNT=COUNT+1
done 
```

Control bash loop with
```bash
#!/bin/bash

```

Bash Functions
```bash
#!/bin/bash

function func {
    echo $1
}

func "Echo func with 1 parameter"

```

Bash Select
```bash
#!/bin/bash

PS3='Choose one word: ' 

# bash select
select word in "linux" "bash" "scripting" "tutorial" 
do
  echo "The word you have selected is: $word"
# Break, otherwise endless loop
  break  
done

exit 0 

```

Case statement conditional
```bash
#!/bin/bash

echo "What is your preferred programming / scripting language"
echo "1) bash"
echo "2) perl"
echo "3) phyton"
echo "4) c++"
echo "5) I do not know !"
read case;

case $case in
    1) echo "You selected bash";;
    2) echo "You selected perl";;
    3) echo "You selected phyton";;
    4) echo "You selected c++";;
    5) exit
esac 

```

Escaping Meta characters
```bash
#!/bin/bash

BASH_VAR="Bash Script"

echo $BASH_VAR

echo \$BASH_VAR

```

Single quotes
```bash
#!/bin/bash

BASH_VAR="Bash Script"

// single quotes eliminates the special characters 
echo '$BASH_VAR  "$BASH_VAR"' 
```

Double Quotes
```bash
#!/bin/bash

// Double quotes in bash will suppress special meaning of every meta characters except "$", "\" and "`". 

BASH_VAR="Bash Script"

echo "It's $BASH_VAR  and \"$BASH_VAR\" using backticks: `date`" 

```

Bash quoting with ANSI-C style

\a	alert (bell)	
\b	backspace
\e	an escape character	
\f	form feed
\n	newline	
\r	carriage return
\t	horizontal tab	
\v	vertical tab
\\	backslash	
\`	single quote
\nnn	octal value of characters ( see [http://www.asciitable.com/ ASCII table] )	
\xnn	hexadecimal value of characters ( see [http://www.asciitable.com/ ASCII table] )

```bash
#!/bin/bash

echo $'web: www.linuxconfig.org\nemail: web\x40linuxconfig\56org' 

```

Bash Addition Calculator Example
```bash
#!/bin/bash

let RESULT1=$1+$2
echo $1+$2=$RESULT1 ' -> # let RESULT1=$1+$2'
declare -i RESULT2
RESULT2=$1+$2
echo $1+$2=$RESULT2 ' -> # declare -i RESULT2; RESULT2=$1+$2'
echo $1+$2=$(($1 + $2)) ' -> # $(($1 + $2))' 

```

Bash Arithmetics
```bash
#!/bin/bash


echo '### let ###'
# bash addition
let ADDITION=3+5
echo "3 + 5 =" $ADDITION

# bash subtraction
let SUBTRACTION=7-8
echo "7 - 8 =" $SUBTRACTION 

# bash multiplication
let MULTIPLICATION=5*8
echo "5 * 8 =" $MULTIPLICATION

# bash division
let DIVISION=4/2
echo "4 / 2 =" $DIVISION

# bash modulus
let MODULUS=9%4
echo "9 % 4 =" $MODULUS

# bash power of two
let POWEROFTWO=2**2
echo "2 ^ 2 =" $POWEROFTWO


echo '### Bash Arithmetic Expansion ###'
# There are two formats for arithmetic expansion: $[ expression ] 
# and $(( expression #)) its your choice which you use

echo 4 + 5 = $((4 + 5))
echo 7 - 7 = $[ 7 - 7 ]
echo 4 x 6 = $((3 * 2))
echo 6 / 3 = $((6 / 3))
echo 8 % 7 = $((8 % 7))
echo 2 ^ 8 = $[ 2 ** 8 ]


echo '### Declare ###'

echo -e "Please enter two numbers \c"
# read user input
read num1 num2
declare -i result
result=$num1+$num2
echo "Result is:$result "

# bash convert binary number 10001
result=2#10001
echo $result

# bash convert octal number 16
result=8#16
echo $result

# bash convert hex number 0xE6A
result=16#E6A
echo $result 

```

Round floating point number
```bash
#!/bin/bash

floating_point_number=3.3446
echo $floating_point_number
# round floating point number with bash
for bash_rounded_number in $(printf %.0f $floating_point_number); do
echo "Rounded number with bash:" $bash_rounded_number
done 

```

Bash floating point calculations
```bash
#!/bin/bash

# Simple linux bash calculator 
echo "Enter input:" 
read userinput
echo "Result with 2 digits after decimal point:"
echo "scale=2; ${userinput}" | bc 
echo "Result with 10 digits after decimal point:"
echo "scale=10; ${userinput}" | bc 
echo "Result as rounded integer:"
echo $userinput | bc 

```


## Redirections

STDOUT from bash script to STDERR
```bash
#!/bin/bash

echo "Redirect this STDOUT to STDERR" 1>&2 

```

STDERR from bash script to STDOUT
```bash
#!/bin/bash

cat $1 2>&1 

```

stdout to screen
```bash
#!/bin/bash

$ touch file1
$ ls file1 
file1

```

stdout to file
```bash
#!/bin/bash

$ ls file1 > STDOUT
$ cat STDOUT 
file1

```

stderr to file
```bash
#!/bin/bash

// By default STDERR is displayed on the screen:

$ ls
file1  STDOUT
$ ls file2
ls: cannot access file2: No such file or directory


// This example will demonstrate recording the error to a file

$ ls
file1  STDOUT
$ ls file1 file2 2> STDERR
file1
$ cat STDERR 
ls: cannot access file2: No such file or directory

```

stdout to stderr
```bash
#!/bin/bash

$ ls
file1  STDERR  STDOUT
$ ls file1 file2 2> STDERR_STDOUT 1>&2
$ cat STDERR_STDOUT
ls: cannot access file2: No such file or directory
file1

```

stderr to stdout
```bash
#!/bin/bash

$ ls
file1  STDERR  STDOUT
$ ls file1 file2 > STDERR_STDOUT 2>&1
$ cat STDERR_STDOUT 
ls: cannot access file2: No such file or directory
file1

```

stderr and stdout to file
```bash
#!/bin/bash

$ ls
file1  STDERR  STDOUT
$ ls file1 file2 &> STDERR_STDOUT
$ cat STDERR_STDOUT 
ls: cannot access file2: No such file or directory
file1

// Or 

ls file1 file2 >& STDERR_STDOUT
$ cat STDERR_STDOUT 
ls: cannot access file2: No such file or directory
file1

```





