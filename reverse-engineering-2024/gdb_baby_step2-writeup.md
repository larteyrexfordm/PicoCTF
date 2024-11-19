These approaches aim to offer different ways to work with GDB and debugging so that you can adapt depending on your preference.

Welcome to the GDB Baby Step 2 Reverse Engineering Challenge 

In this guide, we'll dive into the GDB Baby Step 2 challenge with some alternative approaches and commands. GDB is a powerful tool, and there are different ways to use it to explore a program and uncover its secrets. Whether you're new to GDB or looking to try different methods, this guide will walk you through the challenge step-by-step.


What is GDB?

GDB (GNU Debugger) is a tool that lets you “pause” a running program to examine what’s happening inside. It’s like using a magnifying glass to look closely at the program’s memory and code.

Why GDB?

It helps find bugs or errors in programs.

It allows you to see hidden data (like our flag!) in running programs.

It’s essential for reverse engineering because you can see exactly what’s going on under the head of a program.

Before we start, we need to get the file from PicoCTF for the GDB Baby Step 2 challenge.

Download the file named debugger0_b to your computer and place it in a folder.
wget url_of-the_challenge_file

Preparing GDB

Setting up the Debugger:
You’ll need a working terminal to interact with GDB. If you're using Kali Linux or any Linux-based OS, you should already have GDB installed. If not, you can install it by running:

sudo apt-get install gdb

Once it's installed, open a terminal and navigate to the folder where you downloaded the debugger0_b file.


Alternative Approaches for Debugging the Program

Now, let’s use alternative approaches to explore the program in GDB.


Step 1: Opening the Program in GDB

To begin, let’s open the program with GDB. The first approach uses the gdb command, but let’s also try an alternate command to launch the program:

Standard Command:

gdb debugger0_b

Alternate Command (with file and gdb options): If you want to specify the program file separately, you can type:

gdb -q debugger0_b


This suppresses extra info and just opens the file in GDB right away.


Step 2: Changing Disassembly Flavor

By default, GDB uses AT&T syntax for assembly code, which can be a little tricky for beginners. The Intel syntax is often easier to read. Let’s change it:

Standard Command:

set disassembly-flavor intel

Alternate Approach: You can also change the disassembly style by typing:

disas-flavor intel


This works the same way as set disassembly-flavor intel.


Step 3: Finding the Main Function

To find the main function, we need to list all the functions in the program. There are several ways to do this in GDB.

Standard Command:

info functions

Alternate Approach:
You can also use the display command:

display /r


This will list the addresses of all functions in the program, which is helpful for finding the main function.


Step 4: Disassembling the Main Function

Once we’ve found main, we want to see the actual assembly code. The standard method is to disassemble it:

Standard Command:

disassemble main

Alternate Approach: Instead of using disassemble, you could also use:

x/10i main


This will examine 10 instructions from the start of the main function and display them. It’s a quick way to see what's going on.


Step 5: Setting Breakpoints

Now we want to stop the program at key points to examine it. First, let’s set a breakpoint at the main function.

Standard Command:

break main

Alternate Approach: Instead of setting a breakpoint at main, you can set it at the return address (0x401142):

break *0x401142


Setting the breakpoint at the return address is an alternative to stopping the program when it first enters main. It helps us focus on the program’s end.


Step 6: Running the Program

We’ll let the program run until it hits our breakpoint. The standard command is run, but there’s also a shortcut for it.

Standard Command:

run

Alternate Command (with continue): Instead of using run, you can use the continue command to resume the program after it pauses:

continue


Step 7: Getting the Value of the EAX Register

The key to solving this challenge is checking the value stored in the EAX register. We can do this with two commands:

Standard Command:

print/d $eax

Alternate Command: You can also use the info registers command, which shows all registers at once:

info registers


Look for the EAX register in the output to find the hidden number.


Conclusion: Extract the Flag

Once the program stops at the return point, you’ll find the value inside EAX. The hidden flag will be:

picoCTF{307019}

This is your flag!


Final Thoughts

Using GDB to solve challenges like this one might seem complex at first, but with practice, you’ll get more comfortable exploring programs and finding hidden data. By using different commands and approaches, you can find the method that works best for you. The key is to keep experimenting and learning. Reverse engineering is all about trial and error, and every time you debug a program, you're improving your skills!


