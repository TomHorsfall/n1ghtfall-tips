# Bash Command Line Tips

Bash is one of the most common command line languages used within Linux environments. Understanding how bash works and it's capabilities is essential in becoming an excellent penetration tester or linux administrator. 

Topics Covered:

1. [Environmental Variables](#1-environmental-variables)
2. [Bash History (And reverse-i-search functionality)](#bash-history)
3. Piping and Redirection
4. Text Search and Manipulation
5. Editing Files from the Command Line (vi or vim)
6. Comparing Files
7. Managing Processes
8. File and Command Monitoring
9. Downloading Files
10. Bash Customization

## 1. Environmental Variables
## What are Environmental Variables?
- An Environmental Variable in the context of computer programming are variables set within the command line environment that point to resources on the machine that can be used in processing certain programs or requests.

An Example:
The **PATH** variable is a well-known and necessary environmental variable that is used to tell the computer exactly where certain programs are located. For example, if you want to run python from the command line at any time, you need to define the location of the python exectuable within the PATH variable, otherwise your computer will return a "command not found" error. 

You can look at your path variable from the command line like so:

```bash
echo $PATH
/usr/bin:/bin:/mingw64/bin:/usr/bin
```

Some other useful variables include $USER (aka what user your are), $PWD (print working directory), and $HOME (tells you the location of the user's home directory).

### Defining an environmental variable

An environmental variable can be defined via the **export** command. 

Example:
```bash
export ip=10.10.10.10

ping $ip
```

The export command makes the variable accessible to any subprocesses we might spawn from our current Bash instance. if we set an env variable ithout **export** it will only be available in the current shell. 

To view all environmental variables, you can use the env command:

```bash
$ env
USERDOMAIN=Tom
OS=Windows_NT
COMMONPROGRAMFILES=C:\Program Files\Common Files
PROCESSOR_LEVEL=6
```

## Bash History

Why is thee **history** command so useful? 

During a penetration test you may be logging in as a different user. And if you login with a specific user account, if you run the "history" command it will show commands previously run by that user. Sometimes this could include passwords, give you information on what kinds of servcies are running on the host, or give you information about useful tools that are installed on the host. 

### Tips and Tricks

Let's say the output of histpry looks like this:

```bash
  167  ./test_script.sh tom
  168  ls
  169  echo $path
  170  echo $PATH
  171  echo $home
  172  echo $HOME
  173  env
  174  history
  ```
  If we wanted to re-run the command from line 167, we could type this:
  ```bash
  !167
  ```
  Rather than re-typing the entire command. 

  Or if we wanted to re-run the last command sent we could type this:

  ```bash
  !!
  ```

  ### Where is this information stored?

  Command history is stored in the .bash_history file in the home directory of the user. 
  
  You can control the size of the output of the history command via the **HISTSIZE** and **HISTFILESIZE** env variables.

  **HISTSIZE** Controls the number of commands stored in memory for the current session and 
  **HISTFILESIZE** configures how many commands are kept in the history file. 

  To explore the bash history you can also use the "Up" or "Down" directional arrows on the keyboard to scroll through past commands


To explore previous commands you can also leverage the **reverse-is-search** functionality that comes with bash. 

This tool essentially uses regular expressions to looks through command history and find a command you are looking for. 

To activate this functionality type "Ctrl + r" and begin typing a command you had typed previously. If you find it, hit enter or use the right directional arrow to auto tab the command and then hit ENTER. 

Why would you use this command?

Because sometimes you'll be digging through a computer and realize you need to re-run a command you had done an hour ago. This tool makes it exceptionally easier to figure out what that command was if you couldn't exactly remember what it was, but you remember how it started. 

Example output:
```bash
14407@Tahm MINGW64 ~/Documents/Tips/n1ghtfall-tips (main)
(reverse-i-search)`':
```

## Piping and Redirection









