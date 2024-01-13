# Lab Report 1: Using *cd*, *ls* and *cat*

# `cd`

**Example 1: no arguments**
working directory: `/home/lecture1`
![](/labreport1_screenshots/cd_noarg.png)
- When `cd` is used with no arguments (there are no file or directory paths after the command), the current working directory is changed to the root directory. 
- In the given example, the `cd` command changes the working directory from `/home/lecture1` to `/home`. 
- This is not an error.

**Example 2: directory path as argument**
working directory: `/home`
![](/labreport1_screenshots/cd_dirarg.png)
- When `cd` is used with a directory path as an argument, the current working directory is changed to the directory given as an argument. 
- In the given example, the `cd` command with the relative path `lecture1/` changes the current working directory from `/home` to `/home/lecture1`.
- This is not an error.

**Example 3: file path as argument**
working directory: `/home/lecture1`
![](/labreport1_screenshots/cd_filearg.png)
- When `cd` is used with a file path as an argument, the current working directory does not change and the following message is printed: `bash: cd: [file path]: Not a directory`.
- In the given example, the `cd` command with the path `messages/en-us.txt` did not change the working directory (`/home/lecture1`) and printed the message `bash: cd: messages/en-us.txt: Not a directory`.
- **This is an error:** `cd` is used to change the current working directory, and so file paths cannot be used as arguments. 

# `ls`

**Example 1: no arguments**
working directory: `/home/lecture1`
![](/labreport1_screenshots/ls_noarg.png)
- Prints a list of the current working directory's contents.
- Not an error. 

**Example 2: directory path as argument**
working directory: `/home/lecture1`
![](/labreport1_screenshots/ls_dirarg.png)
- Prints a list of the contents of the directory provided as an argument.
- Not an error. 

**Example 3: file path as argument**
working directory: `/home/lecture1`
![](/labreport1_screenshots/ls_filearg.png)
- Prints the file path provided as an argument. 
- Not an error. 

# `cat`

**Example 1: no arguments**
working directory: `/home`
![](/labreport1_screenshots/cat_noarg.png)
- Reads the user input and prints it.  
- Not an error. 

**Example 2: directory path as argument**
working directory: `/home`
![](/labreport1_screenshots/cat_dirarg.png)
- Prints the following message: `cat: [directory path]: Is a directory`
- **This is an error:** the `cat` command only takes no arguments or file path arguments, as it cannot read anything from a directory. 

**Example 3: file path as argument**
working directory: `/home`
![](/labreport1_screenshots/cat_filearg.png)
- Prints the contents of the file. 
- Not an error. 