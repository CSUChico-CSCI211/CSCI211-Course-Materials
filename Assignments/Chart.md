#CSCI 211: Programming and Algorithms II
Program 1: Chart
Grading Weight: 1 (programs will have a weight between 1 - 5)

##Overview:

The goal of this program is to introduce you to C++ and programming in the Linux environment.

This program reads a set of integers from standard input and draws a bar chart to standard output using asterisks and spaces ('\*' and ' ').

The user specifies a set of up to 100 integers greater than 0.  When the user enters a 0, the program will stop reading standard input and print the chart.

For example, if the user entered, 1 2 3 4 3 2 1 10 0, your program must print:

<pre>
	   *
	   *
	   *
	   *
	   *
       *
   *   *
  ***  *
 ***** *
********
</pre>

Notes:  there are no spaces before the column of the first bar, and there are no spaces after the column of the last bar.

##Program Requirements:

The input numbers might be on separate lines.  If you read them using "cin >>" you don't have to think about lines, spaces, tabs.

Read up to 100 positive integers (greater than 0) from standard input.  You must store these integers in a single array.

After all these numbers are read (that is, after the user enters a 0), draw the corresponding bar chart.  For example consider the following input/output (I use "$" to represent the Linux command prompt):

<pre>
$
$ chart
1 4 2 3 0
 *
 * *
 ***
****
$
</pre>


The user typed "chart" (the name of the program's executable) at the Linux command prompt and then pressed enter.

Then the user typed in the following text:

		<1><space><4><space><2><space><3><space><0><enter>

Note: text between a "<" and a ">" is text that the user types.  Sometimes it is a single key, sometimes it is a string.  "<" and ">" are often used to delineate characters a user types.  In the above string, <1> represents the 1 key, <space> represents the space bar.

Then the program printed the asterisks and spaces.

The final "$" is the Linux command prompt, it is not printed by the program.

Your program must work exactly like this.  It must not print any other characters.

Note: when you type a command at the Linux prompt, the shell looks for a file with that name in all the directories in your path (a path is a list of directories).  If the current directory (called ".") is in your path, then you can just type "chart".  If it is not in your path, you have to type "./chart"  You can add "." to your path by editing the file in your home directory called .profile and adding the following line.  If you don't have a .profile file, create a new one.  Add the following line to your .profile.

<pre>
export PATH=.:$PATH
</pre>


##Testing Your Program:

I have posted some sample tests in the src/p1/tests directory (see how to download files to copy my files to your current directory).

The [testing instructions](https://github.com/CSUChico-CSCI211/CSCI211-Course-Materials/blob/master/Assignments/Testing.md "Testing") contain instructions for testing your program using my sample tests.

I will test your program with additional tests not posted in the test directory.  It is a very good idea to design and implement your own set of tests.

##Hints:

Since you will not be given more than 100 integers, create an array of 100 integers.  It is good programming practice to place the "100" in a single place so that it is easy to change:

<pre>
const int MAX = 100;
int values[MAX];
...
for (int i = 0; i < MAX; i++)
{
	...
}
</pre>

the above is better than

<pre>
int values[100];
...
for (int i = 0; i < 100; i++)
{
	...
}
</pre>

You will actually be drawing a rectangular grid with a width equal to the number of bars (values entered) and a height equal to the height of the tallest bar.  At each spot in the grid you must draw a space or an asterisk.

Since you need to know the height of the tallest bar before you start drawing the bars, in my solution there is a function that finds the largest integer in an array of integers.  It looks like this:

<pre>
// return the largest value in the given array of integers
int find_largest(int values[], int size)
{
int largest = 0;
// code to actually find the largest goes here
return largest;
}
</pre>

While you don't have to write a find_largest() function, in future assignments you will be writing a lot of functions, so creating a function for this assignment will help prepare you for future assignments.

In C/C++ you can pass an array without specifying the size of the array.  In a couple of weeks I will cover in lecture why this works.

If you don't finish in time, turn in what you have.  If you turn nothing in I will give you a zero.  If you turn in something I will give you partial credit.  Partial credit is always better than 0.

##General Requirements:

I will deduct points if your program contains any tabs or is not well formatted.  See the  211 Programming Assignment Formatting Requirements for details and instructions.

I will deduct many points if your program does not compile using the command "g++ -o chart chart.cpp" on a Linux machine (such as jaguar.ecst.csuchico.edu).  If when you submit your program on turnin.ecst.csuchico.edu, you get the message "Make did not report any errors" your program compiled without any errors.

I will grade your program using another program, so if your program does not work exactly as specified above you will lose points.  For example, if you put an space at the end of the line, or a blank line at the end of the output, you will lose points.  Test your program using the sample tests in the test directory (see above).

The first lines of all your files (.h and .cpp) must contain the following comments:

<pre>
	// filename
	// last name, first name
	// ecst_username
</pre>

For example, my program would have the comments:
<pre>
	// chart.cpp
	// Henry, Tyson
	// tyson
</pre>

##How to turn in code:

You must turn in the following file:

<pre>
chart.cpp
</pre>

See the [turn in instructions](https://github.com/CSUChico-CSCI211/CSCI211-Course-Materials/blob/master/Assignments/Turnin.md "How to Turnin") for details on how to turn in this assignment.

Assignments can be turned in up to 24 hours late with a 15% penalty.


##Extra Credit: (10 points)

If you do the extra credit you have to turn in a second chart.cpp (p1 *extra* on turnin.ecst).  Make sure you do not change/delete your original chart.cpp.

No extra credit will be give to late assignments (both the regular assignment and the extra credit must be turned in on time).

In addition to printing the chart pointing "up", also print it pointing down, right, and left.  Include a blank line between each chart.

For example, the input 4 3 2 1 2 3 4 0 will create the following output:

<pre>
*     *
**   **
*** ***
*******

*******
*** ***
**   **
*     *

****
***
**
*
**
***
****

****
***
**
*
**
***
****
</pre>
