#SLIDE 1(00:00-02:12)
You should be absolutely clear at this point that a terminal is just a dumb
device for displaying text characters on the screen, and for sending text
characters from the keyboard to a program that wishes to read them.  Without
programs reading from terminal and writing to it. Terminals are pointless.

What we call a shell in Unix is a program which reads from a terminal and then
interpret what user entered as a command and executes that command. 

Effectively a shell is an interpreter for a programming language, it is just
the expectation of the shell  that the user typing the lines of code one by
one, and each time they enter a line of code the shell then immediately
executes it. So we can see a shell is like an interactive programming
language, The user types a command, and then the shell immediately executes
that command.

For many years the most widely  used shell on Unix systems was known just as
sh, for shell, but more formally known as the B shell, because it was created
by a guy named Steven B. For the most part, all the other shells have been
used at one point or another that are listed here are really just variations
on the original B shell. Most of them takes the core of B shell and just takes
in the additional features.

Perhaps the one exception here is the csh which changes a few things about the
syntax of the  of the original B shell, as well as adding additional features.
The Ksh for example is so called because it is created by a guy named David
Korn, was created a few years after the B shell and mostly adds things rather
than changing anything about the core shell syntax and features. Of all the
shells listed here, the one you need to become most familiar with and the one
we are going to focus on is Bash( aka the B again Shell)

Bash was created in the late 80s by a GUN project and so it got adapted as the
effectively default  shell in Linux systems.  So in fact, most of the time you
open up a terminal window on a Linux system it will  most likely by default
have the bash shell running in it.

Again bash shell is pretty much just the a extension of the original B shell.
I do not believe there is actually anything that they changed about the
original shell, they just added more features. 

#SLIDE 2(02:12-04:40)
So say I boot up my Ubuntu system and the X window server then starts and
finally my whole graphical desktop there is loaded and ready to go. If I then
open a terminal program I will get this terminal emulator window, and in it is
running the bash shell because that is the default on ubuntu systems.  And as
you see here, what I am presented with is first a prompt, and the prompt
displays my user name followed by the name of the system, which here is just
happens to be ubuntu I suppose, that is then followed by colon after which is
listed the path of the current working directory of the shell. Recall that
every process in Unix has associated with it a current working directory is
sometimes called the process working directory. 

In this case as listed as tilde, because in Bash syntax and sh syntax, tilde
is used as special signifier, a special shorthand for my home directory , so
really what should be printed here is /home/brian and this is just a shorthand
. We will talk more about the special meaning of tilde a bit later. And in
this case so after listing the current working directory, there is a $ sign
which simply denotes the end of the prompt. 

And then after the prompt there is a space and my text cursor where if I start
typing, that is where my text is going to start appearing. Because when the
shell is waiting for you to enter command, it puts the terminal into the
echoin mode. 

So now I can type a command and as I type it the characters will appear in the
terminal, and once I hit enter the shell usually interprets the newline
character as the end of a command. So it will then interpret that command and
execute it. 

Before getting in to the details of bash syntax and semantics, also remark
here that shell languages have what I like to call a command based syntax and
semantics, in contrast to the expression based syntax languages we've seen in
languages like Java script python. This stems from a very different design
goal. Shells are mainly about not writing whole bunch of code that runs with
the shell, but writing code that simply launches other programs.

So while it is perfectly possible in say, python to launch other programs, it
is not made specially convenient, because python is mainly about writing code
to run directly in the python interpreter, not to run as separate processes.
Whereas in shell, mainly what is about is running other  programs. 

#SLIDE 3(04:40-05:00)
So this difference of purpose is what explain the reason  behind the syntax
for the basic kind of the command what I call the process command.

A process command is written by specifying the name of the program, and then
after one or more spaces,
we will put  a list of arguments. And the arguments as we will see are not separated
by commas, they are just separated by spaces. 
#SLIDE 4(05:00-05:26)
So for example a process command might
read ls -la bin. And what this is is first the program name ls and followed by
two arguments the first -ld , the second bin.what is going on with these
arguments we are talking about in a moment, but looking first at the program name
if this is the name of some program, some  executable file somewhere on the
system how does the shell know were to find it? 

#SLIDE 5(05:26-10:42)
Well actually there are
there different cases. When you see a program name with no slashes in it, then
the shell will search executable file of that name in one of the directories
listed in what is called the PATH, the path is simply a environment variable
in the shell process. 

So for example , this is what the path variable looks like in the shell on my system. It
has a list of directories separated by colons. First /usr/sbin then
/usr/local/bin/ then /usr/sbin/and /usr/bi/ and /sbin and /bin/.

These are
the directories in the my path. So in my shell when I run the command foo,the
shell will first look for a executable  called foo in each one of the directory,
starting with the one listed first, going left to right. And it goes to the first match it
finds. Assuming it did not find any match then the shell reports a error,
saying
there is no such program called foo.  So that's the first case when I do not
have any of the /es in the
name of the program. 

when the name starts with a / then the shell interprets this as a absolute
path to a executable
file. So in this case /bin/foo, the shell will look for that file and if there
is not that program of that name the shell reports a error saying hey there is
no such program as /bin/foo

The last possibility is that there is / in the name but not at the start. This is then
interpreted by the shell as a relative path name, so it  will look for that path relative
from the process working directory, the current working directory of the shell
itself. And this is one reason why the shell will display the current
working directory. Because it is something you often need to know. So for
example assuming the process' working directory is currently in my home
directory /home/brian/ this will look for the file /home/brian/bin/foo and of
course if there is no such executable file then the shell will give you a
error message.

One thing that almost always tricks newbies is that when they type say foo, to
look for foo in the current directory rather than just in the directories of
the PATH but this is not the case. As just explained, the shell only looks at
the current working directory when there is a / somewhere in the middle of the
name.  The trick than is run foo in the current directory is not to write just
foo, but to write ./foo 

What is going on here is that in a Unix system, every directories always
contains an entry called dot which refers to that directory itself. This is a
special entry that is added to every directory that we create. So when we
write ./foo, that is a relative path, that is  want just foo.  It is just in
this case will trick the shell to looking in the process working directory
before looking at the path. 


We mentioned in Unix directories also always contain a directory called ..
which resolves to the containing directory.  So for example a path that reads
/home/brian/.. that actually resolves to the same things as /home. Like the
dot entry the .. entry is sometimes useful when we write relative path names. 

In any case getting back to our example process command that begins ls,
you can see the program name here has no /es in it. So the shell is going to
look at it in the path. The motivation behind the path mechanism is
that there are a number of programs that in the system that we want the
convenience to be able to run without having to switch to the directories or
having to write out their full path names. So we place these programs in a
number of
standard directories , like /bin or /sbin/ or alternatively we add
the directory in which the program is contained to our path, that way we can execute them
without having to write out their full name. 

In this case. ls is a standard Unix program, sometimes called the list program,
because what is does is to list the contents of a directory it prints out
on your terminal, prints out the contents of some directory. And on most Unix
systems ls is going to found is the /bin directory, cause /bin is a
standard directory for general programs, general common programs. 

The /sbin
directory is  so named because it is for programs with superuser
privileges, hence s, and so you place in there the programs which do things that
have to do with system administration, generally. 

As for the other directories in the path, the /usr directories, we will
talk more about the standard directories layout in  Unix system in a
supplementary unit. 


In any case that explains how a shell locates a program, well what about these
arguments? And how exactly does shell then executes the program, well anytime
in Unix, you have a program executing another program, what is going to
involve is first a fork system call and then a child process that gets created
invokes the exact to actually load the program and run it. 

#SLIDE 6(10:42-