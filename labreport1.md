# Lab Report 1

# `cd`

**Example 1: no arguments** 
(working directory: `/home/lecture1`)
![](/labreport1_screenshots/cd_noarg.png)
- When `cd` is used with no arguments (there are no file or directory paths after the command), the current working directory is changed to the root directory. 
- In the given example, the `cd` command changes the working directory from `/home/lecture1` to `/home`. 
- This is not an error.

**Example 2: directory path as argument** 
(working directory: `/home`)
![](/labreport1_screenshots/cd_dirarg.png)
- When `cd` is used with a directory path as an argument, the current working directory is changed to the directory given as an argument. 
- In the given example, the `cd` command with the relative path `lecture1/` changes the current working directory from `/home` to `/home/lecture1`.
- This is not an error.

**Example 3: file path as argument** 
(working directory: `/home/lecture1`)
![](/labreport1_screenshots/cd_filearg.png)
- When `cd` is used with a file path as an argument, the current working directory does not change and the following message is printed: `bash: cd: [file path]: Not a directory`.
- In the given example, the `cd` command with the path `messages/en-us.txt` did not change the working directory (`/home/lecture1`) and printed the message `bash: cd: messages/en-us.txt: Not a directory`.
- **This is an error:** `cd` is used to change the current working directory, and so file paths cannot be used as arguments. 

# `ls`

**Example 1: no arguments** 
(working directory: `/home/lecture1`)
![](/labreport1_screenshots/ls_noarg.png)
- When `ls` is used with no arguments, a list of the current working directory's contents is printed to the output.
- In the given example, the `ls` command printed `Hello.class`, `Hello.java`, `messages`, and `README`. These are the contents of the `/home/lecture1` directory, which is the current working directory. 
- This is not an error. 

**Example 2: directory path as argument** 
(working directory: `/home/lecture1`)
![](/labreport1_screenshots/ls_dirarg.png)
- When `ls` is used with a directory path as an argument, a list of the contents of the directory provided as an argument is printed to the output.
- In the given example, the `ls` command with the relative path `messages/` as an argument printed `en-us.txt`, `es-mx.txt`, `fr.txt`, and `zh-cn.txt`. These files are the contents of the `messages/` directory.  
- This is not an error. 

**Example 3: file path as argument** 
(working directory: `/home/lecture1`)
![](/labreport1_screenshots/ls_filearg.png)
- When `ls` is used with a file path as an argument, the file path provided as an argument is printed to the output.
- In the given example, the `ls` command with the relative path `messages/en-us.txt` printed `messages/en-us.txt`.   
- This is not an error. 

# `cat`

**Example 1: no arguments** 
(working directory: `/home`)
![](/labreport1_screenshots/cat_noarg.png)
- When `cat` is used with no arguments, the terminal reads the user input and prints it until the command execution is halted.
- In the given example, the `cat` command printed back the user input, such as `j` and `hello`. The same behavior occured when directory paths like `lecture1/` and file paths like `lecture1/messages/en-us.txt` were written as inputs. The command execution stopped with the `^C` keyboard shortcut, which is used to halt execution. 
- This is not an error. 

**Example 2: directory path as argument** 
(working directory: `/home`)
![](/labreport1_screenshots/cat_dirarg.png)
- When `cat` is used with a directory path as an argument, the following message is printed: `cat: [directory path]: Is a directory`.
- In the given example, the `cat` command with the relative path `lecture1/` printed the message `cat: lecture1/: Is a directory`.
- **This is an error:** the `cat` command only takes no arguments or file path arguments, as it cannot read anything from a directory. 

**Example 3: file path as argument** 
(working directory: `/home`)
![](/labreport1_screenshots/cat_filearg.png)
- When `cat` is used with a file path as an argument, the contents of the file are printed to the output.
- In the given example, the `cat` command with the path `lecture1/messages/en-us.txt` prints `Hello World!`, which is the content of the `en-us.txt` file
- This is not an error. 