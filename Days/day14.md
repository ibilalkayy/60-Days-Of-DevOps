On the forteenth day, I learned the following things about Linux.

- In Linux, an alias is **a shortcut that references a command.**
Aliases are mostly used to replace long commands, improving efficiency and avoiding potential spelling errors.

- `alias` will show you all the aliases that are generated.

- `alias <key>="<value>"` will make a new alias and after that, if you type a key, a functionality according to a value will be performed.

- `unalias <key>` will remove an alias from the memory and after that, the key will not be functional.

**Q. What if you want to create multiple aliases at once?**

**A.** You can store them in a file.

- `nano ~/.zshrc` will open up a *zsh* file in which you can store the aliases.

- `alias <key>="<value>"` is the format of giving an alias to a file.

- `source ~/.zshrc` will activate the alias that you saved in a file. Without activation you can't execute the alias.

**Note:** The same pattern will be applied to the bash terminal also. You just need to write `~/.bashrc` instead of `~/.zshrc`.

- `Ctrl+A` will move you to the first point of the command.
- `Ctrl+E` will move you to the end point of the command.
- `Ctrl+U` will delete everything that you entered.
- `Ctrl+K` will delete the command from the back of the cursor.
- `Ctrl+R` will search for the previous command.
- `TAB button` will auto complete the command without writing it as a whole.
- `!<number>` will take a number from the history and run it to access that command.
- `!<command>` will take a command from the history that was used last time and run it to access that command.
- `;` will help you to add multiple commands in one line.
- `sort file-name` will sort the data in an alphabetical order.
- `sort -r file-name` is the reverse of the sort.
- `sort -n file-name` will return the data in a numerical order.
- `jobs` will display all the current processes that are running.
- `ping website` will display all the data packets from a particular server.
- `wget <URL>` will download files from the internet. 
- `wget -O file-name <URL>` will save the downloaded file under a different name.
- `top` will show that how many processes are running and how much CPU usage is consuming?
- `kill process ID` will close the process.
- `uname` will display the kernel name.
- `uname -o` will print the operating system.
- `uname -m` will print the architecture.
- `uname -v` will print the kernel version.
- `cat /etc/os-release` will give the information of your operating system.
- `lscpu` will give you the CPU details.
- `free` will show you the free memory.
- `vmstat` will display the virtual memory state.
- `id` will print the IDs, group ids and stuff. 
- `getent group username` will look up the user details on Linux.
- `zip zip-file.zip text-file.txt` will zip the *text-file.txt* into *zip-file.txt*.
- `unzip zip-file.zip` will unzip the file.
- `hostname` will show the hostname.
- `hostname -i` will show the ip-address.
- `useradd username` will add a new user.
- `passwd username` will give a password to the user.
- `userdel username` will delete a username.
- `lsof` will list all the open files.
- `lsof -u username` will list the files that are opened by a username.

- `nslookup website` will give the ip-address of a website.
- `netstat` will give the details of all the active ports. 
- `ps aux` will give a snapshot of the current processes.
- `cut -c 1-2 file-name` will remove sections from each line of files.
- `ping website1 & ping website2` **"&"** operator will fetch multiple sites data.
- `echo "first" && echo "second"` **"&&"** operator will say if the first command is executed then execute the second command.
- `echo "hey" && {echo "hi"; echo "I am good"}` will say that if the first echo is executed then execute the commands in curly braces.
- `echo "first" || echo "second"` **"||"** operator will say if the first command is not executed then execute the second one.
- `| (pipe)` will send the output from the first command to the second command.

## **Explaining it in a video**

Here you can get an explanation in a video. [14/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=MIQtL_Hnupg&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=13)