# Basic Shell Commands
***

## 1. Shell Basics:

| Command        | Definition                                                                                                     |
|----------------|----------------------------------------------------------------------------------------------------------------|  
| `.`            | a single period refers to the current directory                                                                |  
| `..`           | a double period refers to the directory immediately above the current directory                                |  
| `~`            | refers to your home directory. _Note:_ this command does NOT work on Windows machines (Mac and Linux are okay) |  
| `cd ./dirname` | changes the current directory to the directory `dirname`                                                       |  
| `ls -F`        | tells you what files and directories are in the current directory                                              |  



## 2. Creating Things:
### a) How to create new files and directories..

| Command           | Definition                                                                                                                                                                                                                                                                                                                                            |  
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
| `mkdir ./dirname` | makes a new directory called dirname below the current directory. _Note:_ Windows users will need to use `\` instead of `/` for the path separator                                                                                                                                                                                                    |  
| `nano filename`   | if `filename` does not exist, `nano` creates it and opens the `nano` text editor. If the file exists, `nano` opens it. _Note:_ _(i)_ You can use a different text editor if you like.  In gnome Linux, `gedit` works really well too. _(ii)_ `nano` (or `gedit`) create text files. It doesn't matter what the file extension is (or if there is one) |  

### b) How to delete files and directories...
#### _Remember that deleting is forever. There is NO going back_

| Command           | Definition                                                                                                       |  
|-------------------|------------------------------------------------------------------------------------------------------------------|
| `rm ./filename`   | deletes a file called `filename` from the current directory                                                      |  
| `rmdir ./dirname` |  deletes the directory `dirname` from the current directory. _Note:_ `dirname` must be empty for `rmdir` to run. |  

### c) How to copy and rename files and directories...

| Command | Definition                                                                                                                                                                                                                    |  
|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
| `mv tmp/filename .` | moves the file `filename` from the directory `tmp` to the current directory. _Note:_ _(i)_ the original `filename` in `tmp` is deleted. _(ii)_ `mv` can also be used to rename files (e.g., `mv filename newname` |  
| `cp tmp/filename .` | copies the file `filename` from the directory `tmp` to the current directory. _Note:_ _(i)_ the original file is still there                                                                                      |  



## 3. Pipes and Filters
### a) How to use wildcards to match filenames...
Wildcards are a shell feature that makes the command line much more powerful than any GUI file managers. 
Wildcards are particularly useful when you are looking for directories, files, or file content that can
vary along a given dimension.  These wildcards can be used with any command that accepts file names or 
text strings as arguments.

#### Table of commonly used wildcards 

| Wildcard               | Matches                                        |  
|------------------------|------------------------------------------------|  
| `*`                    | zero or more characters                        |  
| `?`                    | exactly one character                          |  
| `[abcde]`              | exactly one of the characters listed           |  
| `[a-e]`                | exactly one character in the given range       |  
| `[!abcde]`             | any character not listed                       |  
| `[!a-e]`               | any character that is not in the given range   |  
| `{software,carpentry}` | exactly one entire word from the options given |  

See the cheatsheet on regular expressions for more "wildcard" shortcuts.

### b) How to redirect to a file and get input from a file ...
Redirection operators can be used to redirect the ouput from a program from the display screen to a file where it is saved (or many other places too, like your printer or to another program where it can be used as input).


| Command | Description                                                                                                                     |  
|---------|---------------------------------------------------------------------------------------------------------------------------------|  
| `>`     | write `stdout` to a new file; overwrites any file with that name (e.g., `ls *.md > mardkownfiles.txt`)                          |  
| `>>`    | append `stdout` to a previously existing file; if the file does not exist, it is created (e.g., `ls *.md >> markdownfiles.txt`) |  
| `<`     | assigns the information in a file to a variable, loop, etc (e.g., `n < markdownfiles.md`)                                       | 



#### b.1) How to use the output of one command as the input to another with a pipe...
A special kind of redirection is called a pipe and is denoted by `|`. 

| Command | Description                                                                                                                                           |  
|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------|  
| `|`     | Output from one command line program can be used as input to another one (e.g. `ls *.md | head` gives you the first 5 `*.md` files in your directory) |  


*  Combining single-purpose filters with pipes is the most productive way to use the shell...
   *   a program conforms that to Unix conventions, it can easily be combined with others...

Example:   

    ls *.md | head | sed -i `s/markdown/software/g`
   
changes all the instances of the word `markdown` to `software` in the first 5 `*.md` files in your current directory.


## 4. Variables
### a) Assignment
* **`varname=1`** -->

### b) Indexing 
* **`varname[0]`** --> _Note:_ the shell is zero indexed.  That means you always start counting from zero

### c) Referencing
* **`${varname}` -->
* **`${varname[@]` --> 

 

## 5. Loops
NEED TO DO VARIABLE ASSIGNMENT FIRST!!!!
### a) How to repeat operations using a loop...
* **`for`** -->  
    `for filename in *.dat
    do
      mv ${filename} ${newname}
    done`
    
* **`while`** -->
    `count=0   
     while ${count} -lte 6
     do
       COMMAND HERE
     done`

### b) That the loop variable takes on a different value each time through the loop...
### c) The difference between a variable's name and its value...
### d) Why spaces and some punctuation characters shouldn't be used in files' names...
### e) How to display history and re-use commands...
* **`history`** --> displays your command history to the standard output (usually the screen)



## 6. Shell Scripts
### a) How to store shell commands in a file...
### b) How to run a shell script...
### c) How to pass filenames into a shell script...



## 7. Finding Things
### a) How to select lines matching patterns in text files...
* **`grep [options] day haiku.txt`** --> finds every instance of the string `day` in the file haiku.txt and pipes it to standard output. 
	* **`-E`** --> tells grep you will be using a regular expression. Enclose the regular expression in quotes. _Note:_ the power of `grep` comes from using regular expressions. Please see the regular expressions sheet for examples
	* **`-i`** --> makes matching case-insensitive
	* **`-n`** --> limits the number of lines that match to the first n matches
	* **`-v`** --> shows lines that do not match the pattern (inverts the match) 			
	* **`-w`** --> outputs instances where the pattern is a whole word

### b) How to find files with certain properties...
* **`find . -type d` -->
	* **`-type [df]`** --> d lists directories; f lists files
	* **`-maxdepth n`** --> `find` automatically searches subdirectories. If you don't want that, specify the number of levels below the working directory you would like to search
	* **`-mindepth n`** --> starts `find`'s search n levels below the working directory
	
### c) How to use one command's output as arguments to another command...

### d) How are text and binary files different?...
