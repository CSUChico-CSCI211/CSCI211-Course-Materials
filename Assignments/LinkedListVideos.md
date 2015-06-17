#CSCI 211: Programming and Algorithms II
##Program 3: Linked List of Video Objects
##Grading Weight:
4 (programs will have a weight between 1-5)

##Overview:

Implement a linked-list of pointers to Video objects (see p2 for a description of class Video).

Implement a main() that reads and executes commands.  Your program must handle the following commands:

  1. Insert a new video into the linked-list
  2. Print all the videos in the list.
  3. Lookup a video by title and print it.
  4. Print the number of videos in the list.
  5. Remove a video by title

##Requirements:

###Implementation

Use the Video class you created for p2 to store ratings.  If you did not finish p2, create a Video class as specified in p2.  You may need to add a member function.

Create a linked list class of Video * and call it Vlist.  Put this class in the files vlist.h and vlist.cpp.  The nodes in this list must not be the Video objects.  Each node will contain a pointer to a Video object and a pointer to the next node.

Put the main() function in the file main.cpp

The linked-list should always be ordered alphabetically by title.  The insert function should insert videos so that after the insert all videos in the list are ordered alphabetically.

All member variables of class Video and class Vlist must be private.

Use dynamic allocation to create and delete Video and Node objects:

    * When reading a new Video, you must use the new operator to create a new Video object (just like in p2).
    * Create the "new" Video objects in main() and pass a pointer to the object to Vlist::insert()
    * When inserting into the list, you must use the new operator to create a new Node object (just like in class linked-list examples).
    * Create the "new" Node object in Vlist::insert().
    * When removing a video from the list, both the Node and the Video object must be deleted.


You must provide a correct destructor for class Vlist.  It must delete all Video and Node objects.

There must not be any input or output in class Vlist (you cannot use cin/cout/cerr in a Vlist member function).  However, you can call Video's print function.

The only input or output allowed in class Video is output in Video::print() function.  ALL ERROR MESSAGES MUST BE PRINTED FROM main().

Return an exit status of 0 if all the commands were legal.  Return an exit status of 1 if any of the commands were illegal.

###Input

Your program must read commands until the end of input (until user presses ^D or the end of a redirected file is reached:  $vlist < tests/t01.in).  When end of input is reached, exit your program with an exit status of 0 (see below for exit status when a bad command is entered).

Your program must handle the following commands.  The arguments for the command are always on the next line (or lines).  For the insert command the arguments (title, url, comment, length, rating) will be on the five lines following the command (each on its own line just like in p2).  For the lookup and remove commands, the title will be on the next line.

|Command | Action |	Arguments| 	Error |
|:-------|:-------|:---------|:-------|
|insert|	Insert a new video into the linked list.|	Title, url, comment, length, rating| 	Title is already in the list.  See error messages below.|
|print|	Print all the videos in the list using the format from p2.| 	none|	none (print nothing if list is empty)|
|length| 	Print the number of videos in the list as a single integer (don't print anything other than the integer).|	none| 	none (print 0 if the list is empty)|
|lookup|	If the given title is in the list, print the video using the format from p2.|	title (may contain spaces)|	Title is not in list.|
|remove|	If the given title is in the list, remove it.|	title (may contain spaces)|	Title is not in list.|


###Errors and Error Messages

The input will not contain any errors other than those listed in this section.  For example, the insert command will always be followed by a title, url, comment, length, rating (each on a separate line).  The program should NOT terminate for the following three errors.

|Command|	Error|	Error Message (replace XXX with the title entered by user, print the < and >)|
|:------|:-----|:---------|
|insert |Title already in list.|	Could not insert video <XXX>, already in list.|
|lookup |	Title not in list.|	Title <XXX> not in list.|
|remove |	Title not in list.| 	Title <XXX> not in list, could not delete.|

If the user enters a command other than (insert, print, length, lookup, remove) print the following error message and terminate the program with an exit status of 1.  Replace the XXX with the command entered (make sure you print < and > in your error message).

<pre>
    &lt;XXX&gt; is not a legal command, giving up.
</pre>


##Hints:

  1. Students often ask me questions that are answered in the handout.  I don't mind, but it is much faster to read the handout then to ask me a question.  It is very helpful to read the entire handout carefully before you start and review it as you program.  I suggest you print out the handout and check off each requirement when you are sure it is correctly implemented.

  2. Program incrementally.  Get small parts working before you move on.  The next section describes how to break the program into pieces.

  3. The linked list examples from class are all linked lists of integers.  That means the Nodes contain an integer.  For this assignment, the list is a list pointers to Video objects, that means the Node will contains a Video * instead of the integer in the class examples.

  4. You may start with the posted linked-list example code, HOWEVER on the exam you will need to be able to write some of this code from scratch.  It would be better if you wrote as much as you can from scratch.

  5. Use static memory in main() to instantiate the Vlist object:  *Vlsit videos* instead of *Vlist \*videos = new Vlist()*

  6. *lookup* and *remove* take titles as their arguments.  If the command is lookup or remove, use a getline to read the title.

  7. Use getline() to read all the commands.  getline() will automatically throw away the newline character at the end of the line.
  <pre>

    while (getline(cin, command)) {
      // have just read a new command
      if (command == "insert")
      {
        // read the insert arguments (title, url, comment, length, title)
        //...
        cin >> rating;
        // since cin >> rating does not throw away the newline, you need to explicitly ignore it
        cin.ignore();
      }
      else if (command == "remove")
      {
        getline(cin, title)
        // don't have to worry about the newline because getline threw it away

      }
      ...
    }
<pre>
  8. When reading a video, use the same approach you used in p2.  Except the getline for the title will no longer be in the while statement (the reading of the command will be in a while statement).

  9. Since you will be printing error messages in main(), several of the Vlist functions will have to return the status of the function. For example:
  <pre>
    bool Vlist::remove(string title)
    {
    if the title is in the list and was removed
    return true
    else return false
    }
  </pre>
    In main() the value returned by remove can be used to determine if an error message should be printed. Print all error messages from main().

  10. Use asserts to document what you think should be true or false.

  11. When you make a mistake with a pointer, your program usually terminates with a Segmentation Fault.  It can take a lot of time to track down these problems.  Even if you did p2 at the last minute, it is a good idea to start p3 early.


##Plan of Attack:

Step 1: Copy p2's main.cpp video.h video.cpp to your p3 directory (do not use the same directory for both assignments).

Step 2: Create the Vlist class without any functions (vlist.h vlist.cpp).

Step 3: Update main() so it includes vlist.h; about the only code you need from p2's main() is the reading of the Video fields (title, url, ...) and the declaration of the variable (string title, string url, ...).  Delete the rest of the code.

Step 4: Download my Makefile (in ~tyson/211/src/p3) and compile the assignment using the make utility ($ make ).

Step 5: Once the "empty" files compile, write the code in main() to read the input.  Test your code so you are sure it is working.  Make sure you handle end of input (^D), illegal commands, and skipping whitespace correctly.  What you read will depend on the command.  For example, length takes no arguments but insert takes 5 arguments.

Step 6: Once you are certain that your input is working correctly, implement an insert function in Vlist that inserts the videos at the front of the list.  Eventually you will need to insert so they are sorted, but getting this simple function working first is very helpful.

Step 7: Write the Vlist print function.  This function calls Video::print() on all the videos in the list.

Step 8: Implement the insert and print commands in main().  Once they are implemented you will be able to insert any number of videos into the list and print the entire list out.  However, the order will not be correct yet because you have a place holder for the insert function.  As an example of how to implement the commands, below is my implementation of the print command.  I called my Vlist object vlist.

<pre>
if (command == "print")
{
    vlist.print();
}
</pre>

Step 9: Once you are certain that the print and insert commands work, you can update the insert function to insert the video so the list is ordered correctly (alphabetically by title).  Test your new insert function.  If it is correct your program should pass all tests that only use the insert and print commands.  If you don't pass these tests, fix the problem before you move on.

Step 10: Implement the remainder of the commands one by one.  Make sure each works before you move on.  I recommend implementing remove last because if you make a mistake in remove it can be very hard to track down.

Step 11:  Write the destructor for Vlist.

Step 12:  Read the requirements carefully to make sure your program is complete.



##General Requirements:

Make sure your program is well formatted and uses spaces to indent instead of tabs.  See the Formatting Requirements page.

The first lines of all your files (.h and .cpp) must contain the following comments:

<pre>
// filename
// last name, first name
// ecst_username
</pre>

##Testing:

Sample tests are posted in the src/p3/tests directory.

See Introduction to How to Test for instructions on how to test this program.

If you want to save yourself some time typing, read how to use my automatic testing script.


##Submitting:

You MUST turn in your assignment several times (at least three) during development.  Only the last submission has to compile and run and only the last submission will be graded.  The submissions should show your progress (e.g. the first submission has a little bit of the program working, the second a little more, etc).  When I suspect cheating I will look at these early submissions for a clear development trend; I want to prevent students from copying finished programs from another student and then turning them in.

Turn in the following files using https://turnin.ecst.csuchico.edu.

* video.h
* video.cpp
* vlist.h
* vlist.cpp
* main.cpp

##Extra Credit:

No extra credit will be give to late assignments (both the regular assignment and the extra credit must be turned in on time).

Make sure you save a copy of your completely working program before you start the extra credit.  The goal of extra credit is for you to figure out how to solve problems on your own.  I will discuss extra credit, but I won't tell you how to solve it.

3 points:  implement the print_by_length command that prints all the videos in the list ordered by length (short to long). If two or more videos have the same length they should be sorted alphabetically (that is if video "a" has the same length as videos "c" and "d", "a" should be first, "c" second, and "d" last).

3 points: implement the print_by_rating command that prints all the videos in the list ordered by rating (highest to lowest). If two or more videos have the same rating they should be sorted alphabetically.

3 points: implement lookup_expression command that takes a [regular expression](http://en.wikipedia.org/wiki/Regular_expression "regular expressions") and prints all the videos that have titles matching the given regular expression.  Use the system functions [regcomp and regex](http://www.ecst.csuchico.edu/%7Etyson/classes/examples/regcomp/) to implement regular expressions.  If the regular expression does not match any titles in the list OR if the regular expression is not a correct regular expression, print the following to standard error (replace XXX with the regular expression):

<pre>
    Regular expression <XXX> does not match any titles in list.
</pre>

If two or more videos match the regular expression, they should be sorted alphabetically.

If you do the extra credit,  add it to your base assignment and turn it in as **BOTH** "p3 video list" and "p3 extra credit" (you can use the same files for both submissions).
