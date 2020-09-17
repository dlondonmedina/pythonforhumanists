# Really getting into Python Now

## Start in the interpreter

I like to start playing with Python in the interpreter. This section will be pretty short, but I'll give you a bunch of lines in Python, which you should try for yourself. Then I'll translate those lines into plain English.

```python
>>> print("Hello, Dylan")
Hello, Dylan
>>> 2 * 2
4
>>> 2 + 2 * 27
56
>>> 2 - 2
0
>>> 12 % 5
2
>>> 12 % 2
0
>>> 13 % 2
1
>>> 12 % 2 == 0
True
>>> x = 27
>>> x % 2 == 0
False
>>> input("What is your name")
What is your nameDylan
'Dylan'
>>> n = input("What is your name? ")
What is your name? Dylan
>>> n
'Dylan'
>>> print("Hello, " + n)
Hello, Dylan
>>> n == "Dylan"
True
```

---
Me: *Please print "Hello, Dylan"*

Python Interpreter (PI): *Hello, Dylan*

Me: *Calculate the product of 2 and 2*

PI: *4*

Me: *Calculate the sum of 2 and 2 times 27 (**Note:** Order of operations is PEMDAS just like in math).*

PI: *56* (Not 108)

Me: *Calculate 2 minus 2*

PI: *0*

Me: *Calculate the remainder of 12 divided by 5*

PI: *2*

Me: *Calculate the remainder of 12 divided by 2*

PI: *0*

Me: *Calculate the remainder of 13 divided by 2*

PI: *1* 

Me: *Evaluate if the remainder of 12 divided by 2 is 0*

PI: *True* (The remainder of 12 divided by 2 is 0)

Me: *Create a variable called 'x' and assign the value 27 to it*

PI: *(Done)*

Me: *Evaluate if the remainder of the value stored in the variable x divided by 2 is 0* (**Note:** This is a really cool way to check if a number is even or not)

PI: *False*

Me: *Prompt the user for some input with the prompt "What is your name"*

PI: *What is your name* (Waits for a response)

Me: *Dylan*

PI: *Your input was Dylan*

Me: *Create a variable called 'n' and prompt the user for input with the prompt "What is your name? " and when they respond store that response to the variable n.*

PI: *What is your name? * (Waits for a response)

Me: *Dylan*

PI: *(Stores 'Dylan' to the variable n)*

Me: *What's n?*

PI: *Dylan*

Me: *Print the string "Hello, " plus whatever value is stored in 'n'*

PI: *Hello, Dylan*

Me: *Evaluate if the value stored in 'n' is 'Dylan'

PI: 'True'

---

That's all pretty much straightforward. You'll notice I added some notes in the parentheses to explain what's going on. Of course, the Python CLI is cool, but once we exit out of it, all the work we did was lost unless we explicitly saved stuff to a file. Wouldn't it be nice if we could write a set of commands that could be run over and over again without having to type them in manually each time? Yes, indeed! That's where Python scripts come in to play. 

## The Anatomy of a Python Script

While we can issue Python commands directly to the Python interpreter in the Python Terminal, we can also write Python to a file that the interpreter will execute. A few things to know:

* Python files are text files with the file extension .py. A file extension is like .docx or .pdf. They tell the computer what type of file this is. 

* Python files contain a sequence of instructions that are executed in the order they are written. 

* When we execute a Python program, we call the file in Bash using the Python program. 

Next, the general layout of a Python program is as follows:

_test.py_
```python
#!/usr/bin/env python3

# This is a comment. Any line beginning with a hashtag is 
# ignored by the interpreter. 

# At the top of our file we usually have import statements 
# if any.
import requests

# Next we will have our instructions. In more complicated 
# programs these will usually reside in Functions, or 
# reusible bundles of code. I'll give you an example of 
# that here.

def website_checker(url):
    r = requests.get(url)
    if r.status_code == 200:
        return True
    return False

# The instructions section is usually quite long.

# Finally, we *might* have a driver section, or the section 
# that calls the functions if there are functions. 

if __name__ == "__main__":
    print(website_checker('https://www.google.com'))

```

In the above program, I have demonstrated the general format of a python script. The very first line is the shebang line. It is not required, but frequently is included in standalone scripts. It serves two purposes: 

1. It allows you to run the script without invoking Python first. Instead of typing ```$ python3 my_script.py``` the shebang line allows you to simply type ```$ ./my_script.py``` to run the script. The Shebang line tells Bash which program to use to interpret the code. 

2. It tells someone who reads your code what interpreter this code was written for. 

The shebang line is not usually included in multifile programs, and I usually only include it in small, utility scripts that I write. Also, if we use the virtual environment, we can run into trouble because if you look closely, the shebang line tries to use the most recent Python 3 executable in the global environment. Support for pointing to the executable in the virtual environment in the shebang line (```#!env/bin/ python3```) is not recommended practice. So likewise, if I'm writing a program that uses a virtual environment, I'll usually also leave off the shebang.

Next, we import any libraries at the top. In this case, I've imported the library that allows me to request data from websites. **Note:** Sometimes we wait to import libraries until later. We'll discuss this later. The second section is where we have the instructions of our program. This is the code that tells the computer what we want it to do. Frequently the instruction section will contain functions, which we discuss in a couple chapters. Sometimes, the instructions are executed on the fly rather than stored in a function. Finally, the driver section exists if you need to call those functions. In larger programs, the driver section is frequently a separate file, and you might actually have a bunch of different files that are make up different parts of your program, but more on that later.

For this chapter, we're going to start with a script that just contains the instructions section without any imports. For my example, I'm going to create a calculator that will allow the user to convert between Kilometers per hour (KPH) and Miles per hour (MPH). Now this is a real problem, perhaps for someone who is accustomed to driving in the USA and is moving to Canada or Europe. How fast is 100KPH really?

Now I'm not going to build a complex user interface. Just a simple text interface for now. I need to prompt the user to tell me if they want to go from MPH to KPH or from KPH to MPH. Then I need to prompt the user to give me the speed they are going. Since I have two pieces of user input, I also need to have two variables to store that information. 

