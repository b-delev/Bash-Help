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
sudo apt-get install <nameOfSoftware>

// If you have source code

// Decompress the file in a directory. If you have INSTALL, read the instructions
	- execute ./configure <-- creates a makefile
	- run make <-- builds application binaries
	- switch to root --> su
	- make install <-- installs the software
