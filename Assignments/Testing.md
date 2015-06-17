#Introduction to Testing

You will save countless hours in CSCI 111 and CSCI 211 (and probably other classes) if you understand how to test your program.  This mechanism is also used by turnin.ecst.csuchico.edu.

For each assignment, one or more tests will be posted on the class web pages.  For example, for CSCI211 the tests are posted here.  Copy these files to the directory that contains your program  (see how to download files to copy my files to your current directory).


##Programs with Output and No Input (early assignments in CSCI 111)

The simplest programs read no input and produce output:

<code>
int main()
{

cout << "Hello world!" << endl;

}
</code>

In order to make sure such a program is correct, the text written to standard output ("Hello world!") needs to be compared to a correct solution.  For assignments that read no input, you will be given a single correct output file.  In the following example, that file is called "t01.out" and the executable is called hello (an executable is a compiled program):

<code>
$ hello > t01.myout
</code>
Note: if you get a message that hello cannot be found, you might have a problem with your path, try $ ./hello > t01.myout

The > takes what your program wrote to the screen (known as standard output) and redirects it to a file (t01.myout in the above example).  You can view the contents of t01.myout using an editor or the Linux cat utility:

<code>
$ cat t01.myout

Hello world!

$
</code>

You can compare your output (t01.myout) to the correct output (t01.out) using the  Linux diff utility:

<code>
$ diff t01.myout t01.out
$
</code>

If these two files match, diff prints nothing.  That means your program produced the correct output (you passed the test).

The tool vimdiff is an alternative to using diff.  It highlights the differences in red.  You can move around just like in the vim editor.  If you don't know the vim editor, you can exit vimdiff by typing ":qa" then press enter (don't type the quotes).  If you appear to be stuck, try pressing the escape key before the ":qa"

$ vimdiff t01.myout t01.out


##Programs with Input and Output (later assignments in CSCI 111, most assignments in subsequent classes)

Some programs read input and produces output.  The following program reads an integer (from standard input) and writes it to the screen (standard output).

int main()
{
int i;
cin >> i;
cout << "You entered " << i << endl;
}

This program can be tested using the same mechanism described above, except now we will redirect standard input (using <) and standard output (using >).  Assume the executable is called num.

$ num < t01.in > t01.myout

Instead of reading from the keyboard, when you call a program using input file redirection (<) the program reads from the given file.  Thus the above command reads from t01.in instead of the keyboard and writes to t01.myout instead of the screen.

You can compare your output (t01.myout) to the correct output (t01.out) using the  Linux diff utility (see above):

$ diff t01.myout t01.out

If these two files match, diff prints nothing.  That means your program produced the correct output (you passed the test).

The tool vimdiff is an alternative to using diff.  It highlights the differences in red.  You can move around just like in the vim editor.  If you don't know the vim editor, you can exit vimdiff by typing ":qa" then press enter (don't type the quotes).  If you appear to be stuck, try pressing the escape key before the ":qa"

$ vimdiff t01.myout t01.out

Since each input is likely to produce different output, your instructor may give you many tests cases (e.g.  t01.in t01.out    t02.in t02.out    t03.in t03.out etc).  You should try them all:

$ num < t02.in > t02.myout
$ diff t02.out t02.myout
$ num < t03.in > t03.myout
$ diff t03.out t03.myout
$ num < t04.in > t04.myout
$ diff t04.out t04.myout
...

I hope you are thinking about now that there has to be a better way.  After all the Bash Shell is a full programming language, you should not have to type things over and over.

Programs with Input, Output, and Error Output (some assignments in 111, most assignments after 111)

For most CSCI211 assignments (and most assignments in upper division courses) you are required to write error messages to standard error (using cerr <<  instead of cout << ):

int main()
{
.....
cout << "This is written to standard output\n";
cerr << "This is an error, it was written to standard error\n";
}

For assignments that require error messages your instructor will post three files for each test:

testing input:  t01.in
correct output: t01.out
correct error output: t01.err

You can test your program as follows (assuming the executable is called calendar)

$ calendar < t01.in > t01.myout 2> t01.myerr
$ diff t01.myout t01.out
$ diff t01.myerr t01.err
$


The first line runs the program calendar reading from the file t01 (the "<" redirects the file t01 into standard input), writing standard output to file t01.myout (the ">" redirects the standard output to the file t01.myout), and writing standard error to the file t01.myerr (the "2>" redirects the standard error to the file t01.myerr).  Note: "2>" works for the bash shell, other shells using different syntax; the bash shell is the most common shell.

The second line compares the output from your program (t01.myout) with the posted output (t01.out).

The third line compares your error output with the posted error output (t01.err).  If your two files are identical to my two files you have passed test t01.

Repeat this process for all the given test cases.
