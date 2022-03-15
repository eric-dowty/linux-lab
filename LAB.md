# Linux Lab

This lab will walk you through several basic Linux commands and key concepts. It has been tailored for commands specific 
to the Debian v10 release. The examples in the following sections will include the actual command used and expected 
outputs. Your output may be slightly different, which is ok. If you see a **BEFORE MOVING ON** notice just make sure 
that you are getting the right results before moving to the next section.

## Part 1: Getting Help

For all the commands it is helpful to know that you can always refer to the man page (help file) if you get lost or 
confused by simply typing the word `--help` after the command. For example, running command `mkdir --help` prints out 
instructions for how to use the `mkdir` command.

### Exercise 1.1:

Type `mkdir --help` into the command line and press enter. You should see the following usage instructions:

```commandline
root: mkdir --help
Usage: mkdir [OPTION]... DIRECTORY...
Create the DIRECTORY(ies), if they do not already exist.

Mandatory arguments to long options are mandatory for short options too.
  -m, --mode=MODE   set file mode (as in chmod), not a=rwx - umask
  -p, --parents     no error if existing, make parent directories as needed
  -v, --verbose     print a message for each created directory
  -Z                   set SELinux security context of each created directory
                         to the default type
      --context[=CTX]  like -Z, or if CTX is specified then set the SELinux
                         or SMACK security context to CTX
      --help     display this help and exit
      --version  output version information and exit
```

### Exercise 1.2:

Look up help for a few other common commands by adding `--help` like you did for `mkdir` above. Some example commands to 
try: `mv`, `cp`, `rm`. Any others you can think of?

## Part 2: Basic Commands

### Exercise 2.1: mkdir

The `mkdir` command is used to make a new directory. Let's start by making a new directory to do our lab exercises in. 
Type `mkdir linux_lab` into the command line and press enter.

```commandline
root: mkdir linux_lab
```

### Exercise 2.2.1: ls

The `ls` command lists information about files and directories (current directory is the default directory for this, 
more on that later). Type `ls -la` into the command line and press enter. You should see a listing of files and 
directories in the current directory including the new `linux_lab` directory you just created in the exercise above.

```commandline
root: ls -la
total 76
drwxr-xr-x   1 root root 4096 Mar 15 16:52 .
drwxr-xr-x   1 root root 4096 Mar 15 16:52 ..
-rwxr-xr-x   1 root root    0 Mar 15 16:29 .dockerenv
drwxr-xr-x   2 root root 4096 Mar 15 16:52 linux_lab
```

**BEFORE MOVING ON:** if you do not see the directory `linux_lab` in your file listing go back to *Exercise 2.1* and try 
again. 

### Exercise 2.2.2: ls options

The options `-la` used in the previous exercise do the following: `l` provides a more descriptive long listing, `a` 
ensures all files including config files that are usually hidden are listed. I typically always use these two options 
when running the `ls` command. Try running the `ls` command with the following options to see the difference in output:

- `ls`
- `ls -a`
- `ls -l`

### Exercise 2.3: pwd

The `pwd` command mean "present working directory". It will give you the absolute path to the directory you are 
currently in. Type `pwd` into the command line and press enter. You should get a return like the one below telling you
where you are currently at in the file system.

```commandline
root: pwd
/var
```

### Exercise 2.4: cd

The `cd` command means "change directory". Let's now change directory into our `linux_lab` by typing `cd linux_lab` and 
pressing enter:

```commandline
root: cd linux_lab/
```

Now run the `pwd` command to see that our current directory is now the `linux_lab`.

```commandline
root: pwd
/var/linux_lab
```

### Exercise 2.5: touch

The `touch` command creates a new file. Let's create a new files from the command line. Enter the command 
`touch file1.txt` and press enter.

```commandline
root: touch file1.txt
```

Now run the `ls -la` command to see the new file in our current directory.

```commandline
root: ls -la
total 16K
drwx------ 1 root root 4.0K Mar 15 17:19 .
-rw-r--r-- 1 root root    0 Mar 15 17:19 file1.txt
```

**BEFORE MOVING ON:** if you do not see the file `file1.txt` in your file listing go back to *Exercise 2.5* and try 
again. 

### Exercise 2.6: cp

The `cp` command copies a file to a new location. Let's start by creating a new directory by typing `mkdir example_dir_1`
and pressing enter.

```commandline
root: mkdir example_dir_1
```

Now run the `ls -la` command to see the new directory.

```commandline
root: ls -la
total 20
drwx------ 1 root root 4096 Mar 15 17:22 .
drwxr-xr-x 2 root root 4096 Mar 15 17:22 example_dir_1
-rw-r--r-- 1 root root    0 Mar 15 17:19 file1.txt
```

Let's now copy the file `file1.txt` into the new `example_dir_1`. Type `cp file1.txt example_dir_1/` into the command line 
and press enter.

```commandline
root: cp file1.txt example_dir_1/
```

Run the following `ls` commands. You will see that there is a `file1.txt` in your current directory AND a duplicate of
it in the `example_dir_1` directory.

- `ls -la`
- `ls -la example_dir_1/`

### Exercise 2.7: mv

The `mv` command is a lot like the `cp` command except that it moves the file rather than copying it. Let's start by
creating a new file. Type `touch file2.txt` into the command line and press enter. 

```commandline
root: touch file2.txt
```

Now run the `ls -la` command to see the new file in our current directory.

```commandline
root: ls -la
total 16K
drwx------ 1 root root 4.0K Mar 15 17:19 .
drwxr-xr-x 2 root root 4096 Mar 15 17:22 example_dir_1
-rw-r--r-- 1 root root    0 Mar 15 17:19 file1.txt
-rw-r--r-- 1 root root    0 Mar 15 17:29 file2.txt
```

Let's move the file into our `example_dir_1` and observe the difference between `cp` and `mv`. Type `mv file2.txt 
example_dir_1/` and press enter. 
 
```commandline
root: mv file2.txt example_dir_1/
```

Run the following `ls` commands. You will see that there is a `file2.txt` is no longer in your current directory. You 
should see it in the listing for `example_dir_1` though.

- `ls -la`
- `ls -la example_dir_1/`

**BEFORE MOVING ON:** if you do not see the file `file2.txt` in your file listing for `example_dir_1` go back to 
*Exercise 2.7* and try again.

### Exercise 2.8: rm

The `rm` command removes a file. From the command line type `rm file1.txt` and press enter.

```commandline
root: rm file1.txt
```

Now run the `ls -la` command to see that `file1.txt` has been deleted from our current directory.

```commandline
root: ls -la
total 16K
drwx------ 1 root root 4.0K Mar 15 17:19 .
drwxr-xr-x 2 root root 4096 Mar 15 17:22 example_dir_1
```

### Exercise 2.9: rm -f / rmdir

Both `rm -r` and `rmdir` do the same thing. They will delete a directory and all its sub-directories and files. Type
`rm -r example_dir_1` into the command line and press enter.

Now run the `ls -la` command to see that `example_dir_1` has been deleted from our current directory.

```commandline
root: ls -la
total 16K
drwx------ 1 root root 4.0K Mar 15 17:19 .
```

## Part 3: Finding Files and Directories

## Part 4: PATH Environmental Variable

## Part 5: Hard and Soft Links

## Part 6: Permissions

## Part 7: Umask