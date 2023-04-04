### important commands
- uname : This command is used to display the which operating system you are using
```bash
uname
```
- uname -a , uname -all : To display the complete output.
```bash
uname -a
uname -all
```
- cat /etc/*release : To check  the operating system details.
```bash
cat /etc/*release
```
- cat /proc/cpuinfo : To check the cpu information. 
```bash
cat /proc/cpuinfo
```
- cat /proc/meminfo : To check the memory information.
```bash
cat /proc/cpuinfo
```
- lsblk : To check the disk information.
```bash
lsblk
```
- uname -i : To check the archictecture whether it is 64bit or 32bit.
```bash
uname -i
```
- ls : To shown the list of all files and directories.
```bash
ls 
```
- ls -A : To list list of all hidden files.
```bash
ls -A
```
- ls -l : long list of all files and directories.
```bash
ls -l
```
- cat > "file name" : To create a file and add the content . 
# ctr+d to come out from the file
```bash
cat > f1
```
- touch <f1> <f2> : To create empty files.
```bash
touch f1 f1
```
- cp <source file> <destination> : To copy the file one file to another file.
```bash
cp f2 f1
```
- mv <source file> <destination file> : To move the file one file to another file . (overwrited)
```bash
mv f1 f2
```
- pwd : We want to know about which place or location we are present in .
```bash
pwd
```

- cd : To navigate one location to another location. 
```bash
cd
```
- cd .. :To go back to the one location.
```bash
cd ..
```
- cd ../.. : To go back mulitiple locations
```bash
cd ../..
```
- mkdir <name>: To create a diretory or folder.
```bash
mkdir <linux>
```
- cp -r <soucrce dir name> <destination dir name> : To copy the one directory to another directory .
```bash
cp -r l1 l2
```

- mv <source file name> < destination directory name> : To move the file to the directory.
```bash
mv f1 l1
```

- To move the one directory to another directory

```bash
mv f2 f1
```
- rm -r : To remove the directory.
```bash
rm -r f1 f2
```
- rm -rf  : To remove the directory forcefully
```bash
rm -rf <dir name>
```
- head : In a file having more numbers of lines to shown only 1st 5 lines
```bash
head -n 5 <filename>
```
- tail :If you want to have only last 5 lines.
```bash
tail -n 5 <filename>
```
-grep : The grep filter searches a file for a particular pattern of charcters, and display all lines that contain that platform
```bash
grep <word> <file name>
grep root /etc/passwd
```

-awk : In such cases the content needs to be filtered based on the columns in that awk command is used.
```bash
awk -F : '{print $column-number}' <file name>
awk -F : '{print $1 $2}' /etc/passwd
```
- and also cama seperated files
```bash
awk -F , '{print $cama-number}' <file name>
awk -F , '{print $1}' /etc/passwd
```
- vim  : editer is used to create a file and modify the files.
`vim file` -> Press `Insert` or `i` -> Make Changes -> Press `ESC` -> Press Colon `:` -> Press `wq` -> Done
```bash
vim <file name>
```



