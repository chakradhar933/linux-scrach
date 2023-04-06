- 1 . How to create a file in linux ?
- ans: They are multiple ways to create a file but iam using to ways i.e.,

```bash
touch <file name> 
# To create empty files
cat > <filename>
# it will open the promt and give some information to that file.
```
- 2. How to delete zero files or empty files in linux ? 
- ans: To delete the zero files or empty files in linux we can use 'find' command with the "-size" option and -delete option.
```bash
find <path of the files> -size 0 delete
find /root/cat -size 0 -delete
find . -size 0 -delete
```
- 3. How to see the size of the file in linux?
- ans: You can see the size of the file by using command.
```bash
ls -l
ls -Al # to shown hidden files also
# du -sh <file name> this will give both file and directory.
du -sh dir name
```
- 4. How can i see 10 1st and last 10 lines of the code in linux ?
- ans : By using the command 
```bash
head -n 10 <file name>
tail -n 10 <file name>
```
- 5 . If their is a file "f1" having 50 lines are their i just want to print the line number 10 content . how can i find in linux ?
- ans : In this we are using the command
```bash
sed -n 'linenumberp' <file name>
sed -n '5p' f2
```
- 6. 