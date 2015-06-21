#CSCI211 - Lab 2
##Detecting End of Input, Using Standard Error, Returning from main()

##Goals of today's lab:

1. Review of how to test assignments (run_tests, vd, vde)
2. Learn how to detect end of input (also known as end of file or EOF)
3. Learn the syntax of the C++ switch statement
4. Learn how to write to standard error and learn the shell syntax for redirecting standard error to a file (described in exercise 2)
5. Learn how to ask the bash shell for the exit status of the last program executed

##Testing Assignments (the exams usually have questions on this material)

###Background

* PATH environment variable
* diff and vimdiff tools
* bash shell scripting
* file redirection
<pre>
	<        standard input (stdin)
	>        standard output (stdout)
	2>      standard error (stderr) (see Exercise 2 below)
</pre>
* exit status
<pre>
	return 0;
	return 1;
	echo $?
</pre>

###Manual Testing

<pre>
	$ videos < tests/t01.in > results/t01.myout 2> results/t01.myerr
	$ vimdiff results/t01.myout tests/t01.myerr
	$ vimdiff results/t01.myerr tests/t01.myerr
</pre>

###Tools

* run_tests
* vd
* vde
* https://turnin.ecst.csuchico.edu/        NOTE: only works for https, University firewall stops http requests.

run_tests, vd, and vde should be in your ~/bin directory (they are put there when you downloaded 211.tar in during the first lab).

<pre>
	$ cd
	$ cd bin
	$ ls run_tests vd vde
	run_test vd vde
</pre>

If these files are not there, download [them](http://www.ecst.csuchico.edu/~tyson/classes/211.f15/bin) to your ~/bin directory  (create ~/bin if it does not exist).

Once these files are in your ~/bin directory, make sure they work:

<pre>
	$ cd
	$ which run_tests
</pre>

If nothing is printed, follow the instructions on how to set up your path.

When your path is correctly set up, you will see this:

<pre>
$ cd
$ which run_tests
/home/bryan/bin/run_tests
</pre>

With the "/home/bryan" replaced with your home directory.

See [Introduction to Testing](https://github.com/CSUChico-CSCI211/CSCI211-Course-Materials/blob/master/Assignments/Testing.md "Testing") and [How to Test Assignments Automatically](https://github.com/CSUChico-CSCI211/CSCI211-Course-Materials/blob/master/Assignments/AutomaticTesting.md "Automatic Testing") for a detailed description of all of these.

##Detecting the end of input (often called EOF for "end of file")

**You must use this mechanism in exercise 1 below.  You will also use it in most of the assignments this semester.**

When you read using cin (e.g. cin >> my_integer) you can use **the value returned from "cin >>"** to detect the end of input.  Consider the following program (this program is called echo_ints.cpp and is in the src directory for this lab (~/211/lab02_echoints/echo_ints.cpp)):

<pre>
	#include <iostream>
	using namespace std;

	int main()
	{
	int value;

	// as long as we can read an integer from standard input (cin)
	// when the user enters control-D the "cin >> value" will return false
	while (cin >> value)
	{
	// write the integer just read to standard output
	cout << "value = " << value << endl;
	}

	// return 0 from main() if there are no errors
	return 0;

	}
</pre>

When the user enters an integer, the "cin >> value" expression returns true (recall that true is any non-zero value) and the body of the loop is executed.

When the user enters ^D (I use ^D to mean control-D), the "cin >> value" expression returns 0 and the loop is terminated (while loops terminate as soon as the expression is false).

Compile and run the program:

<pre>
	$ cd ~/211/lab02_echoints
	$ g++ -o echo_ints echo_ints.cpp       // what does the -o option do?
	$ echo_ints
</pre>

Now type some integers (each followed by pressing the enter key).

Now type ^D  (hold the control key and press the D key)

What did the ^D do?

When typing values at the command prompt you need to explicitly mark the end of input with a ^D.  When redirecting a file into a program, the ^D is automatic.

Create a file with some numbers in it.  An easy way to do this is to use the cat utility and file redirection .  The following creates a new file called "nums" with the values 1,2,3, and 4:

<pre>
	$ cat > nums
	1
	2
	3
	4
	^D
	$
</pre>

Now run echo_ints and redirect the file you just created as input.

<pre>
	$ echo_ints < nums
</pre>

What happens?  Why does the program stop executing?

How would you redirect the output of this program to another file?  Hint: it very similar to redirecting the input above.

At this point you should be able to do all the above tasks (compile a program, run a program, create a file using cat, and run a program using file redirection (the < filename and > filename)).  If you can't do all of these tasks without notes, go over the above commands (you will do these tasks all semester; it is important you can do them without notes).



##Exercise 1: Practice Detecting EOF and Using a Switch Statement

Write a program (to_text.cpp) that reads zero or more single digits positive integers (0,1,2,3,...,9), and prints the corresponding text string ("zero", "one", "two", "three", ... , "nine").  When the end of input is reached, exit the program.

Put this program in your ~/211/lab02_totext

$ to_text
1
one
2
two
3
three
^D
$

NOTE: when you type ^D you will NOT see it (it is not printed to the terminal).  I put it in the above example to make it clear that the end of input is signaled by pressing ^D.

To get credit, you must pass the posted tests (in your directory ~/211/lab02_to_text/tests and on the web at), and you must use a switch statement (the syntax of the switch statement is shown at the bottom of this web page).

You may start with my echo_ints.cpp program.

Turn in the file to_text.cpp

Exercise 2: Error Output

Starting with the second programming assignment (p2), you will be required to detect and report errors.  All errors must be written to standard error.  Consider the following program (in your directory ~/211/lab02_even and on the web at  ~tyson/211/src/lab02_error)

//error.cpp

#include <iostream>
using namespace std;

int main()
{
// write to standard output
cout << "written to standard output" << endl;

// write to standard error
cerr << "written to standard error" << endl;

// return 0 from main() if there are no errors
return 0;
}

Compile and run this program:

$ cd ~/211/lab02_error
$ g++ -o error error.cpp
$ error
written to standard output
written to standard error
$

Since the default is for both standard output and standard error to be written to the current window, you cannot tell that the first string is written to standard output and the second string is written standard error.  However, you can redirect standard output to one file and standard error to a second file:

$ error    >myout    2>myerr

Look at the two files created (myout and myerr).  What is happening?

Write a program (called even.cpp) that reads integers until end of input (just like in exercise 1 above).

Put this file in the directory ~/211/lab02_even.

After reading the integers:

if all of the integers are even, write "all even" and a newline to standard output.

else if any of the integers are not even, write "not all even" and a newline to standard error.

When there are no errors (when all the numbers are even) return 0 from main().  The Linux standard is that programs should return 0 from main() if there are no errors.

When there is an error (one or more numbers are not even) return 1 from main().

Do not return from main() until after you have printed the appropriate message.

The tests for this exercise (in the directory ~/211/lab02_even/tests) have a .err file for each test.  The error files contain the error output (if any) and a .exit file that indicates the correct exit status (value returned by main()).

Read how to test a program that has error output on the Introduction to Testing page.

If a program is required to have error output, turnin.ecst.csuchico.edu will check the value returned by main() (the exit status).  It should be 0 if there were no errors, 1 if there were errors.  You can see the exit status of the program that just finished executed using the echo command:

$ even < t01.in  >t01.myout   2>t01.myerr
$ echo $?
0
$

This means that the exit status of even was 0.

Hints:

It would be a good idea to spend a little time trying to write this program without reading this hints section.  However, if you get stuck, go ahead and read the hints below.

The modulus operator (%) can be used to determine if a number is even or odd.  For example, if (value %2 == 0) then the remainder of dividing value by 2 is 0.  Thus the value must be an even number.

Don't store all the values.  After each value is read, determine if it is odd or even.  If it is odd, set a flag and continue (a flag is a boolean variable)

bool all_even = true;  // all_even is called a boolean flag, we start by assuming all the values are going to be even

while there are numbers to read
if number is odd
all_even = false;


now look at the all_even flag to determine what you should write and what value should be returned from main()



To get credit, you must pass the posted tests (in the directory ~/211/lab02_even/tests and on the web at  lab02_even/tests)

Turn in the file even.cpp
