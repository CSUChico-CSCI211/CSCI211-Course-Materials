
<big><big><small>CSCI 211: Programming and Algorithms II<br>

Program 1: Chart<br>

</small><small>Grading Weight: 1 (programs will have a weight between 1 - 5)<br>

</small></big><br>

</big>
<hr style="width: 100%; height: 2px;"><big><big><b>Overview:</b></big></big>
<blockquote><big>The
goal of this program is to introduce you to C++ and programming in the
Linux environment.&nbsp; <br>
  <br>

This program reads a set of integers from standard input and draws a
bar chart to standard output using asterisks and spaces ('*' and ' ').<br>
  <br>
The user specifies a set of up to 100 integers greater than 0.&nbsp;
When the user enters a 0, the program will stop reading standard input
and print the chart.<br>
  <br>
For example, if the user entered, 1 2 3 4 3 2 1 10 0, your program must
print:<br>
  <br>
  </big>
  <pre>       *<br>       *<br>       *<br>       *<br>       *<br>       *<br>   *   *<br>  ***  *<br> ***** *<br>********<br><br><br></pre>

  <big>Notes:&nbsp; there are no spaces before the column of the first
bar, and there are no spaces after the column of the last bar. <br>





  <br>





  </big></blockquote>





<blockquote>





  <ol>










  </ol>





</blockquote>





<hr style="width: 100%; height: 2px;"><big><big><b>Program Requirements:</b></big></big>
<div style="margin-left: 40px;"><br>





<big>The input numbers might be on separate lines.&nbsp; If you read
them using "cin &gt;&gt;" you don't have to think about lines, spaces,
tabs.<br>
<br>
Read up to 100 positive integers (greater than 0) from standard input.&nbsp; You
must
store these integers in a single array.&nbsp; <br>





</big><big> </big><br>





<big>After all these numbers are read (that is, after the user enters a
0),
draw the corresponding bar chart.&nbsp;
For example consider the following input/output (I use "$" to represent
the Linux command prompt):</big><br>





<big> </big><br>





<big> </big>
<div style="margin-left: 80px;">
<pre><big>$<br></big></pre>





</div>





<div style="margin-left: 80px;">
<pre><big>$ chart</big></pre>





<pre><big>1 4 2 3 0<br> *<br> * *<br> ***<br>****<br>$<br></big></pre>





<span style="font-family: monospace;"><br>





</span></div>





<div style="margin-left: 40px;"><br>





</div>





<big>The user typed "chart" (the name of the program's executable) at
the Linux command prompt and then pressed enter.</big><br>





<br>





<big>Then the user typed in the following text:<br>


<br>


</big>


<big>&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
&lt;1&gt;&lt;space&gt;&lt;4&gt;&lt;space&gt;&lt;2&gt;&lt;space&gt;&lt;3&gt;&lt;space&gt;&lt;0&gt;&lt;enter&gt;</big><br>





<br>





<div style="margin-left: 40px;"><big>&nbsp;Note: text between a "&lt;"
and a "&gt;" is text that the user types.&nbsp; Sometimes it is a
single key, sometimes it is a string. &nbsp;"&lt;" and "&gt;" are often
used to delineate characters a user types.&nbsp; In the above string,
&lt;1&gt; represents the 1 key, &lt;space&gt; represents the space bar.</big><br>





<br>





</div>





<big>Then the program printed the asterisks and spaces. </big><br>





<big> </big><br>





<big>The final "$" is the Linux command prompt, it is not printed by the
program.&nbsp; </big><br>





<big> </big> <br>





<big>Your program must work exactly like this.&nbsp; It must not print any other characters.</big><br>





<big> </big><br>





<big>Note: when you type a command at the Linux prompt, the shell looks
for a
file with that name in all the directories in your <span style="font-style: italic;">path </span>(a path is&nbsp;a list of
directories)<span style="font-style: italic;">.</span>&nbsp; If the
current
directory (called ".") is in your path, then you can just type
"chart".&nbsp; If it is not in your path, you have to type
"./chart"&nbsp; You can add "." to your path by editing the file in
your home directory called .profile and adding the following
line.&nbsp; If you don't have a .profile file, create a new one.&nbsp;
Add the following line to your .profile.</big><br>





<big> </big><br>





<big> </big>
<div style="margin-left: 40px;">export PATH=.:$PATH<br>





</div>





<big> </big><br>





<big> </big><br>





<br>





</div>





<hr style="width: 100%; height: 2px;"><big><big><small><b><big>Testing
Your Program:<br>





</big></b></small></big></big>
<div style="margin-left: 40px;"><br>





<big>I have posted some sample tests in the <a href="http://www.ecst.csuchico.edu/~tyson/classes/211.f15/src/p1/tests">src/p1/tests</a> directory (see <a href="http://www.ecst.csuchico.edu/%7Etyson/classes/general/how_to_download_files.html">how to download files</a> to copy my files to your current directory)</big>.<br><big>



<br>



The <a href="http://www.ecst.csuchico.edu/~tyson/classes/general/how_to_test.html">testing instructions</a> contain instructions for testing your program using my sample tests.<br>



<br>
I will test your program with additional tests not posted in the test
directory. &nbsp;It is a very good idea to design and implement your
own set of tests.<br>



</big></div>



<big><big><small><b><big><br>





</big></b></small></big></big>
<hr style="width: 100%; height: 2px;"><big><big><small><b><big>Hints:<br>





</big></b></small></big></big>
<div style="margin-left: 40px;">
<div style="margin-left: 40px;"><big></big><br>





</div>





</div>





<div style="margin-left: 40px;"><big>Since you will not be
given more than 100 integers, create an array of 100 integers.&nbsp; It
is good programming practice to place the "100" in a single place so that
it is easy to change:<br>





</big>
<pre style="margin-left: 40px;">const int MAX = 100;<br>int values[MAX];<br>...<br>for (int i = 0; i &lt; MAX; i++)<br>{<br>    ...<br>}<br></pre>





<big><br>





the above is better than<br>





</big>
<pre style="margin-left: 40px;">int values[100];<br>...<br>for (int i = 0; i &lt; 100; i++)<br>{<br>    ...<br>}<br></pre>





<big><br>





</big><big>You will actually be drawing a rectangular grid with a width
equal
to the number of bars (values entered) and a height equal to the height
of the tallest bar.&nbsp; At each spot in the grid you must draw a
space or
an asterisk.<br>





&nbsp;<br>





</big><big>Since you need to know the height of the tallest bar before
you start drawing the bars, in my solution there is a function that
finds the largest integer in an array of integers.&nbsp; It looks like
this:<br>





</big>
<pre style="margin-left: 40px;">// return the largest value in the given array of integers<br>int find_largest(int values[], int size)<br>{<br>    int largest = 0;<br>    // code to actually find the largest goes here<br>    return largest;<br>}</pre>





</div>





<div style="margin-left: 40px;"><big>While you don't have to write a
find_largest() function, in future assignments you will be writing a lot of
functions, so creating a function for this assignment will help prepare
you for future assignments.<br>
<br>
In C/C++ you can pass an array
without specifying the size of the array.&nbsp; In a couple of weeks I
will cover in lecture why this works.<br>





<br>





If you don't finish in time, turn in what you have.&nbsp; If you turn
nothing in I will give you a zero.&nbsp; If you turn in something I
will give you partial credit.&nbsp; Partial credit is always better
than 0.<br>





</big></div>





<big><big><small><b><big></big></b></small></big></big><br>





<blockquote> </blockquote>





<hr style="width: 100%; height: 2px;"><big><big><b>General Requirements:</b></big></big>
<blockquote><big>I will deduct points if your program contains any tabs or is not well formatted.&nbsp; See the&nbsp; <a href="../general/code_formatting.html">211 Programming Assignment Formatting Requirements</a> for details and instructions.<br>
  <br>
I will deduct many points if
your program does not compile using the command "g++ -o chart
chart.cpp" on a Linux machine (such as jaguar.ecst.csuchico.edu).&nbsp;
If when you submit your program on turnin.ecst.csuchico.edu, you get
the message "Make did not report any errors" your program compiled
without any errors.<br>
</big><big><br>

I will grade your program using another program, so if your program
does
not work exactly as specified above you will lose points.&nbsp; For
example, if you put an space at the end of the line, or a blank
line at the end of the output, you will lose points.&nbsp; <span style="font-weight: bold;">Test your
program using the sample tests in the test directory (see above).</span><br>

  <br>

  The first lines of all your files (.h and .cpp) must
contain the following comments:<br>
  <br>
  <div style="margin-left: 40px;">

// filename <br>
// last name, first name<br>
// ecst_username<br>
  <br>
  </div>
For example, my program would have the comments:
<br>
<div style="margin-left: 40px;">
// chart.cpp <br>
// Henry, Tyson<br>
// tyson<br>

  <br>
  </div>
  </big>


</blockquote>





<hr style="width: 100%; height: 2px;"><big><big><small><b><big>How to
turn in code:</big></b></small><br>





</big></big>
<blockquote><big>You must turn in the following file:<br>





  <br>





  </big>





  <div style="margin-left: 40px;">chart.cpp<br>





  <br>





  <span style="font-family: monospace;"> </span> </div>





  <big> </big> <big>See the <a href="../general/how_to_turn_in_assignments.html">turn in instructions</a> for details on how to turn in this assignment.<br>
  <br>
Assignments can be turned in up to 24 hours late with a 15% penalty.<br>
</big></blockquote>
<blockquote><big>
  </big>



  <big><br>



  </big></blockquote>




<hr style="width: 100%; height: 2px;"><big><big><span style="font-weight: bold;">Extra Credit: (10 points)</span></big><br>
<br>
</big>
<div style="margin-left: 40px;"><big>If you do the extra credit you have to turn in a second chart.cpp (<span style="font-style: italic;">p1 extra </span>on turnin.ecst).&nbsp; Make sure you do not change/delete your original chart.cpp.&nbsp; <br>
<br>
</big><big><span style="color: red;">No extra credit will be give to late assignments (both the regular assignment and the extra credit must be turned in on time).<br>
<br>
</span></big><big>
In addition to printing the chart pointing "up", also print it pointing
down, right, and left.&nbsp; Include a blank line between each chart.<br>
<br>
For example, the input 4 3 2 1 2 3 4 0 will create the following output:<br>
<br>
</big>
<div style="margin-left: 40px;">
<table style="text-align: left; width: 100px;" border="1" cellpadding="2" cellspacing="2">
  <tbody>
    <tr>
      <td style="vertical-align: top;"><big><span style="font-family: monospace;">*&nbsp;&nbsp;&nbsp;&nbsp; *</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">**&nbsp;&nbsp; **</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">*** ***</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">*******</span><br style="font-family: monospace;">
      <br style="font-family: monospace;">
      <span style="font-family: monospace;">*******</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">*** ***</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">**&nbsp;&nbsp; **</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">*&nbsp;&nbsp;&nbsp;&nbsp; *</span><br style="font-family: monospace;">
      <br style="font-family: monospace;">
      <span style="font-family: monospace;">****</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">***</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">**</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">*</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">**</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">***</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">****</span><br style="font-family: monospace;">
      <br style="font-family: monospace;">
      <span style="font-family: monospace;">****</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">&nbsp;***</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">&nbsp; **</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">&nbsp;&nbsp; *</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">&nbsp; **</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">&nbsp;***</span><br style="font-family: monospace;">
      <span style="font-family: monospace;">****</span><br>
      </big></td>
    </tr>
  </tbody>
</table>
<br>
</div>
</div>
<br>
<br>
