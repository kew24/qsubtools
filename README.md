# qsubtools

qsubtools is a suite of shell scripts to automate PBS submissions

## qsubi

qsubi automates the submission of creating and activating an interactive node  

```
------------------------------  QSUB INTERACTIVE HELP  
---------- PROGRAM		== qsubi (qsub interactive)
---------- VERSION		== 2.0.3
---------- DATE			== 2022_06_24
---------- CONTACT		== lee.marshall@vai.org
---------- DESCRIPTION		== automates creation of PBS interactive job
---------- PATH			== export PATH=\$PATH:/path/to/qsubi/directory
-------------------- COMMANDS 
---------- USAGE		== qsubs [options]* -s "command"
---------- FLAGS
	[ -d | --debug ]		== creates job script but does not execute
	[ -h | --help ]			== help function
---------- OPTIONS
	[ -c | --cores <int> ]		== number of cores per job 1 to 80, default 1 core
	[ -n | --node <node> ]		== name of specific node, default any node
	[ -N | --name <name> ]		== name specific to job, default STDIN
	[ -q | --queue <name> ]		== specify queue name, default any queue
	[ -w | --walltime <int> ]	== number of hours per job 1 to 744, default 24 hours
-------------------- EXAMPLES 
qsubi
qsubi -c 4 -q shortq
```

## qsubs

qsubs automates the submission of creating and activating of job submissions. 
qsubs will automate single and array based submissions as well as linux and 
R based submissions. 

```
------------------------------  QSUB SUBMITTER HELP  
---------- PROGRAM		== qsubs (qsub submitter)
---------- VERSION		== 2.0.3
---------- DATE			== 2022_06_24
---------- CONTACT		== lee.marshall@vai.org
---------- DESCRIPTION		== automates creation and submission of PBS qsub scripts
---------- PATH			== export PATH=\$PATH:/path/to/qsubs/directory
-------------------- COMMANDS 
---------- USAGE		== qsubs [options]* -s "command"
---------- FLAGS
	[ -d | --debug ]		== creates job script but does not execute
	[ -h | --help ]			== help function
	[ --no_info ]			== suppress PBS description info on output scripts
---------- OPTIONS
	[ -a | --array <file> ]		== file containing column of sample names for array, 
						use SAMPLE as variable for sample name in command or script
	[ -c | --cores <int> ]		== number of cores per job 1 to 80, default 1 core
	[ -n | --name <name> ]		== name specific to job, default user name and date
	[ -q | --queue <name> ]		== specify queue name, default any queue
	[ -r | --rscript <"command"> or <file> ]	== command enclosed in double quotes or script file		
	[ -s | --script <"command"> or <file> ]	== command enclosed in double quotes or script file
	[ --script_args <args> ]	== positional arguments passed to your bash script file
	[ -u | --umask <umask>]		== umask value, default 0022 (group read)
	[ -w | --walltime <int> ]	== number of hours per job 1 to 744, default 24 hours
-------------------- MULTIPLE COMMANDS 
---------- USAGE		== contain multiple commands with double quotes, 
					with each command on separate line, see example
---------- COMMAND VARIABLES	== must start with a backslash \$1
-------------------- EXAMPLES 
touch sample_data.txt
qsubs -n gzip_file -s "gzip sample_data.txt"
touch sample1_data.txt
touch sample2_data.txt
echo sample1 > sample_names
echo sample2 >> sample_names
qsubs -n zip_command -a sample_names -s "zip SAMPLE_data.zip SAMPLE_data.txt"
echo "zip SAMPLE_data.zip SAMPLE_data.txt" > sample_script
qsubs -n zip_script -a sample_names -s sample_script -d
```
