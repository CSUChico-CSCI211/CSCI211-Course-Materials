#CSCI211 - Lab 3
##Introduction the the Linux make Utility & Practice Creating C++ Objects

NOTE: Paying attention to today's lecture will save you lots of time over the next several years.  Students who do poorly in 211 usually don't understand this material.  Students who get an A, understand it well.

##Goals

* Learn the basics of the Linux make utility
* Practice creating c++ objects

##Overview of make

###make's job is to create files

####Example:

Suppose you have a file called hello.cpp and you want to create the executable called hello.  You would type the command  

<pre>
    $ g++ -o hello hello.cpp
</pre>

and g++ would generate hello for you.

Each time you change hello.cpp you have to compile it ($ g++ -o hello hello.cpp) to see if your changes work.

It can get very tiring typing $ g++ -o hello hello.cpp every time you want to compile your hello.cpp program.

If you use the make utility, instead of typing $ g++ -o hello hello.cpp  to compile you would type $ make

####Steps for using make

1. Create a file called makefile or Makefile (most people use Makefile so it appears first in directory using ls)
2. Using an editor (such as scite, vim, nano) edit the file Makefile
3. Insert the rules for creating the files (for making the files)
4. Run the make utility by typing make at the bash command prompt

####Advantages of make

1. You only have to type the compilation command(s) once (that is, put them in the makefile)
2. Make will only compile the files that have changed since the last time you compiled (this is really important in large projects where complete compilation may take several hours).

These are surprisingly big advantages.

####Anatomy of a makefile:

this is a simple and complete makefile:

<pre>
	hello: hello.cpp
		g++ -o hello hello.cpp
</pre>

*NOTE: for most versions of make (including the one standard on Linux), the second line must start with a <tab> so it is a good habit to always use a <tab>.  If vim does not automatically turn the <tab> key into an actual tab, you can insert a tab by typing (while in insert mode)  control-V followed by a tab -OR- you can program vim to understand that Makefiles want tabs by adding the following line to your ~/.vimrc file*

<pre>
    autocmd FileType make set noexpandtab|set autoindent
</pre>

This simple makefile contains a single rule that you can read like this:

> If the file hello is older than the file hello.cpp then execute the command "g++ -o hello hello.cpp"

Basic format of rules in makefiles:

<pre>
    target_file : list_of_dependency_files
    <tab>command_to_build_target_file
</pre>

##Multi-file make

In C++ programs it is common to put each class in its own two files,  class_name.h for the class header, class_name.cpp for the class's member functions.  The next example (lab03_sentence) contains three files:

<pre>
    main.cpp             the file containing the main() function
    sentence.h           the file containing the definition of class Sentence (class Sentence { .... };)
    sentence.cpp        the file containing the source code for class Sentence (the bodies of the member functions)
</pre>

The most efficient way to compile such program is to compile each component into an object file (.o) and then combine the object files into an executable (the combination of .o files is called linking):

<pre>
    g++ -c main.cpp                                  will create the object file main.o
    g++ -c sentence.cpp                            will create the object file sentence.o
    g++ -o sentence main.o sentence.o     will create the executable sentence (will link main.o and sentence.o into sentence)
</pre>

###Simple Makefile Example

<pre>
	# simple makefile

    # This rule tells make how to "make" the executable sentence
    main: main.o sentence.o
    	g++ -Wall -pedantic -std=c++11 -g -o main main.o sentence.o

    # This rule tells make how to "make" the object file main.o
    main.o: main.cpp sentence.h
    	g++ -Wall -pedantic -std=c++11 -g -c main.cpp

    # This rule tells make how to "make" the object file sentence.o
    sentence.o: sentence.cpp sentence.h
    	g++ -Wall -pedantic -std=c++11 -g -c sentence.cpp


    # This rule tells make what to delete when the user type "make clean"
    # BE VERY CAREFUL to only put generated files here
    clean:
    	rm -f main.o sentence.o main
</pre>

##Compiler Options

The above Makefile uses the following command-line options for the g++ compiler:

|Option| Description|
|:-----|:-----------|
|-c|Compile only: create a .o file, don't create an executable (such as a.out)|
|-o filename |Name the output filename instead of the default a.out|
|-g |Put some extra information in the output files (.o and executables) that can be used by the debugger (debuggers are discussed in a future lab)|
|-Wall 	|Show all warnings (warnings help illuminate problems in your program, you should fix your code so there are no warnings)|
|-pedantic|	 Issue all the warnings demanded by strict ISO C and ISO C++ (i.e. issue warnings if your program does not follow the standard exactly)|
|-std=c++11|Use the newest C++ standard (C++11).  In the near future all C++ programs will need to conform to C++11.|



##Default Rules

There are many default rules built into various versions of make.  Thus in a large project the makefile would not contain a rule for every single source file.

When learning how to use make it is best to avoid the default rules and put in explicit rules for each file.


##Exercise 1:
(must complete this google survey to get credit)

cd to the lab03_hello directory

<pre>
    $ cd ~/211/lab03_hello
</pre>

type the command

<pre>
    $ make
</pre>

*What happened?*                **Answer on the google survey.**

type the command again

<pre>
    $ make
</pre>

*What happened?  Why?*      	**Answer on the google survey.**

look at the dates on the files hello and hello.cpp

<pre>
    $ ls -l
</pre>

when hello is newer than hello.cpp, make does not try to recreate it

change the date on hello.cpp using the touch command

<pre>
    $ touch hello.cpp
</pre>

*touch* just updates the last date changed to the current time

now look at the dates again

<pre>
    $ ls -l
</pre>

what do you think will happen when you type make ?

type

<pre>
    $ make
</pre>

What happened?  Why?           **Answer on the google survey**

now edit the file hello.cpp (using any editor such as atom) and make some change
for example: change the text that is printed

make sure you save the file

now type

<pre>
    $ make
</pre>

what happened?  why?         **Answer on the google survey**

#Exercise 2:
(must complete the rest of this google survey to get credit)

go to the lab03_sentence directory

<pre>
    $ cd ../lab03_sentence
</pre>

the ".." means the parent directory (the parent of the current directory).  Alternatively you could have used the full path (~/211/lab03_sentence)

Why does main.o depend on sentence.h?        **Answer on the google survey**

type

<pre>
    $ make
</pre>

type

<pre>
    $ touch sentence.h
</pre>

type

<pre>
    $ make
</pre>

Which files were recompiled?         **Answer on the google survey**

Why were these files recompiled when sentence.h was changed? (look carefully at the Makefile)
**Answer on the google survey**

***This is an important aspect of make, ask if you don't understand why!***

##Exercise 3: (must turn in a Makefile)

The directory lab03_makefile contains a program that uses two different objects: class Foo (in foo.h and foo.cpp) and class Bar (in bar.h and bar.cpp).  Create a makefile that compiles this program.

You may start by using the Makefile from Exercise 2.

Test your Makefile by compiling and running the program (the make order is not important as long as you can run the program):

<pre>
	$ make
	g++ -Wall -pedantic -g -std=c++11 -c main.cpp
	g++ -Wall -pedantic -g -std=c++11 -c foo.cpp
	g++ -Wall -pedantic -g -std=c++11 -c bar.cpp
	g++ -Wall -pedantic -o foobar main.o foo.o bar.o
	$ foobar
	Foo(1,2)
	Bar(3,4)
	$
</pre>

Turn in your Makefile.  turnin.ecst will not test your Makefile, I will grade them by reading them.  Since a Makefile can do anything (such as deleting all the files on a computer) turnin.ecst never runs Makefiles that have been turned in.

Hint: think carefully about the dependencies (the files listed after the target). For example, foo.cpp includes foo.h and thus foo.o depends on foo.cpp AND foo.h

##Exercise 4: Create a Course class

Create a new class called Course (that is, create course.h and course.cpp).  You may start with this example (on Jaguar, copy it from ~tyson/211/example_src/object_start_here).

The Course class should have a single constructor and a print function

Course(string dept, int number, int time);
void print();

You need to figure out what member variables are required by class Course.

Create a new file called schedule.cpp that contains a main() function to test your course class.  In your main() you should be able to use the Course class like this:

Course programming("CSCI", 211, 1000);
Course english("ENGL", 130, 1400);
Course physics("PHYS", 204, 800);

programming.print();
english.print();
physics.print();

The above calls should result in the following output (this output is in the tests/lab03_course directory in the file t01.out).

CSCI 211 at 1000
ENGL 130 at 1400
PHYS 204 at 800

You can compile this program using this command (lab 4 explains a tool for compiling programs with multiple files):

g++ -Wall -o schedule schedule.cpp course.cpp

REMEMBER:  only include .h files (schedule.cpp must include course.h and course.cpp must include course.h).  NEVER INCLUDE .cpp FILES.

To get credit, you must pass the posted tests (in your directory ~/211/lab03_course, and on the web at ~tyson/211/src/lab03_course/tests).

Turn in the files schedule.cpp, course.h, and course.cpp

Exercise 5: Create class Video for p2.

Create the Video class you need for p2 and a simple main() to test it.

If you have finished p2, all you have to do is create a main.cpp and turn in your video.h and video.cpp for this lab (be careful not to delete your 'real' main.cpp).

The sample main() should be similar or identical to the following (you will have to add some other code before the main):

int main()
{
    Video video1("Title One", "www.youtube.com/one", "Comment ONE", 1.1, 1);
    Video video2("Title Two", "www.youtube.com/two", "Comment TWO", 2.2, 2);

    video1.print();
    video2.print();
    return 0;
}

If you have already written the constructor (Video::Video(...)) and your arguments are different than those listed above, your main() should use the arguments you are already using.

If you have not started p2, look at the Plan of Attack section and implement Steps 1-6.

You will need to implement the class Video constructor (Video::Video(...)) and the print member function (void Video::print()).

The output of your program (using the main() above) should exactly match the following (~tyson/211/tests/lab03_video/t01.out). This is the test used by turnin.ecst.csuchico.edu:

Title One, www.youtube.com/one, Comment ONE, 1.1, *
Title Two, www.youtube.com/two, Comment TWO, 2.2, **

The single test will expect this output.

To get credit, you must pass the posted tests (in yoru directory ~/211/lab03_video/tests and on the web at ~tyson/211/src/lab03_video/tests).

Turn in  main.cpp, video.h, and video.cpp.  Turn in all three files even if you have completed p2.
If you finish the lab exercises, you can work on your video (p2) assignment.  If you have finished the exercises and have finished (and turned in a working version) of the video assignment, you may leave early.  Check with me before you leave so I can verify that you have everything turned in.
