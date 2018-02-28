# DECF Walkthrough

1. Reset password
1. \<Windows users\> 

	* Install Cygwin/Putty/Gitbash/Windows Bash  
	* open a remote connection to DECF (`ne150-##@kepler.berkeley.edu`)

	\<Mac/Linux users\>
	
	* Open terminal
	* ssh into DECF (`ssh -X ne150-##@kepler.berkeley.edu`)

1. Create a text file (`nano README.txt`)
	
	* Write something in this textfile: 
	
	```
	example:
	
	==================== <Your Name> ====================
	
	This is the DECF home directory for <Your name>. 
	This directory will include code (MCNP/Serpent) for 
	NE 150 - Spring 2018.
	```
	
	* Save and exit the file.

1. Make a subdirectory:
		`mkdir <some-dir-name>`
		
1. Change into that subdirectory:
		`cd <some-dir-name>`

1. Check available computers
	* Go to the [DECF Ganglia page](https://www.decf.berkeley.edu/ganglia/).
	* Choose room 1111 Etcheverry (only computers in this room have MCNP/Serpent installed).
	* Check for a computer with a low workload from the graphs at the bottom of the page.
	* Switch to that computer for running MCNP/Serpent calculations:
		`ssh <jive,mambo,foxtrot,minuet,etc.>`  
		 **Do not run MCNP/Serpent on Kepler.**
		
1. Exit the DECF machines: `exit`