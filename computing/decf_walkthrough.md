# DECF Walkthrough

Here are some simple instructions to get you up and running on the DECF machines. Once you have completed these instructions, move on to the [MCNP instructions](mcnp_walkthrough.md) for writing and running MCNP simulations.

1. #### Reset password
	Go to the [DECF's account tools](https://www.decf.berkeley.edu/acct/) webpage. Follow the instrcutions to either _reset a forgotten password_, or _change your password_.


1. #### Connect to the DECF system  

	You must log-in to the Kepler, the remote DECF computer, using SSH (secure shell) or an SSH client. How you do this depends on your operating system. In both examples, replace `ne150-##` with your unique DECF username. This can be found in the text file attachment I emailed you earlier in the semester.
	
	**_Windows users_**

	* Install Cygwin/Putty/Gitbash/Windows Bash  
	* open a remote connection to DECF (`ne150-##@kepler.berkeley.edu`)

	**_Mac/Linux users_**
	
	* Open terminal (it is preinstalled; on Mac, look under _Utilities_)
	* ssh into DECF 
	
		```
		ssh -X ne150-##@kepler.berkeley.edu
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
	
	
1. #### Check available computers

	MCNP and Serpent are not loaded on all of the DECF computers, just those in Etcheverry 1111. The 1111 computers are only accessible from Kepler, but the login process is similar. One key difference is that these computers are shared across all NE 150 students, however, and so at any given time some of them may be experiencing larger computational loads. Since there are many 1111 computers to choose from, go to the [DECF Ganglia page](https://www.decf.berkeley.edu/ganglia/).
	* Click the name "1111 Etcheverry" to see computers in that room (only computers in that room have MCNP/Serpent installed).
	* Choose a computer with a low workload from the graphs at the bottom of the page.
	* Switch to that computer for running MCNP/Serpent calculations, again using SSH: 
	
		```
		ssh <jive,mambo,foxtrot,minuet,etc.>` 
		```
		
		Note that here you do not need either your username or the full web address. Since you are in the system already, this information is saved. Also, your files and folders are shared across all these machines (and Kepler), so you don't always have to choose the same one.
		
		**Do not run MCNP/Serpent on Kepler.**
		 
		 
1. #### Create a text file

	Working on the command line often requires us to write notes, inputs, and/or scripts. These can all be created as simple text files. Let's create a README as a test. First, we open a text editor. If you are going to be working with the command line a whole bunch, I suggest you eventually get familiar with some of the more powerful editors–especially either _Vi_ or _Emacs_. You might find the learning curve for those a bit steep for the moment though, so I will use the much simpler and more lightweight _nano_. The command is 
	
	```
	nano README.txt
	```
	
	Since `README.txt` does not yet exist, this command will both create _and_ 	open the file. If `README.txt` did exist, the command would just open it in _nano_. Let's type something in this file: 
	
	(example)
	
	```	
	==================== <Your Name> ====================
	
	This is the DECF home directory for <Your name>. 
	This directory will include code (MCNP/Serpent) for 
	NE 150 - Spring 2018.
	```
	
	Once the file is written save it (`<ctrl> O`) and exit (`<ctrl> X`). 


1. #### Navigate through your files

	The structure on this system is very similar to your personal computer, with files and folders (also called directories). You can list all the contents of the folder you are in at the moment by typing `ls`. If you execute this command, you shouldn't see anything but the README you just created in this directory. Also, you can always tell where in your file-system you are by typing `pwd`. This should show something like `/home5/ne150-##`. Each term separated by a backslash is a separate directory, and you are in the last one. (In this example, you are in your root directory, `ne150-##`, a subdirectory of `home5`.)
	
	You may create directories and subdirectories using the command `mkdir` (for "**m**a**k**e **dir**ectory") followed by the name of the directory.

	```
	mkdir ne150_mcnp
	```
	
		
	On your personal computer, you'd click this new folder to go inside. On the command line, we use the command `cd` (for **c**hange **d**irectory).

	```
	cd ne150_mcnp
	```
	
	Now, if we type `ls` we shouldn't see anything listed, but we can check that we are in the right place by typing `pwd`. We should see that we've moved into the location `/home5/ne150-##/ne150_mcnp`.
	
	The Unix command line uses special characters to indicate two special directories in relation to where you are currently located. First is `.`, which is a shortcut for whatever directory you are inside. `.` is equivalent to the output of the `pwd` command. The second special character is `..`, a special shortcut for the (parent) directory immediately above your current directory. To get back into this parent directory, just type
	
	```
	cd ..
	```
	
	You can change directories to anywhere on your system by specifying the entire path to that location (assuming the location exists and you have permission to access it).
	
	```
	cd /path/to/my/favorite/directory
	```	

1. #### Get help

	When you're in doubt about something there are a couple of good options. First, Google is your friend. Almost every question you will come up with has been posed/answered on [StackOverflow](https://stackoverflow.com/questions/3327013/how-to-determine-the-current-shell-im-working-on). Second, most shell commands have a manual entry, which can be accessed with the `man` command. These give very thorough (though sometimes difficult for beginners to read) documentation of the command. As an example, you could try 
	
	```
	man ls
	```
	
		
1. #### Exit the DECF machines

	Logging off the DECF computers is very straightforward. Just type `exit`, and you will sever the SSH connection.


Other commands:  
* cp/cp -r  
* rm/rm -rf  
* ls -la  
* clear  
* echo
* variables
* hidden files (`.file`)  
* printenv  
* screen

---
[MCNP Walkthrough >>](mcnp_walkthrough.md)