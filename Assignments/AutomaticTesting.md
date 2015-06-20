#How to Test Assignments Automatically
These instructions work for most of the assignments in this class and for most of the assignments in Tyson's classes. These instructions as well as the [Introduction to Testing](https://github.com/CSUChico-CSCI211/CSCI211-Course-Materials/blob/master/Assignments/Testing.md "Introduction to Testing") instructions were taken from Tyson's 211 class. 

##Automatic Testing Mechanism
This is the same mechanism used by [turnin.ecst.csuchico.edu](https://turnin.ecst.csuchico.edu)

With most assignments you can use the run_tests bash script to automatically test your program.  A bash script is a program that can be executed by the bash shell.  It is a normal text file just like a .cpp file.

This script uses the method describe in [Introduction to Testing](https://github.com/CSUChico-CSCI211/CSCI211-Course-Materials/blob/master/Assignments/Testing.md "Introduction to Testing"); if you did not read and understand this description be prepared for lots of frustration and poor assignments grades.

The run_tests script must be placed in the directory that contains your program.  There must also be a subdirectory called tests that contains all of the sample tests (copied from or downloaded from the course web-page).

Most assignments have a test directory (e.g. ~tyson/211/tests/p2 for 211's p2 assignment).  In this directory there is a tape archive file (.tar) that contains the tests directory and the run_tests script.  Here are the steps for using it:

This example is for 211's p2.  Replace the "211" with your course and the "2" with the current assignment number to use this method on other assignments.

1.  Copy the file p2_tests.tar from the tests/p2 directory to the directory containing your program.
(see how to download files to copy my files to your current directory)

2. Expand the tar (tape archive) file (works the same on Linux, Cygwin, Mac)
<pre>
	$ tar -xvf p2_tests.tar
</pre>
This will create a sub-directory called tests with all the tests in it and create the run_tests script

3. If you did not download the run_tests script during the first lab (it would be ~/bin/run_tests), download it and put it into your ~/bin directory (create a new directory if it does not exist).<br><br>Name the file run_tests and give it execute permission:
<pre>
	$ cd ~/bin
	$ chmod 700 run_tests
</pre>
Update your PATH so it includes your ~/bin, but use your entire directory path (for example, my home directory is /home/bryan, so I want to add /home/bryan/bin to my PATH)<br><br>You can set your PATH variable in your ~/.bashrc file (Linux) or your ~/.bash_profile (Mac OS).  Create the file if it does not exist.  An example of what you would add to this file:
<pre>
	PATH=$PATH:/home/bryan/bin
</pre>
no spaces, use your home directory, not my home directory
4. Run the run_tests bash script followed by the name of the executable (this example assumes the executable is called "videos").  The bash script will create a results directory with the results from your program.
<pre>
	$ run_tests videos
</pre>
If this does not work, try the following
<pre>
	$ chmod 700 run_tests
	$ run_tests videos
</pre>
If this does not work, try the following
<pre>
	$ ./run_tests videos
</pre>
If this does not work, send your instructor e-mail.


##Understanding failed tests

Each test is made up of one to five files.  For example, the t01 test can contains the files:
<pre>
	tests/t01.out     this is the output your program is expected to write to standard output (cout)
	tests/t01.in       optional, only exists if assignment requires your program to read input from standard input (cin)
	tests/t01.err      optional, only exists if assignment specifies errors be written to standard error (cerr instead of cout)
	tests/t01.exit    optional, only exists if assignment specifies the exact exit status your program should return (the value returned from main())
	tests/t01.cmd   optional, only exists if assignment requires the reading of command line arguments (p5 in 211)
</pre>

When the run_tests script runs a test it redirects the input file (tests/t01.in in this example) to the program and using file redirection creates the following result files:
<pre>
	results/t01.myout     always created
	results/t01.myerr      only created if tests/t01.err exists
	results/t01.myexit    only created if tests/t01.exit exists
</pre>
Then the run_tests script compares your output files (which are in the results directory) with the correct output files (which are in the tests directory).  The diff utility prints nothing if the given two files are the same.  It prints the differences if they are not the same (see [Introduction to Testing](https://github.com/CSUChico-CSCI211/CSCI211-Course-Materials/blob/master/Assignments/Testing.md "Introduction to Testing")).
<pre>
	diff results/t01.myout  tests/t01.out
	diff results/t01.myerr  tests/t01.err     if these files exist
	diff results/t01.myexit tests/t01.exit   if these files exist
</pre>
If your output files are the same as the correct output, run_tests will print that you passed the test.  If one, two, or all three of your output files are incorrect, run_tests will print that you failed test and tell you for which output you fails:
</pre>
	stdout   (standard output, the .out file)
	stderr   (standard error, the .err file)
	exit      (the exit status returned from your program, the .exit file  (the value returned from main()))
</pre>
If you fail a test you can look at the files in the tests and results directories.  For example, if you fail t01 because the stdout was incorrect, compare tests/t01.out with results/t01.myout
<pre>
	$ diff tests/t01.out results/t01.myout
</pre>
If you know how to use vim, you can use the vimdiff utility.  It shows the two files side-by-side and highlights the differences.
</pre>
	$ vimdiff tests/t01.out results/t01.myout
</pre>
vimdiff will highlight the differences.  You can move around the files using the arrow keys and exit with the command    :qa<enter>

Tyson provides two scripts ([vd]("http://www.ecst.csuchico.edu/%7Etyson/classes/bin/vd vd") and [vde](http://www.ecst.csuchico.edu/%7Etyson/classes/bin/vde vde")) that start vimdiff for you.  Read the comments at the top of the scripts to see how they work.  In order to use these scripts you will need to put them in a directory in your path and give them execute permission

<pre>
	$ cd
	$ mkdir bin
	$ cd bin
	$ cp ~tyson/211/bin/*  .            // if you are working at home download them and set the permission: $ chmod 700 ~/bin/vd ~/bin/vde
</pre>
Now edit your path so it includes your ~/bin directory.

If you don't understand this process, you will not be able to figure out why your program fails tests.  For example, you turn in your assignment to turnin.ecst.csuchico.edu and it reports that you failed tests t03.  If you don't know to compare results/t03.myout to tests/t03.out you will not be able to fix your program.


**Understanding this mechanism will save you a lot of time and significantly improve your grade.**


##Testing Programs that Read from Files

Some programs (e.g. p5 in 211 and programs in 311) will require you to read from a file instead of from standard input (that is, opening a file instead of reading from cin).  For these program the .in file is not redirected to the program's standard input; it is assumed to be the inputfile that the program will read.  Such program must use command line arguments (which are specified in a .cmd file) to specify the input file.  Consider the following example.  This program reads everything in the input file (named tests/t01.in in this example) and writes it to standard output.

<pre>
	t01.out
		hello world
	t01.in
		hello world
	t01.cmd
		tests/t01.in
</pre>

To manually run this test you would type the following command (this assumes your program is called a.out):

<pre>
	$ a.out tests/t01.in > results/t01.myout
</pre>

When this tests is run automatically (using run_tests), the contents of t01.cmd will become the command line arguments to the program.  Standard output and standard error will be redirected as described above.
