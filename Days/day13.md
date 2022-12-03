On the thirteenth day, I learned the following things about Linux.

- `sudo` (super user do) will be used when some commands require administrative permission. If you want to access some files that require admin permission then you will use `sudo` to enter the password and give the permssion.
- `df` is used to find the disk storage capacity.
- `df -m` will show the data size in MBs.
- `df -mh` will show the data in MBs and in human readable format.
- `du` will estimate the disk space usage statistics.
- `du -h` will give the file usage space in human-readable format.
- `head` will print the first few lines of a file.
- `head -n 4 file-name` will print the first four lines of a file.
- `tail` will print the few lines from the bottom of a file.
- `diff` will compare content of the files line by line and see if there is any difference.
- `locate` will find the files by name.
- `find` search all the files present in a directory.
- `find . -type d` will only find the directories that are present in a current directory.
- `find . -type f` will only find the files that are present in a current directory.
- `find . -type f -name "file-name"` will only find the files that are present in a current directory and the name of the file is given.
- `-name` is case sensitive but if you don't want to use the case sensitive then use `-iname`.
- `mmin` (last modified n minutes ago) `find . -type f -mmin -20` will show only the files that are modified in a current directory less than 20 minutes ago.
- `find . -type f -mmin +15` will show only the files that are modified in a current directory more than 15 minutes ago.
- `find . -type f -mmin +2 -mmin -10` will show only the files that are modified in a current directory more than 2 minutes ago and less than 10 minutes ago.
- `find . -type f -mtime -10` will show only the files that are modified in a current directory less than 10 days ago.
- `find . -type f -maxdepth 1` will only show the files that are present in the first directory. It is not going recursively.
If you want to recursively search then make the maxdepth equal to 2, 3, and so on.
- `find . -size +1M` will find all the files that has a size more than 1 MB.
- `find . -empty` will find all the empty files.
- `find . -perm 777` will find the files that has 7(read), 7(write), and 7(execute) permission.


If you find the long detail of a file, the read, write and execute permissions have 3 hyphens. The first hyphen shows the user permission which has a value 4. The second hyphen shows the group permission which has value 2 and the third one shows the permission of all the other users and it has a value 1. `0` stands for no permission.

Let's say if a file has only read and write permission then it will be equal to 4+2=6.

You can change the permissions by writing
- `chmod u=rwx,g=rx,o=r file-name`

If I write `777`, it will assign read, write, and execute permission to every hyphen of a file. 
- `chmod 777 file-name`

If I write `577`, it will assign read, and execute permission to the first three hyphens and read, write and execute permission to the remaining hyphens of a file. 
- `chmod 577 file-name`

How to perform a functionality on many files?
Let's you want to find multiple files and delete them.

- `find . -type f -name "*.txt" -exec rm -rf {} +` will find and remove all the files. `{}` will contain a list of all the files.

- `whoami` will print the person username who is logged in.

**grep(global regular expression print)**

- `grep "text" filename` will find the text in a file and it is case-sensitive.

- `grep -w "text" filename` will find the complete word written in a file.

- `grep -i "text" filename` will find the text in a file even if it is not case-sensitive.

- `grep -n "text" filename` will find the text with a line number in a file.

- `grep -B 3 "text" filename` will find the lines that came before the given text.

- `grep -rwin "text" .` will find the text recursively in a current directory.

- `grep -wirl "text" .` will find all the files that contain the given text.

- `grep -wirc "text" .` will count the files that contain the given text.

- `history` will show the history of all the commands that has been used.

- `history | grep "ls"` will show history of all the **ls** command that are used.

- `grep -P "regular expression" filename` will find the specific text in a file by using regex.

## **Explaining it in a video**

Here you can get an explanation in a video. [13/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=eGC9j2u2uoA&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=12)