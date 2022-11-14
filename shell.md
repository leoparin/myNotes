why?
图形化界面不是很方便批量处理文件，而且也有很多情况根本处理不了

# 1 file path
## absolute path
start with root slash
the others are separators
![[Screenshot 2022-11-14 at 16.04.03.png]]

## relative path
``` shell
ls -l scripts/my_script.sh
```

-   . ( single dot) denotes the current directory in the path.
-   .. (two dots) denotes the parent directory, i.e., one level above.


# 2 file system
Which file would be accessed by which user is decided by two factors in Linux:

-   File ownership
-   File permission
(the same for directory)
## 2.1 file ownership
three kinds of owner:`user group other`
又包含关系
other :super group contains all users（所有人都可以看或者写）
 ‘User’ is a single user, Group is a collection of users and Other consists of all the users on the system.

## 2.2 permissions in linux(chmod)
**Permissions for files**

-   Read – Can view or copy file contents
-   Write – Can modify file content
-   Execute – Can run the file (if its executable)

**Permissions for directories**

-   Read – Can list all files and copy the files from directory
-   Write – Can add or delete files into directory (needs execute permission as well)
-   Execute – Can enter the directory
``` zsh
ls -l
-rwxrw-r-- 1 abhi itsfoss 457 Aug 10 11:55 agatha.txt
```
![[Pasted image 20221028143333.png]]

-   **File type**: Denotes the type of file. d means directory, – means regular file, l means a [symbolic link](https://linuxhandbook.com/symbolic-link-linux/).
-   **Permissions**: This field shows the permission set on a file. I’ll explain it in detail in the next section.
-   **Hard link count**: Shows if the file has [hard links](https://linuxhandbook.com/hard-link/). Default count is one.
-   **User**: The user who owns the files.
-   **Group**: The group that has access to this file. Only one group can be the owner of a file at a time.
-   **File size**: Size of the file in bytes.
-   **Modification time**: The date and time the file was last modified.
-   **Filename**: Obviously, the name of the file or directory

### 2.2.1 permissions
`rwxrw-r--`
all three kind of owners (see the ownership section) in the order of User, Group and Other.

`Note: Root user has super powers and normally, it has read, write and execute permissions to all the files, even if you don’t see it in file permissions.`

## 2.3 change permissions
command: `chmod`
change mode of access
### 2.3.1 absolute mode
In the absolute mode, permissions are represented in numeric form (octal system to be precise). In this system, each file permission is represented by a number.
-   r (read) = 4
-   w (write) = 2
-   x (execute) = 1
-   – (no permission) = 0
 can combine them and thus one number can be used to represent the entire permission set.(chmod 777 why)

### 2.3.2 symbolic mode
absolute mode you should always provide three numbers(even u don't need to change come permissions)
-   u = user owner
-   g = group owner
-   o = other
-   a = all (user + group + other)

-   + for adding permissions
-   – for removing permissions
-   = for overriding existing permissions with new value
``` bash
chmod g+x agatha.txt
```

## 2.4 change file owner
``` bash
chown <new_user_name> <filename> //only change owner

chown <new_user_name>:<new_user_group> <filename>

```

## 2.5 symbolic link
``` bash
lrwxrwxrwx 1 abhishek abhishek 23 Jul  2 08:51 link_prog -> newdir/test_dir/prog.py
```

### 2.5.1 what? 
像windows的快捷方式一样
### 2.5.2 why?
That’s the whole purpose of the links after all. You access the target file by accessing the link. You can make changes to the target file through the links. Let’s see with example.
### 2.5.3 how？
``` bash
ln -s target_file link_name 
//-s means softlink, otherwise will create a hard link
```

## 2.6 hardlink
![[Pasted image 20221028152548.png]]
### 2.6.1 what?
hard link is a manually created entry in a directory that points to an already existing inode.(开一个新的分支)

### 2.6.2 why?


### 2.6.3 how?


# 3 find
```shell
# 4 find file name test in current dir
find . -type f -name test


```

# 5 CURL

```bash
//Post:
curl -d " data " http://localhost:5000/methods

//Put
curl -X " "
```

# 6 quotes
why?
white space is used for seperate commands, if the file name contains white space will cause error
## 6.1 single quotes
ignore all the special characters
```shell
echo '$SHELL'                                                   
$SHELL

echo $SHELL                                                 
/bin/zsh

echo "$SHELL"                                        
/bin/zsh
```

## 6.2 double quotes
also tend to ignore special character, except for `$ '' \`
``` shell
abhishek@its-foss:~$ var=My 'own villa' is yellow
own villa: command not found
abhishek@its-foss:~$ var="My 'own villa' is yellow"
abhishek@its-foss:~$ echo $var
My 'own villa' is yellow
```

double quotes and single quotes can be used to hide each other

## 6.3 back slash
Backslash is like putting single quotes around a single character. The backslash 'escapes' the character it is put before
``` shell
abhishek@its-foss:~$ var=variable
abhishek@its-foss:~$ echo \var
var
abhishek@its-foss:~$ echo $var
variable
abhishek@its-foss:~$ echo \$var
$var
```

use of the backslash character in continuing a single command over multiple lines.

## 6.4 back quote
The shell has this command substitution feature where a specified command is replaced with the output of the command.
``` shell
abhishek@its-foss:~$ echo The current date and time is `date`
The current date and time is Monday 23 August 2021 04:55:18 PM IST
```

For years, the back quotes were used for command substitution in Shell scripting. But these days, modern UNIX and Linux systems prefer the `$(command)` construct instead.

