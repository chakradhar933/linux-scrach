### Open the killerkoda Platform to practice the linux commands.
```
Other References: In this video we are learn linux commands.

Killercoda Platform : [https://killercoda.com/rkalluru](https://killercoda.com/rkalluru)
```

**Basic Linux commands**

* To connect the server either aws cloud or killercoda.

### Linux is a command line interface.

- [ ]  **uname** is a command in linux which is used to display the which operating system you are using.

```bash
uname
```

- **uname -a , uname —all :** it is a command is used to ****display the complete output**.**

```bash
uname -a
uname --all
```

- Lets say you joined in a an organisation and open the machine you will checkout what is this machine by using using we are using the command ****cat /etc/*release****
- it will be shown the complete information about your os.
- To check the vendor operating system in your organisation.

```bash
cat /etc/*release
```

- To check the cpu information

```bash
cat /proc/cpuinfo
```

- To check memory information.

```bash
cat /proc/meminfo
```

- To check the disk information.

```bash
lsblk
```

- To check the architecture weather it is 32bit or 64bit

```bash
uname -i
```

- List of all files and diretories

```bash
ls
```

- List of all hidden files.

```bash
ls -A
```

- To give more information about files and dirctories.

```bash
ls -l
```

- To create a empty files

```bash
touch <file name>
```

- To create a files with content and save the file ctrl+d

```bash
cat > <filename>
```

- To remove the files

```bash
rm -f <filename>
```

- To copy the one file to another file

```bash
cp <source file name> <destination file name>
```

- To move the files one file to another file (ex take f1 to f2 = f1 is overwrite to f2) f1 is removed.

```bash
mv <source file name> <destination file name>
```

### Theoretical Points

### Practical things the trainer did

- uname - This command is used to display the which os you are using.
- uname -a , uname -all - This command is use to display complete information about the os.
- cat /etc/*release - This command shown the vendor os.
- cat /proc/cpuinf - This command is used to display the cpu information.
- cat /proc/meminfo - This command is used to display the memory information
- lsblk - This command is used to check the disk information.
- uname -i - This command is used to shown bits of os (32bit or 64bit).
- ls - list of all files and dirctories.
- ls -A - To list of all hidden files.
- touch - to create an empty file
- cat > <file name> - To create a files with content.
- rm -f  <file name> - To remove the files
- cp <source file> <destination file> - To copy the files one file to another.
- mv <source file> <destination file> - To move the files one file to another file (its overwrite the previous file).