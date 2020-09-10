# A Taste of Python

## File Structures

Before we get too far into Python, there's one thing you need to understand very well. That is file structures. Your files are stored the computer in a hierarchical structure. A good way to think of it is as a tree starting from the root.
```
    / or c:\ [The root directory. Everything is within this directory]
    /bin
    /opt
    /var
    /home
        /user1
            /Documents
                /3010
                    /code
                        my_function.py
                        hangman.py
                        anotherprogram.py
                /Articles
                    transitions.docx
                    techofhate.docx
            /Desktop
                hangman.py
            /Videos
            /Pictures
```
If you look at the directory above, in the root I have the directories bin, opt, var, and home. These directories are at the same level, so they are called siblings. Each of these is a directory within the root, so the root is the parent. In Windows, the root is "c:\" and folders will likely have different names, but the structure is similar. If we look at the "home" directory, we have a directory called "user1", and within that a few directories, including Documents, Desktop, Videos, and Pictures. Documents contains directories 3010 and Articles. user1 would be called a child of home. 3010 contains the code directory. /code and Articles both contain files.

When I want to identify a file, I can identify it with its absolute path. This is the path from the root to the file or folder I'm identifying. So to identify the absolute path of hangman.py, I would need to call it /home/user1/Documents/code/3010/hangman.py. Likewise, to identify transitions.docx, I'd need to call it /home/user1/Documents/Articles/transitions.docx. Using the absolute path in a command or in code will guarantee that the computer can find a file I'm looking for. In commands and programming, it's important to note that unless we use a search function, the computer will not be able to "search" for a file. So, if I am working in /home/user1/Desktop and I issue the command python hangman.py the computer will look for hangman.py in my current working directory, and since there is no file called "hangman.py" in that working directory, it will be unable to find the file, and the terminal will throw a File Not Found error.

What's going on here? Why can't the computer just know what file I'm talking about and run it. After all, it's stored in the memory, right? Yes, but there may be multiple files called "hangman.py" in different directories. That is totally legal in terms of storage, and maybe even reasonable practice. After all, you might be working on 100 websites on your local server, and each of them will have an "index.php" or "index.html" file because the web server looks for that. When entering commands or executing programs, don't want your program to stop and say, "which hangman.py?" every time you try to reference a file. To address such possible collisions, computers use something called "namespaces." We'll think about this more later, but for now think of it as the "working context" in which your program is running. When you type pwd into your terminal, it tells you what the working context is, or where your terminal is focused. When you issue a command or write a line of code that references a named entity like a variable or a file, it looks for that entity or file in the working context unless you specify otherwise. This means that if you're working in /home/user1/Documents/code/3010 and you enter python hangman.py it looks only in the 3010 directory even though there is a hangman.py in Documents (see above).

The thing to understand now is that the working context is where the program looks for named entities. If that entity (a file or variable) doesn't exist in that context (in that directory), then the program won't look elsewhere. It will throw an error. This is true for executing code and for changing directories. Let's say I'm working in the root directory (/). If I want to change directories to code/ I can't simply say cd code because there is no "code" directory in the root. Instead, I have to explicitly give the terminal the path to that directory with this command cd home/user1/Documents/code Let's break down how this is interpreted:

* Computer change the working directory to code

* which exists inside Documents,

* which exists inside user1,

* which exists inside home,

The terminal is currently in the root. /home/ exists in the root so it can find that. Then inside /home/, user1/ exists as a directory, so it can find that. Then inside user1/, it can find Documents/ because that exists there. Finally, inside Documents/ it can find code/

I hope I'm not belaboring this too much, but it is crucial, especially as we move into next week to consider scope. You might know exactly where all of the files are located at. That's how a human brain works. We can create nice conceptual maps that help us infer stuff. Computers do not infer. If try to use a named entity (file or variable) in a different context (like calling a python script from another directory), the computer will only look in the local context unless you give it an explicit path to find that entity. It will never infer that you mean the "hangman.py" in /home/user1/Documents/code/3010/ and not the "hangman.py" in /home/user1/Desktop/

In short, remember, that you must be really explicit when you leave the comforts of a graphical interface like the Finder or File Explorer.

## Compiled versus Interpreted Languages

### Compiled? Interpeted? What the What?

Generally when we talk about programming, we are talking about a human readable programming language that is easy for a human to understand. However, if we look at what's actually happening on the processor when the commands are being executed, those commands are in binary, or sets of on and off switches. Here is a miniature example of what addition looks like in human readable form and the binary operation that occurs on the processor when a computer calculates it:

Human Readable:
12 + 11 = 23
Assembly Code:

Binary Operation:
1100 + 1011 = 10111

I'd recommend that you take a moment to search for the binary representation of 23 and you will find that it is 10111.

Why does this matter? A processor can't do anything with 23 until it is converted to binary, which are then converted to a series of charged and uncharged states, or a series of ON or OFF switches. It can, however, do operations with these sequences of electrical charges, and a great deal of work is done by the computer to translate between human readable and machine readable forms.

For us, this means that every line of code eventually is converted into binary, and so what matters to us is how our code becomes binary. This leads us to compiled versus interpreted languages. The code we write, whether in Python or Java or C++ is written in human readable form. This means that we can understand it, and Python is particularly understandable. But the code must either be compiled or interpreted for it to run. 

### Assembly and Machine Code

I'll discuss the difference between compiled and interpreted in a moment, but there is a crucial intermediary between binary or bytecode and our high level programming languages. This intermediary is called assembly. Assembly is low level programming language that is a little bit human readable, but it is representations of specific commands that are executed by the processor. In other words, for a computer to perform an operation like 12 + 11, it would be one line of code in Python, but would require a number of operations on the processor to complete the summation. For instance, the computer needs to load the binary representation of 12 and 11 into registers (tiny bits of memory) on the processor. It needs to perform the operation on the binary values in each of the registers. The computer needs to write the result to another register and then send the decimal value of the result to the screen (which is a couple more steps). Assembly language contains the series of commands that cause the processor to do this. Assembly has a 1 to 1 relationship between command or line of code and operation performed by the processor. The translation between Assembly and the binary that the processor reads is done by the Assembler, which is processor specific (so an x86 and x64 processor would have different assemblers and different Assembly languages).

You don't really need to know anything more about Assembly for our purposes except that all of the code we write is probably going to be converted into Assembly. Interpreted and Compiled is largely a difference in when and how that occurs.

### Compiled Languages

Many programming languages are compiled. C++ and Java would be two examples. This means that a programmer writes their program, and then they run it through a compiler, which is a special program that converts the high level language into either an "executable" file of Assembly or some other low level language (often .exe in Windows) or directly into binary as is the case on some mobile phones or single board computers. To run the program, the programmer would not run the code written in the high level language (the source code), but instead would run the compiled executable which is the low level translation of the source code.

Compiled languages have the advantage of being much faster to execute because at runtime the computer is reading assembly instead of the high level language (this will make more sense when I talk about interpreted languages). They are also slightly more complicated and often a little more difficult to learn. The communities online that surround C++ and Java, two high-level compiled languages, are also a little more grumpy towards newcomers than Python.

### Interpreted Languages

An interpreted language does not need to be compiled. Instead, the programmer writes in the high level language. Then they run the program using the interpreter (in our case the Python program). At runtime, the interpreter reads the source code, converts the source code to lower level code like assembly. That lower level code is then executed by the processor.

Notice, compiled languages are turned into executables and when we want to run the program, we don't run the source code, we run the executable which doesn't need to be interpreted into some lower level language at runtime. Interpreted languages on the other hand must be first interpreted into a lower level language and then executed, all at runtime. This can make things really slow.

Python has a few tricks to address this deficiency. First, when we execute any Python script, you'll probably see a __pycache__ folder created. In that folder, Python saves an interpreted version of the program in cache. This way, if Python has to run a program again, it will check to see if the program is the same in the cache first and if so, it will not re-interpret the source code, but run the cached version. If there is no cached version or if changes have been made, Python updates the cache and interprets the source code. Developers have also created Cython, which allows the developer to write Python or Cython code but get performance like that of a compiled language. This is a bit beyond the scope of this class, however.
Do I need to know all of this?

No, not really. I won't be testing you on it, but hopefully it will help you have some context around programming and programming languages. It is definitely going to be important to know the difference between a compiled and interpreted language, but the details of how they work (how programs are compiled or interpreted) is not something you need to know unless you get really serious about programming or get into computer science.

## Now Python

![Python with I'm a dad hat](img/dadsnake.jpg)

Python refers to two related things. First, Python refers to a programming language that we use to give commands to our computer. This we'll talk at length about throughout the quarter. Second, Python refers to the program that runs on your computer that interprets the code that you write. Dr. Chuck talks about this to some extent in the book. Python the program converts your code into machine language that causes your computer to do things. Just like any program, Python is regularly updated and has minor and major versions. You'll hear almost immediately when looking at Python that there are two major versions: Python2 and Python3. Python 2.7.14 is the most recent version of Python2, and Python 3.8 is the main version of Python3. When we talk about Python version, we're talking about which version of the Python program we're using to interpret our code (we're also talking about our code, but more on that later).

This difference is pretty important because as the language evolves over time, some of the features stop working or the syntax, or the way we write code, changes. For example, if we want to print some text to the screen, we use the "print" method. In Python 2 the syntax was this:

```
print "Hello, Snek!"
```

and for the same functionality in Python 3 you have to write:

```
print("Hello, Snek!")
```

The Python3 interpreter would throw a Syntax error because it no does not recognizes the "print" function without parentheses. In short, as the Python program is updated, the way we write Python code has to change to account for the expectations of the interpreter. Does this mean that we have to update all of our code? Not necessarily. It does mean we need to be concerned with which version of Python we're writing for and which is running our code.

In this class you will be writing code for a Python3 interpreter or you will be writing Python3 code, but it is good to be familiar with some of the major differences. We'll talk about them as they come up. What is important, though, is that you will need to make sure the Python3 interpreter is installed on your computer.

## Python Interpreter

When we write Python programs, we're usually writing a series of instructions to a file. When we run the program, we tell the Python interpreter to open the file and read and execute the instructions that are contained therein. However, we can also issue commands to the Python interpreter in the same way we can with Bash. The Python CLI can be opened by launching Python without specifying a script. You'll notice before that I just need to type ```python``` in Windows and ```python3``` in Mac/Linux because in the latter I have both Python 2 and Python 3 installed.

### Windows
```
~$ python
Python 3.8.3 (tags/v3.8.3:6f8c832, May 13 2020, 22:37:02) [MSC v.1924 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

### Mac/Linux
```
~$ python3
Python 3.8.2 (default, Jul 16 2020, 14:00:26)
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

You know that you're in the Python interpreter because of the three greater than (```>>>```) symbols. Once there, we can play around. I recommend you follow along. 

```python
>>> 2 + 2
4
>>> 2 * 8
16
>>> 2 * (18 + 72)
180
>>> print("Hello, world!")
Hello, world!
>>> sorted([18, 27, 2, 9, 6])
[2, 6, 9, 18, 27]
>>> type(2.7)
<class 'float'>
>>> type(2)
<class 'int'>
>>> type('Puppies')
<class 'str'>
>>> exit()
~$ 
```

What you see here is a sequence of commands that I sent to the Python interpreter in the Python programming language. On the prompt lines (preceded by ```>>>```), I entered my commands. On the following lines is the response of the Python interpreter. Kind of like a conversation:

---

**Me:** *Python, please add 2 and 2.*

**Python:** *4*

**Me:** *Python, please multiply 2 and 8.*

**Python:** *16*

**Me:** *Python, please first add 18 and 72, and then multiply that sum by 2.*

**Python:** *180*

**Me:** *Python, please print to the console the string "Hello, world!"*

**Python:** *Hello, world!*

**Me:** *Python, please sort the list of numbers 18, 27, 2, 9, and 6 in ascending order.*

**Python:** *[2, 6, 9, 18, 27]*

**Me:** *Python, please tell me what type of data 2.7 is.*

**Python:** *It is a floating point decimal*

**Me:** *Python, please tell me what type of data 2 is.*

**Python:** *It is an integer.*

**Me:** *Python, please tell me what type of data "Puppies" is.*

**Python:** *It is a string*

**Me:** *Please exit, python*

**Python:** *exits and returns to Bash prompt*

---

If you followed along with the code above, you just coded your first bit of Python. Congratulations! Generally, when we code Python, we write the commands into a text file and then the interpreter executes them when we tell them to do so, but for now, we have cut out the middleman of the file and written our commands directly to the interpreter. It's important to note that the commands are executed in the order we give them. The same is true when we write our code into a file. The interpreter will execute those commands in order. This is the project for next chapter, so I will leave it at that. You've just gotten your first taste of Python. 

## Virtual Environments

You might be wondering, how do we keep all the versions of Python sorted out? That's a good question and it extends to all the other libraries that we install. When we use someone else's code, we're taking on dependencies. As they update their code, we might have used an older version, so we need to make sure that we don't accidentally pull in the newer version of their code because it might no longer be compatible with our code. Also, we ourselves could write a program in 2020, but within the next year probably, Python 4 will be released. This means that if we update to Python 4 on our machine, our code will probably break because there will be changes in how Python is written. We need a way to make sure that the same version of the Python interpreter is always used to execute our code. We manage this and all of our dependencies using what's called Virtual Environments. These allow us to bundle up our code and dependencies at a frozen moment in time, and isolate that project's dependencies from other projects and versions of Python.

Managing Virtual Environments has become extremely easy. There are a number of tools to do so including **pipenv** and **venv**. We'll be using **venv** here because it is included when you install Python, and where it stores the virtual environment directory is a bit more obvious. To launch it we simply tell Python to execute the **venv** module. To tell Python to use a module, we need to use the ```-m``` flag. 

```
$ python3 -m venv -h
usage: venv [-h] [--system-site-packages] [--symlinks | --copies] [--clear] [--upgrade] [--without-pip]
            [--prompt PROMPT]
            ENV_DIR [ENV_DIR ...]

Creates virtual Python environments in one or more target directories.

positional arguments:
  ENV_DIR               A directory to create the environment in.

optional arguments:
  -h, --help            show this help message and exit
  --system-site-packages
                        Give the virtual environment access to the system site-packages dir.
  --symlinks            Try to use symlinks rather than copies, when symlinks are not the default for the platform.
  --copies              Try to use copies rather than symlinks, even when symlinks are the default for the platform.
  --clear               Delete the contents of the environment directory if it already exists, before environment
                        creation.
  --upgrade             Upgrade the environment directory to use this version of Python, assuming Python has been
                        upgraded in-place.
  --without-pip         Skips installing or upgrading pip in the virtual environment (pip is bootstrapped by default)
  --prompt PROMPT       Provides an alternative prompt prefix for this environment.

Once an environment has been created, you may wish to activate it, e.g. by sourcing an activate script in its bin
directory.
```

My command was ```python3 -m venv -h```, which basically means "Python, execute a module called venv and send the -h command to it." You can see from the help article that is returned that when you send the ```-h``` command to venv, it displays the help article. Now we can look at the general syntax for using **venv**. First, it's worth noting that I called ```python3``` rather than ```python```. If you're in Windows and only have Python 3 installed, or if you plan to use Python 2 in Mac or Linux, you would call ```python```. You'll see that there is a required, positional argument. We'll learn about arguments when we talk about functions, but for now, think of it as a bit of extra data that will be used by the program. Specifically, in this case it is an ```ENV_DIR``` which probably stands for environment directory. This means we need to give the command a name of a directory where the environment data will be stored. This does not mean the name of the directory for the project, but some other name that we can remember is our virtual environment directory. Let me show you the code first, so maybe it's a bit more clear. 

```
$ mkdir my_project
$ ls
my_project
$ cd my_project
$ ls

$ python3 -m venv env
$ ls
env
```

Ok, first I made a new directory for my project and changed into that directory. I'm using ls to show you what is there. Next, I used **venv** and created an environment in a directory called ```env```. This ```env``` is arbitrary. I choose to call the directory "env" because it's known and makes sense. You could call it "puppy" or "an_environment_directory" but that would make less sense. Also, it's worth noting that the env directory was created by venv. I didn't need to create it first. Finally, you'll never need to manually change anything inside that env folder. Just create it and leave it alone. The package management tools will manage the environment for you.

Our next step after creating the resources for our virtual environment is to activate it. Once the environment is activated, whenever we use Python, we will be using the one in this environment. This means that our commands to call Python will always be ```python``` rather than ```python3``` because in **THIS** environment there is only one version of Python installed. So let's activate our environment:

### Mac/Linux

```
~/my_project$ source env/bin/activate
(env) ~/my_project$
```

### Windows

```
~/my_project/~ env\Scripts\activate
(env) ~/my_project$
```

In both cases we run the activate script to launch our virtual environment. Pay attention to the ```(env)``` bit because that tells you your Bash prompt is working in that virtual environment. If this all seems a little confusing now, that's okay. It becomes much more clear with practice. Now that we have our virtual environment created and activated, we can start working.

## Pip and Pip Freeze

When we use Python, we probably will be installing libraries that other people have created. These libraries give us functionality that allows us to avoid having to write a bunch of stuff. We'll talk about this in detail in a few chapters, but for now, consider the work it would require to connect to a website. First, we'd need to use sockets to get our network card to connect to the internet. Then we'd need to build our requests. Then we'd need to listen for a response and so on. Instead, I can just install the **requests** library that someone else built and maintains, and all that work is done for me. I just use functionality that is build into **requests**. We do the same thing when we use a web browser, but a web browser has more functionality built in and is used predominately through a GUI. 

More on this later. For now, we just need to know how to install and manage our virtual environment and the packages that are installed there. To install a package the command is simply ```pip install {package name}```. We'll again talk about this at length in a few chapters. For now, what is most important is the ```pip freeze``` command. If we just type that in our Bash terminal the list of packages and their version numbers will be printed to the screen. In general, we will issue the ```pip freeze``` command with the output being written to a file called **requirements.txt**. This will allow us to track the single file in our git repository rather than the entire **env/** directory.

## Conclusion

This chapter was a brief introduction to Python and is designed to prepare you for the next chapter. In the next chapter, we'll discuss the first lessons in Python programming. We'll cover the basic syntax and variables. 
