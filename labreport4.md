# Lab Report 4

## 1: Log into `ieng6` 
Keys pressed: `ssh<space>grenjith<shift>2ieng6-201.ucsd.edu<enter>`
- I typed out the `ssh user@ieng6.ucsd.edu` command replacing user with my UCSD username and then and connected to `ieng6` by pressing the enter key.
![](/labreport4_screenshots/step1.png) 
^At end of step 

## 2: Clone your fork of the repository from your Github account (using the SSH URL) 
Keys pressed: `git<space>clone<space><command>v<enter>` 
- I typed out the `git clone` command with the SSH key to my fork of the `lab7` repository that I copy-pasted from the GitHub website. 
![](/labreport4_screenshots/step2.png) 
^At end of step 

## 3: Run the tests, demonstrating that they fail 
Keys pressed: `cd<space>l<tab><enter>`, `bash<space>t<tab><enter>`
- I typed out the `cd` command, and after typing the first letter `l` of the `lab7` directory, pressing `<tab>` autocompletes the directory path. I then pressed `<enter>` to run the command. 
- I typed out the `bash` command and typed out the first letter `t` of the `test.sh` file; pressing `tab` then autocompletes the file name, and then I ran the command by pressing `<enter>`.
![](/labreport4_screenshots/step3.png) 
^At end of step 

## 4: Edit the code file to fix the failing test 
Keys pressed: `vim<space><shift>l<tab>.<tab><enter>`, `/cha<enter>`, `jllxi2<esc>`, `<shift>;wq<enter>` 
- I ran the `vim` command to edit the `ListExamples.java` file (typing 'L' and pressing `<tab>` and then pressing '.' and then `<tab>` autocompleted the file name). 
- I then found the comment indicating the line to change by pressing `/` and then typing `cha` and pressing enter, effectively searching for the first occurence of the text string `cha` which was the comment. 
- I then navigated to the exact position to change by pressing `jj` (equivalent to down twice). I pressed `x` to delete the next character `1`. I then entered insert mode by pressing `i` and typed `2` to fix the test. I pressed `<esc>` to exit insert mode. 
- I saved the file and exited by typing `:wq` and pressing `<enter>`. 
![](/labreport4_screenshots/step4-1.png) 
^After running `vim ListExamples.java` 
![](/labreport4_screenshots/step4-2.png) 
^After editing file 
![](/labreport4_screenshots/step4-3.png)  
^At end of step (after saving file) 

## 5: Run the tests, demonstrating that they now succeed
Keys pressed: `<up><up><enter>`
- The `bash test.sh` command was 2 up in the command history, so I accessed it by pressing `<up>` twice and pressed `<enter>` to run the test. 
![](/labreport4_screenshots/step5.png) 
^At end of step 

## 6: Commit and push the resulting change to your Github account (you can pick any commit message!)
Keys pressed: `git<space>add<space><shift>l<tab><enter>`, `git<space>commit<enter>` `iupdate<esc>` `<shift>;wq<enter>` `git<space>push<space>origin<space>main<enter>`
- I added the `ListExamples.java` file to be committed and pushed by typing `git add ` and pressing `<tab>` to autocomplete the filename after typing `L`. 
- I then committed the changes using the `git commit` command. I edited the commit message by pressing `i` to enter insert mode, typing `update`, and pressing `<esc>` to exit insert mode. I saved the commit message by typing `:wq` and pressing `<enter>`. 
- I pushed the changes to the `main` branch of the remote repository (`origin`) by running the `git push origin main` command. 
![](/labreport4_screenshots/step5-1.png)  
^After writing commit message 
![](/labreport4_screenshots/step5-2.png)  
^At end of step (after pushing changes) 