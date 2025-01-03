<h1><b>Reverse-Engineering: GDB BABY STEP 1</b></h1>

<h2>Tackling PicoCTF-2024 Reverse-Engineering Challenge: GDB Baby Step 1</h2>

If you're diving into reverse engineering or want to get familiar with the GNU Debugger (GDB), this guide will help you tackle the PicoCTF “GDB Baby Step 1” challenge. GDB is a powerful tool for debugging and reverse engineering, often used by security professionals and developers to understand how programs work at a low level.

<b>What is GDB?</b>

GDB stands for the GNU Debugger, a tool that allows you to inspect and control the execution of a program. It’s mainly used in Linux environments and helps programmers "see" inside their programs as they run. With GDB, you can:

<b>Disassemble code</b>: Break down the program to understand its logic.

<b>Inspect registers</b>: View the contents of the CPU's registers to see how data is handled.

<b>Set breakpoints</b>: Pause the program at specific points to investigate its behavior.


In reverse engineering, GDB is vital for dissecting compiled programs and understanding how they work without access to the source code.

<h3>Getting Started with the Challenge<h3>

 <b>Setup</b>: Use a Kali Linux virtual machine (VM) and download the “GDB Baby Step 1” challenge from the PicoCTF website by using the syntax:
 
```wget link_to_the_challenge``` 

to download the challenge file


 <b>Granting Executable Permissions</b>: Before running the file, you’ll need to make sure it has the necessary executable permissions. You can use this command:

```chmod +x debugger0_a```

<b>Alternatively</b>, if you prefer, you can also use:

```sudo chmod 755 debugger0_a```

This grants full permission to the file and makes it executable.


<b>File Analysis</b>: Once downloaded and made executable, check the file type by running:

```file debugger0_a```

You could also use the ls -l command to confirm the permissions:

```ls -l debugger0_a```

The result shows that it’s an ELF (Executable and Linkable Format) file, a common format for Linux executables. This file is 64-bit and not stripped, meaning we can see its symbols and debug it easily.



<h3>Disassembling with GDB</h3>

Now, let’s use GDB to disassemble and explore the code:

Start GDB with the following command:

```gdb debugger0_a```

<b>Alternatively</b>, if you prefer a more compact command for starting GDB with your program, use:

```gdb -q debugger0_a```

The -q flag will start GDB in quiet mode, avoiding unnecessary startup messages.


To list all functions, type:

```info functions```

<b>Alternatively</b>, use the nm tool to list the symbols (including function names) in the binary:

```nm debugger0_a```

This will give you a list of symbols, including the main function.


Change the disassembly format to Intel syntax (more familiar for many users):

```set disassembly-flavor intel```

Another <b>alternative</b> to this step would be to directly change the syntax to Intel in GDB’s configuration file, but the above command is a quick and temporary solution.

Disassemble the main function:

```disassemble main```

An <b>alternative</b> approach would be to use objdump to disassemble the binary:

```objdump -d debugger0_a```

This shows the disassembled code of the program, allowing you to locate the value stored in the EAX register.


To convert the hexadecimal value to decimal, use Python or any other tool you prefer:

```python -c "print(int(0x86342))"```

<b>Alternatively</b>, you can use an online converter or a simple bash script:

```echo $((0x86342))```

This will return the decimal value 549698, which is the flag: picoCTF{549698}.



<h2><b>Alternative Debugging Method</b></h2>

For a more hands-on approach, you can use GDB's debugging features:

Set a breakpoint at the main function:

```break main```

<b>Alternatively</b>, you can use b for short:

```b main```


Run the program:

```run```

A shorthand for run is r, so:

```r```


Use layout asm for assembly code visualization and step through the code with ni (next instruction) until you reach the instruction that loads the value into the EAX register. Instead of using layout asm, you can also use:

```disas```

to display the disassembled code directly within GDB.


To view the value in EAX, type:

```print/d $eax```

<b>Alternatively</b>, use the shorter version:

```p/d $eax```

This will show the value 549698, confirming the flag.




<b>By using GDB, you’ve learned how to inspect a program’s code, understand the contents of registers, and find the hidden flag. This is a fundamental skill in reverse engineering, and with more practice, you can take on more complex challenges.

It's not a crime to start small. Enjoy learning and tackling more CTF challenges—they’re a fun way to learn and grow in the world of hacking.</b>


