# Introducing the command line

Interecting with programmatic data requires a basic understanding of how to use a command line interface (CLI) - i.e. interacting with our computer using text-based commands.

We do this through a program known as a 'terminal', which runs a software known as a 'shell' - common shells include `bash` and `zsh`. You can probably ignore such details here: for our purposes, phrases such as 'terminal', 'shell', and 'console' are basically synonymous.

It may be the case that you don't end up interacting with the terminal much at all, so don't be put off by the fact that we have to start this journey in possibly the most low-level technical part. However, if you progress to a more advanced level, this will become essential knowledge!

## Opening the command line

### Linux and MacOS

Linux and MacOS are closely related operating systems, part of a family known as 'Unix' (or Unix-like) operating systems. Even though Windows is the most popular consumer OS, Unix operating systems form the basis of most computer infrastructure, and are the basis for scientific computing.

On MacOS and most Linux distributions, you can access the command line through an application called 'Terminal'. On some Linux distributions, it may also be called 'Konsole' or 'gnome-terminal' (although if you are using those distributions you probably don't need this guide).

### Windows

Windows is not a Unix-like OS, and as such has its own set of terminals for interacting with the Windows OS - most commonly 'Command Prompt' (`cmd`) or 'PowerShell'. However, this is a distinct software with its own CLI language and tools. For scientific computing, Windows now has official capability to install a Linux subsystem called Windows Subsystem for Linux (WSL). The will enable to you interact with a command-line interface in the same way as described in this repo and most scientific computing guides.

WSL can come preinstalled on some setups, but if not, information on installing WSL [can be found on the official Microsoft website](https://learn.microsoft.com/en-us/windows/wsl/install). I am not a Windows user, so cannot offer any specific advice, but if you end up installing it let me know if there's anything worth adding to this guide.

## Basic Interactions

### Navigating

When you have opened your terminal, you will see some generic opening statements followed by the command line:

```sh
tom ~ % 
```

The individual details might vary according to the system and shell your are using. Here, `tom` is my login, `~` is my current directory, and `%` is the symbol which indicates you can begin typing commands! (this could be `$` if you are using `bash` rather than `zsh`).

The first thing you might want to find out where you are. You can do this by typing in the command `pwd` (which stands for 'print working directory'), and pressing return:

```sh
tom ~ % pwd
/Users/tom
```

So, we're in the directory `/Users/tom` (think of this as having the same directory open in your GUI file manager). This specific directory is known as the 'home directory' - this is often represented in shorthand as '`~`', which is why it appears as such on our command line.

We can see what is in our directory by using the `ls` (list files) command:

```sh
tom ~ % ls
Applications			bin
Desktop					Movies
Documents				Music
Downloads				OneDrive - Durham University
Google Drive			Pictures
```

Looks about right for my home directory. We can change directories by using the `cd` (change directory) command:

```sh
tom ~ % cd Documents
tom Documents % pwd
/Users/tom/Documents
```

Note that after I changed directories, my command line began showing I was in the `Documents` directory, indicating we succesfully moved. One confusing factor here is that, by typing `cd Documents`, we only searched for directories called `Documents` within the working directory. Now, our working directory has changed, so if I try and change to e.g. `Desktop`, I will get an error:

```sh
tom Documents % cd Desktop
cd: no such file or directory: Desktop
```

This is because there is no directory called `Desktop` in the `Documents` directory (i.e. no filepath `/Users/tom/Documents/Desktop`). So how do we get to the `Desktop` directory from here?

One option would be to provide the full filepath:

```sh
tom Documents % cd /Users/tom/Desktop
```

Another option would be to return to the home directory, and then move to the Desktop from there. We can do this by providing the full filepath (`cd /Users/tom`), or by using the `~` shortcut (`cd ~`). As we are also in a directory 'beneath' the main one, we can also use the `..` shortcut, which says 'go to the directory above this' (e.g. `cd ..`). We could also chain this with the `Desktop` destination to go there directly (e.g. `cd ../Desktop` or `cd ~/Desktop`).

### Some introductory commands

Now that we're comfortable moving around, here are some other common beginner commands:

 - __`mkdir`:__ Makes a directory. e.g. `mkdir new_directory`. 
 - __`echo`:__ Prints text to the terminal window. e.g. `echo hello world`. 
 - __`touch`:__ Creates a new empty file. e.g. `touch new_file.txt`.
 - __`mv`:__ Move or rename a directroy. e.g. `mv new_directory ~/newlocation/new_name_of_directory`.
 - __`rm`:__ Delete a file or directory. e.g. `rm ~/newlocation/new_name_of_directory`. 

### Slightly more advanced commands

Most commands have a series of options you can activate via 'flags'. `rm` is a useful example. For instance, `-i` activates 'interactive mode', where you are promped for confirmation, which is very useful for such a powerful command that can cause damage by deleting files. `-r` deletes 'recursively', deleting all sub-directories and files. This is a **very dangerous** command. The conmmand `rm -r my_directory` will blast away absolutely everything within `my_directory`. A slip of a finger could delete everything within your home directory or hard drive! 

Another useful thing to know is the use of `*` as a wildcard. It tells the shell to find any and all characters. For instance, `ls *.txt` would list all `.txt` files in the current directory, `rm report_*` would delete all files beginning with `report_`, and `cp *.jpg ~/pictures` would copy all `jpeg` files in the current working directory to `~/pictures`.

Some more advance commands that I use a fair amount include the following. I will not explain how to use them, but leave you to google if they are useful (or use the `man` command, which gives you a printed 'manual' of any command!):

 - __`curl` or `wget` (depending on OS):__ download files found at given URLs.
 - __`grep`:__ Search for fragments of text within larger bodies.
 - __`wc`:__ Counts the number or words, lines, characters, etc. in a file or output.
 - __`|` (pipe):__ links commands together. For instance, `ls | wc -l` 'pipes' the output of `ls` into `wc -l`, counting the number of lines in the `ls` output. As `ls` prints out one directory per line, this gives us a count of the number of files and directories in your working directory.
 - __`>` (right angle bracket):__ Output the results into whatever is specified (usually a file) - e.g. `ls > my_directories.txt` 

It is also possible to view and edit documents and files within the command line using commands such as `vim` - I will highlight that it is possible here, but it tends to be preferable for advanced powerusers. I prefer to edit my code using GUI software (specifically, VS Code), and will recommend that in a later section.

There's plenty more, but I will leave you to explore online material for help.

## Shell scripts (`.sh` files)

A shell script is a file that contains a series of commands for Unix-style command-line interpreter to execute. We can use these to automate repetitive tasks. For instance, we could produce our own file to list files in our home directory:

```sh
# counthome.sh

# `ls -1` lists each file on a new line, and `wc -l` counts the lines.
count=$(ls -1 ~ | wc -l)

# Print the result to the terminal.
echo "You have $count files in your home directory."
```

Note a couple new techniques here: `#`, which indicites a 'comment' (the computer will ignore these lines when running, allowing us to make notes for ourself), and setting a variable (`count=`), which allows us to call is later by specifying `$count`.

Now, we run the file by entering `./counthome.sh` - note that `./` is necessary, indicating 'the file within the current directory. If we do so, we will get just the `echo` statement printed to the terminal.

This is a simple and relatively useless example, but later (when learning about running code  on the HPC) we will make use of more practical `.sh` scripts.

## Run commands (`rc` file)

Every time you start a new shell, it will 'forget' all the instructions, variables, and commands you gave it in the previous session. As you develop in using the command line, there may be an number of commands and instructions you want to have at your fingertips.

An `rc` files (e.g. `~/.bashrc` or `/.zshrc`, depending on your shell) is effectively a shell script that is run every time the terminal is started. This allows you to set up your environment and preferences every time you start. You can create an empty file and edit it in a text editor (e.g. `cd ~`, `touch .bashrc`). The `.` preprended to the file name indicates that this is a 'hidden file' that is not shown by default in e.g. file managers, or using the `ls` command.

A useful example of a use of an `rc` is managing your `PATH`. The `PATH` is a list of directories where the shell looks for commands (this includes commands such as `cd` and `ls` that you are already using!). As you create your own scripts and commands, it would be useful to them from anywhere without indicating the full filepath (e.g. `~/foo/bar/usefultool`). As a result, people often put these scripts into a directory called `bin` in an accessible location (e.g. `~/bin/usefultool`). This file can in practice be called anything you like - it is just convention that it is called `bin`, as this communicates the function clearly when other people begin exploring your directories. We can add the directory to the path using the command `export PATH=$PATH:~/bin`. However, we would have to do this every time we open a new session. Instead, by creating an `rc` file and including the line `export PATH=$PATH:~/bin`, this adds the `~/bin` directory to your `PATH` automatically the the beginning of every session. Now, your terminal will search when seeking a command to be executed, and your `usefultool` will work anywhere!

Another example of a useful way of using the `rc` file is using aliases. Say you have a long command you use quite often - for instance, changing directories to one with along filepath (e.g. ). We can use the `alias` tool to save our fingers by creating a shortcut command. Running the command `alias gotodir="cd ~/my/very/long/directory/path"` means that every time you run `gotodir`, it will instead run the longer command in the background. Once again, the shell will 'forget' theses aliases when it is closed, so you will want to add alias commands to your `rc` file.

Later in this material, various parts of the Python installation will add their own lines to your `rc` file. Don't be surprised if things start appearing that you haven't added! It is always best to understand where things have come from and what they do, however, because often lines can be added that are mutually exclusive or break if executed in the wrong order.