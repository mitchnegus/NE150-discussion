# DECF & Command-Line Tutorials

## Contents

[**DECF**](#decf)  

* [Reset password](#reset-password)  
* [Connect to DECF](#connect-to-decf)  
* [Check availabile computers](#check-available-computers)  
* [Exit DECF](#exit-decf)  

[**Command-line basics**](#command-line-basics) 

* [Create text files](#create-a-text-file)  
* [Navigate the filesystem](#navigate-the-filesystem)
* [Manipulate files and directories](#manipulate-files-and-directories)
* [Command-line efficiency](#command-line-efficiency)
* [Get help](#get-help)



## DECF

Here are instructions to get you up and running on the DECF machines. Once you have logged in to DECF, you can continue on to the next section where you can find command-line basics. If you are already familiar with the command-line, you can move on to the [MCNP instructions](mcnp_walkthrough.md) for writing and running MCNP simulations.


### Reset password

Go to the [DECF's account tools](https://www.decf.berkeley.edu/acct/) webpage. Follow the instructions to either _reset a forgotten password_, or _change your password_. If you have not yet changed your password, your initial makeshift password can be found in your DECF account text file. (I email this to you after you forward me your MCNP license from RSICC.)


### Connect to the DECF system  

You must log-in to the Kepler, the remote DECF computer, using SSH (secure shell) or an SSH client. How you do this depends on your operating system. In both examples, replace `ne150-##` with your unique DECF username. This can also be found in the DECF account text file.
	
**_Windows users_**

* Install [Cygwin](https://www.cygwin.com/)/[Putty](https://www.putty.org/)/Gitbash/Windows Bash  
* open a remote connection to DECF (`ne150-##@kepler.berkeley.edu`)

**_Mac/Linux users_**
	
* Open terminal (it is preinstalled; on Mac, look under _Utilities_)
* ssh into DECF (replacing `##` with your number)
	
	```
	$ ssh -X ne150-##@kepler.berkeley.edu
	```

If your login is successful, you should see a welcome message appear on the screen. It should look something like this:
	
```
Last login: Mon Mar  5 15:33:33 2018 from airbears2-10-142-32-65.airbears2.1918.berkeley.edu
**************************************************
	
Please remember to only run jobs on either the
1111 Etcheverry or Archipelagos clusters.

DECF website:
http://www.decf.berkeley.edu

Check the clusters status:
http://www.decf.berkeley.edu/ganglia

Send questions/requests to:
consult@newton.berkeley.edu

**************************************************
```
	
	
### Check available computers

MCNP and Serpent are not loaded on all of the DECF computers, just those in Etcheverry 1111. The 1111 computers are only accessible from Kepler, but the login process is similar. One key difference is that these computers are shared across all NE 150 students, however, and so at any given time some of them may be experiencing larger computational loads. Since there are many 1111 computers to choose from, go to the [DECF Ganglia page](https://www.decf.berkeley.edu/ganglia/).

* Click the name "1111 Etcheverry" to see computers in that room (only computers in that room have MCNP/Serpent installed).
* Choose a computer with a low workload from the graphs at the bottom of the page.
* Switch to that computer for running MCNP/Serpent calculations, again using SSH: 
	
	```
	ssh <jive,mambo,foxtrot,minuet,etc.>` 
	```
		
	Ommit the angle brackets, and note that you do not need either your username or the full web address here. Since you are in the DECF system already, this information is saved. Also, your files and folders are shared across all these machines (and Kepler), so you don't always have to choose the same one.
		
	**Do not run MCNP/Serpent on Kepler.**
		
		
### Exit DECF

Finally, when you are done, logging off the DECF computers is straightforward. Just type `exit`, and you will sever the SSH connection.



## Command-line basics

Once you have connected to the DECF machines, you will only be able to operate them via the command-line. As such, it is critical that you know how to use the command-line, at least at a very basic level. 

The command-line works very similar to an interactive programming language, and is often called the shell. There are a variety of different shell types, and the shell type used by any given computer is dependent on the operating system. DECF, which runs a flavor of Linux, uses _tcsh_ as its default shell. You may also frequently hear of _Bash_, which is the default shell on macOS and Ubuntu. _Bash_ is on the whole very similar to _tcsh_, except for some minor differences. 

Rather than having a user interface, like _My Computer_ on Windows, or _Finder_ on Mac, the command-line requires that you type in one or more commands as (usually) terse keywords, and then hitting enter to execute the command. In the following instructions, a `$` is the prompt symbol, and indicates that what follows needs to be entered into the terminal. Each `$` indicates a new command.
		 
		 
### Create text files

Working on the command line often requires us to write notes, inputs, and/or scripts. These can all be created as simple text files. Let's create a README as a test. First, we open a text editor. If you are going to be working with the command line a lot, you should eventually get familiar with some of the more powerful editors–especially either _Vi_ or _Emacs_. You might find the learning curve for those a bit steep for the moment though, so this tutorial will use the simpler and more lightweight _nano_. The command to open the editor is just `nano`, which will open a blank text file. Following the command with a filename will open a file with that name. To create a README, type
	
```
$ nano README.txt
```
	
Since `README.txt` does not yet exist, this command will both create _and_ 	open the file. If `README.txt` did exist, the command would just open it. Let's now type something in this file: 
	
(example)

```	
==================== <Your Name> ====================
		
This is the DECF home directory for <Your name>. 
This directory will include code (MCNP/Serpent) for 
NE 150 - Spring 2018.
```
	
Once the file is written save it, by typing `^O` (for write-out), and exit, by typing `^X` (`^` is the `<ctrl>` key). If you forget these commands, nano conveniently displays them all at the bottom of the screen.


### Navigate the filesystem

The structure on this system is very similar to your personal computer, with files and folders (technically called directories). You can **list** the contents of the directory you are in at the moment by typing `ls`. If you execute this command, you shouldn't see anything but the README, if you just created it in this directory. Also, you can always tell where in your file-system you are by typing `pwd`, which stands for **p**resent **w**orking **d**irectory. The console output should show something like `/home/ne150-##` (again, replacing `##` with your personal account number). This is the local computer address of your current location, called the **path**.
	
In the path, each term separated by a backslash is a separate directory, and you are located in the last one. (In this example, you are in your root directory, `ne150-##`, a subdirectory of `home`.)
		
#### Directories and subdirectories
	
You may create directories and subdirectories using the command `mkdir` (for "**m**a**k**e **dir**ectory") followed by the name of the directory. 

```
$ mkdir mcnp-tests
```
		
On your personal computer, you'd click this new folder, `mcnp-tests`, to go inside. On the command line, we use the command `cd` (for **c**hange **d**irectory). Create a new directory, `mcnp-tests` by running

```
$ cd mcnp-tests
```
	
Now, if we type `ls` we shouldn't see anything listed, but we can check that we are in the right place by typing `pwd`. We should see that we've moved into the location `/home/ne150-##/mcnp-tests`.


You can change directories to anywhere on your system by specifying the entire path to that location (assuming the location exists and you have permission to access it).
	
```
$ cd /some/other/place
```	

##### Special Path Shortcuts
	
The Unix command line uses special characters to indicate some special directories in relation to where you are currently located: `.`,`..`, `~`, and `-`.

* **`.`** The single period is a shortcut for whatever directory you are inside at the moment. It is equivalent to the output of the `pwd` command. 
* **`..`** The double period is a shortcut for the (parent) directory immediately above your current directory. To get back into this parent directory, just type
	
	```
	$ cd ..
	```	
* **`~`** The tilde is a shortcut for your username's home directory. This is where you are placed immediately after login; on DECF this is the `/home/ne150-##` directory. The path to the `mcnp-tests` directory (explicitly `/home/ne-150-##/mcnp-tests`) can be abbreviated as `~/mcnp-tests`. While you could also use `~` to conveniently get back to your home directory with the command
	
	```
	$ cd ~
	```
the home directory is such a commonly accessed location that `~` is the default location. Just typing 

	```
	$ cd
	``` 
will work too.
* **`-`** The dash is a shortcut for the directory you were previously in. Typing 

	```
	$ cd -
	```
is like using a web-browser's back button, and will take you to your last location. Note that you cannot use the `-` in file or directory paths, just when changing directories.

#### Absolute and relative paths
	
The highest directory on your computer is always given as just a single backslash, `/`. Any file or location on your computer can be specified in relation to this directory, and that path is the **absolute path**. In the example above, the directory `/` contains a directory named `some`, which contains a directory named `other`, which contains a directory named `place`. 
	
Let's take a look at an example directory tree that you might use for NE150:
		
```
/
└── home/
    └── ne150-##/
        ├── README.txt
        ├── mcnp-tests/
        │   ├── mcnp-test1.inp
        │   └── mcnp-test2.inp
        └── hw/
            ├── mcnp-hw1.inp
            └── mcnp-hw2.inp
``` 

In this example, each indent represents another subdirectory level, and we have added another subdirectory, `hw`, to join `mcnp-tests` inside our `ne150-##` directory. We can also see that several MCNP input files were added to the subdirectories of `ne150-##`.  One of these files, `mcnp-test1.inp` exists in the `mcnp-tests` directory, and so the absolute path to that file would be
	
```
/home/ne150-##/mcnp-tests/mcnp-test1.inp
```
	
You can also give a **relative path** to a file, based only on your current location. Say you are located in the `ne150-##` directory, you are able to give the path to `mcnp-input1.inp` as just
	
```
mcnp-tests/mcnp-test1.inp
```

You can see here that you don't need to specify the directories above where you are located in the path. The computer works from where you are at the moment.
	
Notice this path does not start the path with a backslash (`/mcnp-tests/mcnp-test1.txt`). If it had, the computer would look for the directory named `mcnp-tests` in the root directory `/`. By starting a path with a backslash, the computer assumes you are giving an absolute path, rather than a relative path. 
	
Lastly, we can also specify relative paths using the directory shortcuts `.` and `..`. Using our relative path example above, the relative path to `mcnp-test1.inp` could be written equivalently as
	
```
./mcnp-tests/mcnp-test1.inp
```

which just explicitly indicates that `mcnp-tests` is a subdirectory in the current directory (`ne150-##`). 
	
Along these same lines, we can reference a file using any and all parent directories of the current directory using the `..` shorthand. If we are in the `mcnp-tests` directory and want to give the path to `mcnp-hw1.inp`, we need to go up one directory to `ne150-##` (given by shortcut `..`), and back down into `hw` to find it. The relative path is then	
	
```
../hw/mcnp-hw1.inp
```

You can use multiple `..` shortcuts separated by backslashes to go up through an arbitrary number of parent directories. As an example, if you wanted to reference the root directory `/` from the `mcnp-tests` directory, you could use the relative path

```
../../..
```

to specify that `/` is 3 directories above `mcnp-tests`. (Though in this specific instance, it is still much more efficient to just use the absolute path, `/`.)


### Manipulate files and directories

Once you are able to navigate your system, you should also learn how to manipulate files. Just like you are able to copy, move, and delete files on your personal computer, you can use keywords to perform the same actions on the command-line. To demonstrate, we will reproduce the example directory structure described in the last section.

#### Redirecting an echo

Almost all programming languages include some form of print statement that prints an output to the screen. On the command line, the `echo` command "echoes" the command's input to the console. 

```
$ echo "Hello world"
Hello world
```

In addition to opening and writing a file using a text editor, we can use an output redirect to send the output of any command to a file. Any command followed by a `>` and a filename will have its output redirected into the file, rather than the console. 

```
$ echo "Hello World" > helloworld.txt
```

Note that this redirect will overwrite the file if it exists, and create a new file if it does not. Frequently you may want to add text to the file, rather than overwrite it. The `>>` redirect will append output to the end of a file in this manner. Let's create a file that will eventually contain an MCNP input. We can change into the `mcnp-tests` directory and create the file `mcnp-test1.inp` by typing

```
$ cd mcnp-tests
$ echo "Sample MCNP Input" >> mcnp-test1.inp
```

If you open the `mcnp-test1.inp` file, you should the statement you passed to the echo command. 

#### Remove files

Since we no longer need the `helloworld.txt` file, we can remove it using the `rm` command:

```
rm helloworld.txt
```

You can remove directories in the same way, however you must add the `-r` option to indicate that the shell should recursively delete the  directory and all of it's contents. (You must include the `-r` option even if the directory is empty.)

#### Copy files

You can copy this file using the `cp` command.

```
$ cp mcnp-test1.inp mcnp-test2.inp
```

This takes the file `mncp-test1.inp` and copies it as the file `mcnp-test2.inp`, leaving the original in-place.

Next, we can create the `hw` directory by copying the `mcnp-test` directory. Like removing directories, we must include the recursive, `-r` option to copy directories. If we move up one directory, back into `ne150-##`, we can recursively copy the `mcnp-tests` directory into one we might use for homework inputs.

```
$ cd ..
$ cp -r mcnp-tests hw
```

#### Move and rename files

Both moving and renaming files is performed with the same command (you might consider renaming a file as just moving the file to a new location corresponding to the new name). The command syntax follows a similar pattern to copying files.

If we change into the `hw` directory, we can rename the freshly copied `mcnp-test1.inp` and `mcnp-test2.inp` files:

```
$ cd hw
$ mv mcnp-test1.inp mcnp-hw1.inp
$ mv mcnp-test2.inp mcnp-hw2.inp
```

Unlike copying or removing files, you do not need the recursive `-r` option when moving or renaming directories.

##### Moving/Copying Rules

There are some subtle rules that are followed depending on what you give the copy/move commands as arguments.

###### File to file:
If the first argument (the object to be copied) is a file and the second argument (the destination) is a file, the file will be moved/copied into that file.
###### File to directory:
If the first argument is a file and the second argument is a directory, the file will be moved/copied into that directory but keep its name.
###### *Directory to directory:
If the first argument is a directory and the second argument is a directory, the first directory will be moved/copied into the second directory, provided the second directory already exists. If it doesn't already exist, the first directory will be moved/copied as the second directory. 


### Command-line efficiency

When working on the command line, there are tons of useful tricks you can use to work more efficiently. Here are some of the ones that you might find most useful: 

* **`<Up/Down-Arrows>`** Cycle through your previous inputs and save yourself from repeatedly typing the same command.
* **`clear`** Clear the console to have an uncluttered workspace.
* **`<tab>`** Autocomplete the command you're typing, including commands and paths.
* **`<ctrl> + a`** Move the cursor to the start of the line (like the "Home" key).
* **`<ctrl> + e`** Move the cursor to the end of the line (like the "End" key).
* **`<ctrl> + k`** Delete everything from the cursor to the end of the line.


### Get help

When you're in doubt about something there are a couple of good options. First, Google is your friend. Almost every question you will come up with has been posed/answered on [StackOverflow](https://stackoverflow.com/questions/3327013/how-to-determine-the-current-shell-im-working-on). Second, most shell commands have a manual entry, which can be accessed with the `man` command. These give very thorough (though sometimes difficult for beginners to read) documentation of the command. As an example, you could try 
	
```
man ls
```

To exit the manual, type `q`.


### Other commands: 

There are many other commands or concepts that you may find useful. I've included a list here; feel free to look them up.

* Remote copy: `scp`/`scp -r`
* List all: `ls -la` 
* variables
* hidden files (`.file`)  
* printenv  
* screen

---
[MCNP Walkthrough >>](mcnp_walkthrough.md)