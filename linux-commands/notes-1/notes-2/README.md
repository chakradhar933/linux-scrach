Continous with linux commands

### Theoretical Points

- We want to know about which place or location we are present in

```bash
pwd
```

- To navigate one location to another location

```bash
cd
```

- To go back to the one location

```bash
cd ..
```

- To go back mulitiple locations

```bash
cd ../..
```

**Creating a directories**

- To create a diretory.

```bash
mkdir <name>
```

- To copy the one directory to another directory .

```bash
cp -r <source dir name > <destination dir name>
```

- To move the file to the directory

```bash
mv <source file name> < destination directory name>
```

- To move the one directory to another directory

```bash
mv <source directory> <destination dir>
```

- To remove the directory

```bash
rm -r <dir name>
```

- To remove the directory forcefully

```bash
rm -rf <dir name>
```

- In a file having more numbers of lines to shown only 5 lines

```bash
head -n 5 <filename>
```

- If you want to have only one line

```bash
tail -n 1 <filename>
```

- The grep filter searches a file for a particular pattern of charcters, and display all lines that contain that platform

```bash
grep <word> <file name>
grep root /etc/passwd
```

- In such cases the content needs to be filtered based on the columns in that awk command is used.

```bash
awk -F : '{print $column-number}' <file name>
awk -F : '{print $1 $2}' /etc/passwd

```

- and also cama seperated files

```bash
awk -F , '{print $cama-number}' <file name>
awk -F , '{print $1}' /etc/passwd
```

### Linux editors

We can edit the file by and save the changes by following instructions.

`vim file` -> Press `Insert` or `i` -> Make Changes -> Press `ESC` -> Press Colon `:` -> Press `wq` -> Done

We can come out of file without saving the changes

`vim file` -> Press `Insert` or `i` -> Make Changes -> Press `ESC` -> Press Colon `:` -> Press `q!`

- vim editer is used to create a file and modify the files

```bash
vim <file name>
```

### Things that I do need to perform