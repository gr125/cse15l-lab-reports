# Lab Report 1: Using *cd*, *ls* and *cat*

# *cd*

**Example 1: no arguments**
working directory: /home/lecture1/
![](/labreport1_screenshots/cd_noarg.png)
- The current working directory is changed to the root directory. 
- Not an error.

**Example 2: directory path as argument**
working directory: /home/
![](/labreport1_screenshots/cd_dirarg.png)
- The current working directory is changed to the directory given as an argument. 
- Not an error.

**Example 3: file path as argument**
working directory: /home/lecture1/
![](/labreport1_screenshots/cd_filearg.png)
- The current working directory does not change, and the following message is printed: "bash: cd: [file path]: Not a directory"
- This is an error; *cd* is used to change directories, and so file paths cannot be used as arguments. 

# *ls*

**Example 1: no arguments**
working directory: /home/lecture1/
![](/labreport1_screenshots/ls_noarg.png)
- Prints a list of the current working directory's contents.
- Not an error. 

**Example 2: directory path as argument**
working directory: /home/lecture1/
![](/labreport1_screenshots/ls_dirarg.png)
- Prints a list of the contents of the directory provided as an argument.
- Not an error. 

**Example 3: file path as argument**
working directory: /home/lecture1/
![](/labreport1_screenshots/ls_filearg.png)
- Prints the file path provided as an argument. 
- Not an error. 

# *cat*

**Example 1: no arguments**
working directory: /home/
![](/labreport1_screenshots/cat_noarg.png)
- Reads the user input and prints it.  
- Not an error. 

**Example 2: directory path as argument**
working directory: /home/
![](/labreport1_screenshots/cat_dirarg.png)
- Prints the following message: "cat: [directory path]: Is a directory"
- This is an error: the *cat* command only takes no arguments or file path arguments, as it cannot read anything from a directory. 

**Example 3: file path as argument**
working directory: /home/
![](/labreport1_screenshots/cat_filearg.png)
- Prints the contents of the file. 
- Not an error. 