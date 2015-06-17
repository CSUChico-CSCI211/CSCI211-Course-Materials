#CSCI 211: Programming and Algorithms II
Program 2: Video Rating System

Grading Weight: 2 (programs will have a weight between 1-5)

The third programming assignment will use the classes and the input code from this assignment.  If you don't get this assignment working (at least through Step 7) you will have to catch up to finish the next assignment.

##Overview:

Read an unordered collection of video descriptions each containing a title, url, comment, length, and rating.

Allow the user to specify how the videos should be sorted:  by rating, by length, or by title.

After all the descriptions have been read, print them to standard output (using cout) sorted using the specified criteria (rating, length, or title).


##Requirements:

Create a class to store the video descriptions.  Call this class Video and put it in the files video.h and video.cpp.  All the member variables in class Video must be private.

Put the main() function in the file main.cpp

Allow the user to specify up to 100 videos.  If more than 100 videos are specified, print the message "Too many videos, giving up." and a newline (endl) to standard error (using cerr) and terminate the program.

Return an exit status of 0 if there are no errors, 1 if there is an error (exit status is the value returned from main()).

Use an array of pointers to videos (Video \*) to store the videos.  Use dynamic memory to create a new Video object for each description read (use the C++ new operator).

The first thing in the input must be the sorting criteria (on its own line).  The valid strings are "rating", "length", and "title."

rating:  sort the output so the highest ratings come first.
length: sort the output so the shortest videos come first.
title: sort the output so the videos titles are in alphabetical order.

If the first line is not one of the above strings, print the message "XXX is not a legal sorting method, giving up." (where XXX is the first string in the input; the illegal sorting method) and a newline (endl) to standard error (using cerr) and terminate the program.

After the sorting method string (rating, length, title), the input will contain only valid video descriptions (you do not have to worry about errors in the descriptions).  Each description will be formatted as follows:

first line: the title of the video (may contain spaces)
second line: the URL of the video (may contain spaces)
third line: a comment (may contain spaces)
fourth line:  a floating point number that is the length of the video
fifth line: an integer from 1 to 5 that is the rating of the video

Each field of the video description will be on its own line.  The title, URL, and comment are strings.  The length is a floating point number.  The rating is an integer (it will always be in the range of 1-5).  The following is valid input.  Remember that the first line is the sorting method.

rating
United Break Guitars
http://www.youtube.com/watch?v=5YGc4zOqozo
Great example of one person getting a giant company to listen
4.5
4
Funny Cats
http://www.youtube.com/watch?v=nTasT5h0LEg
Why are there so many cat videos on youtube?
2.75
1
It's Not About the Nail
https://www.youtube.com/watch?v=-4EDhdAHrOg
Favorite web video
1.68
5
Pet Interviews - Guinea Pig
https://www.youtube.com/watch?v=jW3XtKBlTz0
Best guinea pig interview
1.75
4


The following is the correct output for the above input (sorted by rating as specified in the above input).

It's Not About the Nail, https://www.youtube.com/watch?v=-4EDhdAHrOg, Favorite web video, 1.68, *****
United Break Guitars, http://www.youtube.com/watch?v=5YGc4zOqozo, Great example of one person getting a giant company to listen, 4.5, ****
Pet Interviews - Guinea Pig, https://www.youtube.com/watch?v=jW3XtKBlTz0, Best guinea pig interview, 1.75, ****
Funny Cats, http://www.youtube.com/watch?v=nTasT5h0LEg, Why are there so many cat videos on youtube?, 2.75, *

If two or more Videos have the same values for the current sorting methods (e.g. you are sorting by length and two or more videos have the same length), these videos should be sorted in the same order as the input.  For example, in the above sample input if both Dog Playing Piano and Cupcake eating challenge had the same rating,  Dog Playing Piano would be first because it is first in the input.

##Hints:

1. Make sure you understand how the input is ordered and the required output before you start.

2. Program incrementally.  Get small parts working before you move on.  The next section describes how to break the program into pieces.

3. cin >> my_string will not work for strings with spaces.  You will need to use getline(cin, title) where title is a C++ string.

4. Use the call to getline in the while loop:  while (getline(cin, title))   // while there are more video descriptions to read

5. Use "cin >> " to read both the length and the rating.

6. After you read the rating (which is the last element of the description) there will be an extra line feed that you need to get rid of before you can read the next description (getline will read an empty line if you don't get rid of the newline).  Use the following statement to get rid of that line feed:  cin.ignore();

7. When sorting the videos you need to be able to determine how two video objects should be ordered.  The easiest way to do this is to write member functions to handle the comparisons in class Video.  For example, this function could be used when sorting the videos by length:

<pre>
    // return true if the current video is longer than the given video (other), return false otherwise
    bool Video::longer(Video \*other)
    {
      return m_length > other->m_length;
    }
</pre>

8. You will need to compare strings alphabetically when sorting by title.  If you use C++ style strings (as suggested above) you can compare them using the normal comparison operators:

<pre>
    string str1 = "hello";
    string str2 = "goodbye";
    if (str1 > str2)
    {
       // this code is executed if str1 is alphanumerically greater than str2
    }
</pre>

9. Use the bubble sort algorithm (look at the animation on this page to see how it works) to sort the videos.  The following code uses the Video::longer() function above and sorts the array by video length:

<pre>
    for (int last = num_videos -1; last > 0; last--)
       for (int cur = 0; cur < last; cur++)
         if (videos[cur]->longer(videos[cur+1]))
           swap(videos[cur], videos[cur+1]);  // since videos is an array of pointers you can simply swap the addresses at the cur and cur+1 locations.

</pre>

10. Start today.



Plan of Attack:

Step 1: Create video.h and put an empty class definition and the #ifndef/#endif construct.  You may start with the object_start_here to start your .h file (see How to Download Files).

Step 2: Create an empty video.cpp that includes video.h  (see object_start_here).

Step 3: Create main.cpp and write an empty main() (a main function that does not do anything).  main.cpp should also include video.h.

Step 4: Using the Makefile in your p2 directory (downloaded in Lab 1), compile the assignment using the make utility.  If you names the files as specified above, double check that you include only .h files (never include a .cpp file), and copy my Makefile to your current directory, you can compile your program simply by typing "make" at the command prompt:

$ make

Step 5: Once the "empty" files compile, write the code in main() to read the input (the sorting method string and the video descriptions).  Write the data to standard output to make sure you are reading it correctly.  Make sure you continue reading video descriptions until the end of input.

Step 6: Implement the Video class.  Include a constructor and a print function.

Step 7: After you read each description, create a new Video object (using the new operator).  Call the print function for that new object.  Make sure the output is in the correct format so you don't have to worry about the print format anymore.

// Create the new Video object
Video *temp_video_pointer = new Video( -- the variables that hold the values you just read in go here -- );

// tell the new Video object to print itself
temp_video_pointer->print();

Step 8: Use the array of 100 pointers to Video objects to hold the videos (instead of the temp_video_pointer above).  Instead of printing after each on you read, print all the Videos in the array after you are done reading all the input.  The output of your program should be complete except for the order of the videos.  Make sure everything is working before you move on.

Step 9: Implement the sorting of the videos.  Do not start this step until you have tested your program and are sure all the other components are working.


General Requirements:

Programs should be well formatted so they are easy to read and uniform. Avoid using tabs in your programs. Code must be correctly indented, but you should use spaces for indenting, not tabs. See the Formatting Requirements page.

The first lines of all your files (.h and .cpp) must contain the following comments:

// filename
// last name, first name
// ecst_username


Testing:

Sample tests are posted in the src/p2/tests directory. These tests are included in the 211.tar file downloaded in the first lab.

Since this program requires error messages written to standard error (cerr) in addition to output written to standard output (cout), the test cases include output (e.g. t01.out) and error output (e.g. t01.err) files.

See Introduction to Testing for instructions on how to test this program.

If you want to save yourself some time typing, read how to use my automatic testing script.


Submitting:

You MUST turn in your assignment several times (at least three) during development.  Only the last submission has to compile and run and only the last submission will be graded.  The submissions should show your progress (e.g. the first submission has a little bit of the program working, the second a little more, etc).  When I suspect cheating I will look at these early submissions for a clear development trend; I want to prevent students from copying finished programs from another student and then turning them in.

Turn in the following files using https://turnin.ecst.csuchico.edu.

video.h
video.cpp
main.cpp
