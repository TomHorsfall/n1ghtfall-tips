# Finding files in Windows using the dir command


After successfully gaining access to a machine, one of the most important toolsets you’ll need to acquire is the ability to navigate the OS and look for files that may aid you in elevating your privileges OR finding the flag you need.


Understanding various windows command search functions is essential in making this process as easy as possible. I’ve spent far too much time trying to parse directories with a minimal understanding of the tools at my disposal. The purpose of this readme is to help beginners learn some basic windows commands for searching files.


Resources:
- https://www.howtogeek.com/363639/how-to-use-the-dir-command-in-windows/
- https://www.computerhope.com/dirhlp.htm
 

## The dir command

This command is used in Windows to display what is stored in the current working directory


Switches used by the dir command:

- d: Displays all directories in the current path
- r: Displays read only files
- h: Displays hidden files
- a: Files that are ready for archiving??
- s: system files (a.) files that Windows depend on to operate and b.) files with the hidden flag turned on)
- i: Not content indexed files
- l: Reparse points?
 

Important Notes:

You can combine flags for different functionality
For example: “dir /adh” will display all hidden directories
You can use the “-“ flag as a NOT Boolean
For example: “dir /a-d” would display all files that are NOT directories
 

Here are some examples of how to use the dir command:
 

Display all directories:

```bash
dir /ad
````

 

### Sorting Your Results

 

One can use the /O switch followed by various codes to display results by time and date. This may be useful if you’re in a directory with thousands of files and need to see the most recently created file (or the very first file created)
 

Switches to use with dir “ /O” to sort your results:

```bash
D: Sorts by date/ time. Older entries appear first.dir
E: Sorts by file extension in alphabetical order.
G: Sorts by listing folders first, then files.
N: Sorts by the name of file/ folder in alphabetical order.
S: Sorts by file size, smallest to largest.
```

Important Notes:

You can switch the order of any of these by including the “-“
For example: If you wanted the newest entries to appear first you could run “dir /O-D” rather than “dir /OD”
 
 

# Look Recursively for files within a folder (and subfolders) using the /s command


Using this command will return a lot of results.
This command is sometimes useful to run when you need to look for a particular file within a few subdirectories but aren’t sure where it exists. Expect that it will take some time to return results

To Display All Files and Folders and Everything Inside:


```bash
dir /s
```


The above command will list the results of all files within the subdirectories of the current working directory.


If you wanted to list all files of a certain type (for example all python files) you could run a command like this:

 

```bash
dir *.py /s
```


This will return the location of all py files within the subdirectories of the current working directory


If there are a TONF of results we can add the /p flag which will “pause” the results after each new directory where a file is found.

 

```bash
dir *.py /s /p
```


### Saving your findings to a file



Something to remember is that if you need to remember what you searched for, you can do this using a pipe. This will save the output to a file of your choosing and then you can review it at another time if needed

 

For example:

 

```bash
dir *.py /s > all_python.txt
```