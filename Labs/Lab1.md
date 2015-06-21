#CSCI 211 - Lab 1
##Introduction to Linux and the g++ Compiler

##Goals:

* Overview: Linux organization
* Introduce several basic Linux commands
* Provide an example of creating, compiling, and running a c++ program
* Set up all the directories for the course assignments
* Provide practice creating, compiling, and running c++ programs

##BUSY WORK DISCLAIMER:

Some teachers (especially in high school) waste your time with busywork.

The tasks I ask you to perform are to teach you information and skills that you must have to do well in computer science.  If you learn what I'm showing you, it will save you lots of time throughout the semester.

If you take the attitude "I just want to get done with this busy work so I can leave" it is unlikely that you will be able to complete CSCI, CINS, or EECE.  This lab, the other labs, and the assignments are not meant to keep you busy, they are meant to teach you want you need to know to be successful.

Paying attention, learning, and understanding how things work is difficult.  If you do not want to pay attention, learn, and understand how things work, I strongly recommend you do not major in CSCI, CINS, or EECE.


##Lab Attendance/Grade

Part of your lab grade is based on attendance.  I will take role after my lecture.  If you finish the assignments AND turn them into [turnin](https://turnin.ecst.csuchico.edu/ "Tyson's Turnin"), then you may leave early.  Speak to me if you need to leave early but have not finished the assignments.  **Students who leave early without turning in that weeks assignments will NOT get credit for attending lab.**

##Getting your ecst computer account
(skip this if you already have an ecst account)

In order to log on to the computers in the 211 lab (OCNL 244), you must have an ecst (Engineering College) account.

This is different than the university account (often called a Wildcat account, or University Portal account).

If you have never had an ecst account you can create one by visiting the account creation page.  It will take about 1 business day for your new account to become active.

If you already have an ecst account but your forgot your password, you must go to the system administrator's (Elbert Chan) office hours:  OCNL 249 Monday - Friday 4:00 - 5:00.  You will need your student ID.

If you don't have an account, you can log in with username & password as "student"  However, you will not be able to save any of your work.


##Using the Linux Computers in OCNL 251

The computers in OCNL 251 are running the Linux operating system (the Ubuntu distribution with the xfce window manager).  They are stand-alone computers except your home directory is on a shared file server in Butte Hall.  This means all your files will be available no matter which machine you use (or if you log in remotely to jaguar.ecst.csuchico.edu from home using ssh or putty).

SOMETIMES the network file links (one for home directories, one for web directories) between the 251 lab computers disconnect.  The only way to reset them is to reboot the computer.  If you can't access your home directory or my directories, the links probably failed and you should reboot the computer.


##Lecture Notes:

###[Linux Tutorial (recommended for everyone)](http://ryanstutorials.net/linuxtutorial/)

###Linux Overview
	* Kernel
	* Shell  (csh, tsh, ksh, bsh, bash)
	* Windowing System (X-windows is the most common)
	* Windows Manager (Xfce, KDE, Gnome, etc)

###Linux Command structure

Commands in the Linux environment all have textual names.  Instead of opening a window that shows the content of a directory you type a command at a prompt in a window.  For example, the command "ls" show the contents of the current directory.  A program called the shell will print a prompt (usually a "$" but can be anything you want) to indicate that it is ready for you to type a command.

When you type a command the shell looks for a program with that name to execute.

<pre>
$ ls
</pre>
shell looks for an executable file named "ls" in the special collection of directories (called the path)

Why text better than clicking buttons?  Consider the problem of editing a group of files.  For example, I have a bunch of files with "112" in them and I need to change the "112" to "211"  The following command changes 112 to 211 in all the .html files in the current directory:

<pre>
$ for file in *.html; do sed s/112/211/g &lt; $file &gt; tmp; mv tmp $file; done
</pre>

While it may take some time before you can write such complicated commands, once you learn how to use a text based command shell it is much faster than using a point-and-click interface.

####Know What You are Doing

Linux assumes that you really want to do what you say you want to do.  In other words, if you use the remove command to delete a file, the file will be deleted.  It won't be put into the trash, it will be deleted.  Once a file is deleted, it is deleted forever (system backups are done every night, so if the file existed the previous night you can get a copy from the backups).

####Special Keys

* ^C kill the current process

* ^D End of input (end of file) character
When you want to tell a program you are done entering input, type ^D

* ^Z Stop the current process (the process will still exist, but it won't be running).  Don't do this until you understand how to restart processes (commands: jobs, fg, bg).


####File Redirection

Programs usually write to the current window.  For example, if your program has the following line:  cout << "hello\n"   hello will be written to the current window.

You can tell the bash shell to redirect standard output (i.e. cout) to a file

<pre>
	$ hello_world > hello_world.myout
</pre>

Now when the program hello_world is run, text written to standard output will be place in the file hellow_world.myout

Programs usually read from the keyboard.  For example, if your program has the following line:  cin >> value;   the number typed at the keyboard will be placed into the variable value

You can tell the shell to redirect standard input (i.e. cin) from a file

<pre>
	$ add < test_1.in
</pre>

Now when the program add is run, text read from standard input (cin) will be read from the file: test_1.in

####Linux Pipes

One of the most powerful features of the bash shell is the ability to connect the output of one command to the input of another command.  Consider these two commands:

<pre>
	$ ls    this will list all the files in the current directory
	$ wc    this will count all the characters, words, and lines in the input
</pre>

If we take the output of ls and connected it to the input of wc (we say "pipe the output of ls to the input of wc") we can find out how many files are in the current directory

<pre>
	$ ls | wc
</pre>

The | is usually on the key above the Enter key.

Any number of commands can be pipped together.

####Common Linux commands

| Linux Command     | Command Details     | Examples |
| :------------- | :------------- | :-------- |
| cd       | change directory<br> ~ is used to mean your home directory<br>	.. is used to mean the parent of current directory       |$ cd  <br>change to your home directory <br>$ cd  ~user      <br>change to specified user's home directory   (e.g.   $ cd ~tyson) <br> $ cd  ..             <br>change to the parent of the current directory (the directory above the current directory) <br>	$ cd  211       <br>  if "211" is a sub-directory of the current directory, change to it|
|ls | list the files in the current directory | |
|pwd |	show the current directory (called the path)| |
|mkdir | make a new directory|$ mkdir 211     <br>       make a new directory in the current directory called "211" <br>$ mkdir ~/211   <br>      make a new directory in your home directory called "211" |
|chmod | change the protection (access) of a file or directory if you change the protection of your home directory as follows, no one will be able to access any of your files | $ cd ~/ <br>                         change to your home directory <br>$ chmod 700 .  <br>       don't forget the dot (.) t the end of this command |
|rm |	delete a file <br> rm -r allows you to delete a directory and everything in it, use it carefully | |
|cp | copy a file | |
| man | show the manual page for a command | $ man cp <br> the -k option searches for keywords in all man pages (useful if you forget the name of a command) <br> $ man -k copy <br> usually this produces too many matches and they scroll by too fast to read <br> $ man -k copy \| less <br> Note:  the apopos command does the same thing as "man -k" <br> $ apopos copy \| less |
|which| tells you which executable is executed when you type a command |$ which cp |


####Linux editors:

For 211 we will not be using an integrated development environment (IDE).  The reason we are not using an IDE is because I want you to develop a good understanding of the tasks performed by an IDE.  Once you understand these tasks well you can switch to an IDE.

When writing programs without an IDE you use a stand alone editor to create your program (vs. using the editor built in to Visual C++). This means you can pick from hundreds of available editors.  Here are some common choices (most are available on the computers in 251):

* SciTE:  Menu based editor that is easy to use.  Similar to notepad.  Can download on your home machine so you can use the same editor at home as you use in lab.  Cannot use over text-based connections (like putty)  (actually there is a way to use it but it takes work to set up).
* nano:  Simple text based editor (no mouse), all the commands are always on the screen (on some platforms a similar editor called pico is available and nano is not). You can use nano via a text-based connection (like putty).
* gvim: Graphical version of  vim (see below).  A little harder to learn how to use.
* vim : Powerful and very popular version of the popular vi editor.  Works on most Linux and Microsoft platforms.  It is hard to learn how to use but very fast once you learn how to use. Vim Homepage
* emacs: Powerful and very popular editor.  It is hard to learn how to use but provides powerful tools once you learn how to use it.  Works on most Linux and Microsoft platforms GNU's emacs page
* sublime: Graphical paid editor favorite of many upper class students and is a great editor.
* Atom: New open source graphical editor from GitHub, offers plugins including ones that allow you to connect to SFTP connections and remotely edit code on lab machines from home.

All these editors works from the command line:

<pre>
	$ SciTE hello.cpp &
</pre>

**NOTE: SciTE in OCNL 251 is broken and cannot create a new file.  You have to create the file BEFORE you edit it:**

<pre>
	$ touch hello.cpp
	// the touch command will create a new file if the given file does not exist
	$ SciTE hello.cpp &
</pre>

Note:  The & at the end of this command tells the shell to create a new process to run the given command.  That means that while the editor window is running you can continue to use the command prompt.

All of these are available on Linux and MacOS.  Vim and Emacs are hard to learn, so if you don't already know one, I suggest you start using SciTE.  In a couple weeks I will give lab on vim.

If you plan to use Putty to do your assignments at home (not recommended), then vim or nano is a better choice (it requires some extra setup to use gvim or SciTE over putty).

Whatever editor you end up using, become an expert.

##Turning in Lab Assignments

Some of the lab exercises must be turned in using [turnin.ecst.csuchico.edu](https://turnin.ecst.csuchico.edu/ "Tyson's Turnin") (see instructions for [turning in file](https://github.com/CSUChico-CSCI211/CSCI211-Course-Materials/blob/master/Assignments/Turnin.md "How to Turnin")) for you to get credit.  For this lab you must turn in files for exercises 4 and 5.  At the end of each exercise I will indicate what files must be turned in.

My goal is to provide assignments that you can complete during lab.  However, if you cannot finish the assignments during lab, you have until midnight on the Friday Saturday following lab to turn them in (most semesters the deadline is Friday, but since there is a Friday afternoon lab in Spring 2015, the deadline is Saturday; you should try to turn them in Friday, it is easy to forget about assignments due on Saturday).

Some of the lab exercises do not have to be turned in.  Usually these assignments provide the information you need for subsequent lab assignments and programming assignments.  I strongly suggest you complete all lab assignments.

##Exercise 1: Setting up your 211 environment

The following steps set up the directories for the entire semester.  Make sure you follow the instructions carefully.

These instructions will work on the lab computers AND on your Linux/OSX laptop/desktop.  If you have your laptop today and plan to bring it to every lab, you can follow these instructions only on your laptop.  If you do not plan on bringing a laptop to lab, log in to a lab computer and then follow these instructions.

The following will create two directories "211" and "bin" in the directory in which you execute these commands.  Life will be much easier if you do this in your home directory (either on the Department's computer or on your own laptop).  After the semester you can move the directory to a different location.  You can also create a symbolic link (shortcut) from another directory.

When I provide a "$" with some text after it, type that text (a command) into the shell.  When typing commands DO NOT type the // or the text after the //

<pre>
	$ cd                // go to your home directory
	$ chmod 700 .       // change the protection so no one can steal your files (you can skip this on your laptop)
</pre>


There are three methods to download the needed file.  If your computer has the utility wget, use the first.  Otherwise use the second.

* Method 1: your computer has the wget command (type "which wget" at the $, if a filename is printed then wget is installed)

<pre>
	$ wget www.ecst.csuchico.edu/~tyson/211/downloads/211.tar     // copy 211.tar from my web page to current directory
</pre>

* Method 2: your computer does not have wget

<pre>
$ sftp USERNAME@jaguar.csuchico.edu    // USERNAME must be your ecst username
</pre>

If you get an error message, type this command  ($ rm .ssh/known_hosts) and retype the above sftp command
If you don't get an error message, you should be prompted for your ecst password
Once you log in you will see the sftp prompt "sftp> "
For the following, type everything after the "sftp> "

<pre>
	Connected to jaguar.ecst.csuchico.edu.
	sftp> cd /user/faculty/tyson/211/downloads   // change directory on jaguar to the 211 downloads directory
	sftp> get 211.tar                            // copy the file "211.tar" from jaguar to your computer
	...
	sftp> quit                                   // exit sftp
</pre>

* Method 3: use a web browser

Save the file 211.tar into your home directory (simply clicking on 211.tar will download it to your downloads directory, move it to your home directory).

While this might seem like the easiest method, knowing both wget and sftp is very worthwhile.

The "tar" file you just downloaded is like a .zip file.  It contains all the directories and files you need this semester.
When expanded it will create a directory called "211"  If you already have a directory or file named "211" you must rename it

<pre>
	$ mv 211 211.old           // only do this if you already have a 211 directory or file
</pre>

Unpack 211.tar (this creates the directory 211 with a subdirectory for each assignment)

<pre>
	$ tar -xf 211.tar          // extract all the directories and files
	$ ls                       // you should see the directories "211" and "bin"
	$ ls 211                   // you should see a bunch of lab and project directories
	$ cd 211/lab01_hello       // change to the directory for the following exercise
</pre>

If you are working on a computer in the lab, you can repeat this process on your home computer/laptop.  You can copy files to/from jaguar and your home computer/laptop using sftp.

##Exercise 2: Creating, compiling, and running a C++ program

For this lab you will be writing three programs.  It is a very good idea to put each program in its own directory.  If you get in the habit of putting each program in its own directory you will save time later in the semester.  I regularly see students waste time because they attempt to put multiple programs in one directory.  The above step created three directories for lab 1:  ~/211/lab01_hello  ~/211/lab01_print  ~/211/lab01_add.

In your directory for lab 1 hello (~211/lab01_hello if you follow my instructions above), create the file hello.cpp (use any editor, I recommend that you use scite if you don't know vim (use vim if you know vim)).  Start the editor with "hello.cpp" as the filename:

<pre>
$ touch hello.cpp     // only in OCNL 251 because SciTE is broken
$ SciTE hello.cpp &
</pre>

the & starts the process in the background and allows you to use the editor AND the command window at the same time

-or-

<pre>
$ vim hello.cpp
</pre>

Now edit the file so it contains the following text.  Save the file and exit the editor.

<pre>
	#include <iostream>
	using namespace std;

	int
	main()
	{

		cout << "hello world" << endl;
		return 0;

	}
</pre>

Compile this file using the command:

<pre>
	$ g++   hello.cpp
</pre>

if you got an error, use the editor to fix the error

This should have created the file a.out, use "$ ls -l" to find out if a.out is in your directory.  Notice that a.out automatically has execute protection ("x").  When a file has execute permission you can execute it.

<pre>
	$ ls -l a.out
</pre>

Run your hello program.  You can execute the program by typing a.out at the Linux prompt.

<pre>
$ a.out
</pre>
If a.out doesn't work, try ./a.out.  If "./a.out" worked and "a.out" did not work, read about how to fix your path.

You do not have to turn in this exercise.  The following two exercises must be turned in.

##Exercise 3: Write a program that reads two numbers, adds them together, and prints the result

Change the directory to your lab01_add directory

<pre>
	$ cd ../lab01_add
</pre>

If that did not work, try using the "full directory path" or "full path"

<pre>
	$ cd ~/211/lab01_add
</pre>

When your program is run, it should work like this (the "a.out" "40" and "2" are typed by the user; the "40 + 2 = 42" is printed by the program):

<pre>
	$ a.out
	40
	2
	40 + 2 = 42
	$
</pre>

For this exercise you will need to read in an integer.  You can read an integer in C++ like this:

<pre>
	cin >> value1;
</pre>

Where "value1" has been declared as an integer before this line (C++ integers are declared just like in Java).

Create a new file called add.cpp using an editor.  Write the add program so it reads and adds the two numbers.

Compile and run your program to make sure it works correctly.  Your output must EXACTLY match my output (&lt;number&gt;&lt;space&gt;&lt;+&gt;&lt;space&gt;&lt;number&gt;&lt;space&gt;&lt;=&gt;&lt;space&gt;&lt;number&gt;&lt;newline&gt;)

Some sample input and output are available in your lab01_add/tests directory.

<pre>
	$ ls tests
	t01.in  t01.out  t02.in  t02.out  t03.in  t03.out
	$
</pre>

In this directory you will find files like t0.in1 and t01.out.  t01.in is the input for your program and t01.out is the expected output.  I will use all the tests in this directory to grade your program.  If you pass these tests you will get full credit (these are the same tests used when by turnin.ecst.csuchico.edu).

An easy way to see the content of a small file is to use the Linux cat command:

<pre>
	$ cat tests/t01.in
	40 2
	$ cat tests/t01.out
	40 + 2 = 42
	$
</pre>

See [Introduction to Testing](https://github.com/CSUChico-CSCI211/CSCI211-Course-Materials/blob/master/Assignments/Testing.md "Testing") for full description of how to test your assignments.  If you understand the described mechanism now, it will make your semester much easier, and will improve your grade.  One of the most important aspects of this lab is for you to understand the testing mechanism.

Once your program is working, turn add.cpp in on [turnin.ecst.csuchico.edu](https://turnin.ecst.csuchico.edu/ "Tyson's Turnin").  See instructions for [turning in files.](https://github.com/CSUChico-CSCI211/CSCI211-Course-Materials/blob/master/Assignments/Turnin.md "How to Turnin")

You must pass all the posted tests to get credit for a lab assignment.

Lab exercises are due midnight the Saturday night following lab.

##Exercise 4:  Write a program that reads a number and prints "hello" that number of times:

<pre>
	$ a.out
	5
	0 hello
	1 hello
	2 hello
	3 hello
	4 hello
	$
</pre>

All the characters shown above were printed by the program, except the 5<enter> which was typed by the user.

Change directory to the lab01_print directory.  Create a new file called print.cpp.

Use a for loop to implement this program.

When your program is working, test it with the posted tests (see the testing and turn in instructions for exercise 3; the only difference is that the tests are in the directory lab01_print/tests).

Make sure your program passes all the tests.

Turn in print.cpp to [turnin.ecst.csuchico.edu](https://turnin.ecst.csuchico.edu/ "Tyson's Turnin").

##Exercise 5: Make sure you understand the [testing mechanism](https://github.com/CSUChico-CSCI211/CSCI211-Course-Materials/blob/master/Assignments/Testing.md "Testing")

The main point of these assignments is to introduce you to the testing mechanism.

Students who don't understand how < and > are used to test assignments struggle throughout the semester.

##Exercise Deadline

All labs are due at 11:59pm the Saturday following lab.  For this lab you must turn in add.cpp and print.cpp.

If you are not able to complete all the exercises, turn in your partial work for partial credit.
