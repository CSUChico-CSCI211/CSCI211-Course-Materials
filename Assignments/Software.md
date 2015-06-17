#Software Installation Instructions

There are five options for implementing your assignments:

## Option 1: Install Linux on your computer
Installing Linux on your own computer is the best option.  I expect all CSCI & CINS majors to be able to install Linux. Linux is very easy to install.  I recommend using the Xubuntu distribution.  It is based on the ubuntu distribution (ubuntu has a great software installer). See below for installation instructions. This is also the version/desktop environment you will see in the labs.


## Option 2: Use a Macintosh
The Mac operating system is very similar to Linux.  However, Apple recently removed all the GNU software from their Xcode development package.

You will need to use the Homebrew package manager to install the GNU software we need:  g++ compiler, gnu's make utility, gdb, and ddd

I feel the easier option is to use option 3 and just installing a Linux VM and use for local development.  

You will also need an editor. I recommend Sublime or Atom.

## Option 3: Use a Virtual Machine
Install a program on your Window or Apple computer that will allow you to install and run Linux as a program on your native OS.

I recommend using VMware. We have a site licence that allows you to download and install a professional version.

Log into accounts.ecst.csuchico.edu and select Request/Renew MSDN Academic Alliance/VMWare access. Once you request access to MSDN/VMware, you will receive an email (on your @mail.csuchico.edu account) with instructions on how to log in and download software. The email usually arrive the next business day. You will be able to download many Microsoft products (include the OS) and VMware. I


## Option 4: Install the UNIX/Linux emulator Cygwin on your windows machine.
Cygwin allows you to open a command shell window on your windows machine.
It provides all the commands you need to do the class projects.
It takes about 30 minutes to install.
See below for installation instructions.  Make sure you follow them exactly or you may miss something.


## Option 5: Use a remote terminal program to connect to the Departments computers from home.
This is not the best option for two reasons
1. Department machines sometimes go down for entire weekends.
2. You cannot use any graphical programs (such as the scite editor) (actually you can, but it tends to be slow and is hard to setup).
3. You have to copy to files to your computer before you can turn them in (I recommend using WinsSCP or install Cygwin and use sftp).

Download the program putty
Open the application
Use jaguar.csuchico.edu or tiglon.csuchico.edu as the host you want to connect to.
A window should open and ask for your ecst username and password.
You will have to use either the nano or vim editors

The projects in this class will be written in C++.  There is an excellent C++ compiler called g++ available for free from GNU.  Your programs will be tested using the GNU compiler.  If you develop using a different compiler (e.g. Visual C++, Borland C++, etc.) your programs may not pass my testing.

On Apple computers, the Apple C++ compiler pretends to be the GNU g++ compiler.  Run the command "$ g++ --version" to see if you are using the Apple compiler or the GNU g++ compiler.  The Apple compiler will mostly work for 211 projects, but you will not be able to use the gdb debugger.

You will need the following software (the Linux & Cygwin instructions below include instructions for installing all of these):

    GNU's C++ compiler, called g++ (version 4.8 or higher)
    make (a utility for managing the compilation of programs)
    gdb (GNU's debugger for g++) and/or ddd (GNU's graphical debugger)
    an editor: most any editor will work, I use vim but it is hard to learn.  Scite is easy to learn and is installed on the lab computers.  Many students love Sublime.
    a file transfer utility (such as sftp) to copy files to/from your home computer and the Department's computers

All of these are on the department Linux computers, and all are available for Linux, OSX, and cygwin.

NOTE: Software and operating systems are constantly changing.  Please let me know if the following instructions don't work for you.

##Installing Linux Natively

I recommend using the Xubuntu distribution of Linux. There is only one Linux, but there are many distributions. A distribution (or distro for short) is Linux coupled with support software. The main differences between Linux distros are:
1. The installation software/process
2. The application installation software or package manager
3. The default windowing system or GUI. Xubuntu has good solutions for all three of these.  

The windowing system (user interface) for Ubuntu is very annoying. Xubuntu is the same distro as the lab machines so will provide you a consistent windowing environment for local development as well as lab. You can use whatever distribution you want. If the distribution is based on ubuntu, these instructions should work

Step 1: Download Xubuntu (14.04 is a long term release that will be supported for 3 years)

When you download Xubuntu you will download a single file that is an image of a DVD.  Depending on the version you download, it will have a name like this:  xubuntu-14.04-desktop-amd64.iso

Step 2: Create the installation/boot DVD

You need to create a special DVD for installing Xubuntu.  The file you downloaded in step (1) is a special file that contains all the files on the Xubuntu CD.

This Xubuntu page has instructions on how to burn this DVD.


Step 5: Back up all the data on your computer

Step 6: Insert the DVD and restart your computer

The installer will ask you if you want to erase windows first or if you want to install Xubuntu at the same time as windows is installed.

If you want to keep windows, then pick the "with windows" option.

If you want to delete windows (AND ALL YOUR FILES), pick the only Xubuntu box.

You should be able to use the default answers for the rest of the questions.  I recommend using a password on log in so others cannot steal your files.

Step 7: Installing software

A great feature of Xubuntu is how easy it is to install software.  Under the "Applications" menu there is an Install Software button.  This program will let you pick from thousands of applications to install.

There is also a more "manual" way to install applications.  This tool is call apt-get.  You can use apt-get to install the g++ compiler.  At the shell prompt type the following (you must be connected to the internet for this to work).

$ sudo apt-get install g++

That is all you have to do.  And there are thousands of other applications you can install using apt-get.  Usually if I want an application I just try apt-get to see if it is there.  For example,

$ sudo apt-get install scite

All the other software you need should already be installed... but if you are missing something, try using apt-get.

##Cygwin Installation (do this if you want to use windows w/o installing VMware)

If you choose to use windows without installing a virtual Linux, you will need to download the Cygwin Linux emulator.  Cygwin allows you to open Linux-like windows on your Windows PC  (it works on all flavors including Windows-7 and Windows-8).  It will allow you to write your entire program on your computer and then copy it to a department machine for final testing (recall that all programs will be tested using a Linux computer).

Here are the steps for installing Cygwin on your windows machine

<pre>
    Using windows explorer create a directory c:\cygwin
    Go to http://www.cygwin.com and download setup-x86.exe for 32bit and setup-x86_64.exe for 64 bit (from the install page), and copy it to c:\cygwin
    Run c:\setup-x86_64.exe      -or -  c:\setup-x86.exe
    Choose "Installation from Internet"
    press <next> button
    Type "c:\cygwin" as the root directory  (this should be the default)
    Leave the "all Users" and "Unix/binary" buttons checked
    press <next> button
    Use c:\cygwin as the package directory (this should be the default)
    press <next button>
    Leave the "Direct Connection" button checked
    press <next> button and wait until the list of servers has been downloaded
    select a web-site to download from.  I try to pick something I think is close.  They all should work.
    press <next> button and wait
    Eventually, you should now see a menu of items to select for download.  When you click on a "+" it opens the sub-directory.  Then select the "Skip" and the "Skip" will be replaced with the version you will download.  Some of these might already be selected.
        from the Devel menu select
            ddd
            gcc-core: C compiler
            gcc-g++: C++ compiler
            gdb
            make
        from the editors menu select at least the following
            vim
            gvim
            nano
            any other editor you may want to use
        from the Utils menu select
            cygutils
        from the Net menu select
            openssh
    press the next button
    if asked if you want to include additional libraries that are required, answer yes
    wait for cygwin to download (this can take 10-30 minutes depending on your internet connection and the speed of the download site you are using)
    Leave the "create icon on desktop" and "add icon to start menu" boxes checked and press finish.
</pre>

Now you are ready to use Cygwin.  If the following tasks work, you probably have Cygwin installed correctly:

<pre>
    Open a Cygwin window by clicking on the Cygwin icon.  It should be a window with a black background and the prompt will probably be a $, but might be something else
    Type pwd <enter>  (<enter> means to press the enter key).  This is the directory that cygwin has set up as your home directory.
    Create a test C++ program or download a test C++ file from my website.  In the following, replace the USERNAME with your ecst username
        sftp USERNAME@jaguar.ecst.csuchico.edu
        answer yes to the security question
        enter your ecst password
        the prompt "sftp> " should be on the screen
        type the following EXACTLY:  get   /var/www/tyson/211/example_src/hello/hello.cpp
        type quit
    Now check to see if hello.cpp was downloaded to your current directory using the ls command:  $ ls
    If it is there you can compile and run it:
        $ g++ hello.cpp
        $ a.exe
    If you see "Hello world." on the screen your install is correct.
</pre>

If the program does not run (the bash shell will tell you that it could not find a.exe) then try the following:

$ ./a.exe

If this works the PATH variable does not include the current directory.  That means if you try to execute a file in the current directory, the shell will not find it.

You can modify the PATH variable so it include the current directory.  Search for PATH on this cygwin documentation page to find out how to change it and add the current directory "." to your PATH.
