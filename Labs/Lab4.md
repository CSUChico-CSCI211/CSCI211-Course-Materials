#CSCI211 - Lab 4
##Introduction to the GNU Debuggers gdb/ddd

##Goals

* Learn the basics of gdb and ddd so you can use them to find bugs in your class projects.

##Required Survey

You do not have to turn in any files for this lab but you do have to [complete this survey.](http://goo.gl/forms/5d4cIFwdst "Lab4 Survey")

The survey is worth 3 points.

##gdb/ddd Lecture Notes:

gdb is a program debugger.  It allows you to examine a program while the program is executing.  The interface to gdb is textual (just like the interface to the bash shell is textual).  You control gdb by typing textual commands at its prompt (the gdb command prompt is "(gdb)").

ddd provides a graphical user interface for gdb.  The user can control gdb by pressing buttons and making menu selections.  It also contains the ability to illustrate data structures (such as a linked list) using diagrams.

Both gdb and ddd are available on Linux, OSX (must install using homebrew, see note below), and Cygwin (sometimes they don't work well on Cygwin).

You can learn about gdb and ddd using the man command

<pre>
	$ man gdb
	$ man ddd
</pre>

Complete gdb documentation is at [gdb manual.](http://www.gnu.org/software/gdb/documentation/ "GDB Manual")

Complete ddd documentation is available on [ddd's homepage.](http://www.gnu.org/software/ddd/ "DDD Documentation")

ddd is easier to use in that it provides a nice menu and shows the codes being executed.  However, it has a lot of features that may seem overwhelming at first.  I suggest you try gdb first using the few simple commands listed below.  Once you have a good idea how gdb works, you can use ddd. Once you understand the concepts of debugging, you will probably prefer use ddd to debug your programs.

##Starting gdb (and ddd)

1. Compile your programs with the -g option.  All .o files and the final linking must have the -g option.  The -g option tells the compiler to put extra information (such as variable names) into the executable so a debugger can access them.

2. At the command prompt type gdb (or ddd) followed by your executable name
<pre>
	$ g++ -g -o p1 p1.cc

	$ gdb p1
	GNU gdb (GDB) 7.1
	Copyright (C) 2010 Free Software Foundation, Inc.
	License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
	This is free software: you are free to change and redistribute it.
	There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
	and "show warranty" for details.
	This GDB was configured as "x86_64-slackware-linux".
	For bug reporting instructions, please see:
	<http://www.gnu.org/software/gdb/bugs/>...
	Reading symbols from /user/faculty/tyson/tmp/lab06/p1...done.
	(gdb)
</pre>
3. (gdb) is the prompt for gdb.  There are lots of commands that you can type here.  For example, if you type run, your program will start executing.

The following table lists the most commonly used gdb commands (these are the most basic commands, this is NOT a complete list).

|Command|Shortcut|Description|
|:------|:-------|:----------|
|quit|q|quit the debugger and exit.  If a program is running it will ask you if you still want to quit.
help|h|W/o and argument lists help topics.  If followed by a command, will describe that command:  e.g. help run|
|run|r|Start running the current program.  May be followed with command line arguments:  e.g.   run < t01.in|
|print|p|Print the given variable.  For example, if there is a variable i in the current context, "print i" will print the value of i.|
|list|l|List the C++ code for the currently executing instruction.  List advances through the code each time it is called.|
|list 42|l 42|Lists the code at line 42 (you may pass any number here)|
|where|where |Prints the current line number and all the functions that were called to get there (prints the run time stack).|
|up|up|Move up to the function that called the current function (move up the run-time stack, see where above). For example, if main() calls foo() and gdb is stopped in foo(), the up command will move gdb's focus to main() so you can see what was going on in main().|
|down|d|Move down the run time stack (see up and where).|
|break|b|Set a breakpoint.  Must specify a line number for the current file, or filename:line for another file|
|step|s|Execute one and only one line of code.|
|next|n|Same as step, but skips over function calls.|
|finish|f|Execute until the end of the current function.|
|continue|c|Continue execution until the next breakpoint or until the end of the program.|

##Exercise Setup:

**MACINTOSH NOTE:**  You cannot do this lab *natively* on a Mac unless you have GNU's g++ and gdb installed.  These are no longer part of xcode, you have to download and install them using homebrew.  It takes over an hour to install g++ using [homebrew.](http://brew.sh/) I recommend using a Debian Linux VM using VMware that is provided for free by the department through the same store portal as Dreamspark that you should have enrolled into when you created your ECST account. I also enroll all my students at the start of the semester, let me know if you didn't get the email or enrolled late as I might need to manually add you.

Tyson has created several sample programs for you to use with the debugger.  They should be in your 211/lab04_gdb directory.

You can compile all the programs with one call to make:

<pre>
	$ cd ~/211/lab04_gdb
	$ make
</pre>

make should not issue any errors, let me know if you get errors.

You don't have to turn anything in for this lab but you must complete this [google survey.](http://goo.gl/forms/5d4cIFwdst "Lab4 Survey")

##Exercise 1:

run gdb with the executable p1

<pre>
	$ gdb p1
</pre>

type run at the (gdb) to run this program

**ON SURVEY:**  What error causes this program to terminate?
**ON SURVEY:**  On what line does this program crash?

type list at the (gdb) to list the source code

**ON SURVEY:**  Explain the defect in the program that causes this problem.

type quit at the (gdb) to quit the debugger

##Exercise 2:

run gdb with executable p2

<pre>
	$ gdb p2
</pre>

type run at the (gdb) to run this program

type where at the (gdb) to see the list of functions that were called

**ON SURVEY:** What error caused this program to terminate?
<br>
**ON SURVEY:**  What functions were called before the program crashed?

notice that the where command told you the arguments to the functions f() and g()

you can use the print (p) function to print the values of a variable:

<pre>
	(gdb) p b
	$1 = 52
</pre>

**ON SURVEY:** What is the address of the variable b?

gdb is currently pointing to the code in function f().  If you use the up command it will be pointing at the code in the function that called f().

Use the up command to go to the function that called f().

**ON SURVEY:** What is the address of the variable a?


##Exercise 3:

run ddd with the executable p3

	$ ddd p3

press the run button or type run at the (gdb) to run this program

ON SURVEY: Explain why this program has a segmentation fault.

Try printing the different variables:

	(gdb) p cur
	(gdb) p *cur

Alternatively, you can double click on the "cur" in the text window.

Here are some hints if you can't figure it out:

You can find the error by watching the execution of the insert function.

Insert a breakpoint at the first line of the insert function

	(gdb) break 25

now start the execution over again: press the run button to type

	(gdb) run


the execution will stop at line 25 (the breakpoint you set) when insert is called for the first time
Notice the stop sign where the debugger stopped executing

use the where command to see the run time stack
	Linked_list::insert() was called from line 41
	its argument i = 1

use the list command to see the code

try printing the different variables using the print command (or by double clicking on the variables)

	hint:  the variable this points to the current object, try printing this and *this


Exercise 4:

Program p4 is the same program as p1 but is compiled w/o the -g option

run gdb with the executable p4

	$ gdb p4

run the program

type typing where at the (gdb)

ON SURVEY: What is different about running p4 with gdb than running p1 with gdb?

ON SURVEY: Is the p1 executable smaller or larger than the p4 executable?


After completing the exercises and the survey, you may work on the Video List assignment (p3)
