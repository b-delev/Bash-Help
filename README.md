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

Searching

```bash
sudo updatedb = update database of files
locate <text> = search the content of all the files 
locate <fileName> = search for a file

find = the best file search tool (fast)
find -name “<fileName>”
find -name “text” = search for files who start with the word text 

```



