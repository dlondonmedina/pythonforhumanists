# Really getting into Python Now

In the last chapter we discussed Python in pretty abstract terms. In this chapter, we are going to start using it and applying some of those abstract concepts. I'm going to first show you a bit about the interpreter. Then I'm going to show you the anatomy of a Python script, and finally, we'll build a simple Python program that helps us convert speed limits. I recommend you follow along as we go. 

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



## Building a Python Program

For this chapter, we're going to start with a script that just contains the instructions section without any imports. For my example, I'm going to create a calculator that will allow the user to convert between Kilometers per hour (KPH) and Miles per hour (MPH). Now this is a real problem, perhaps for someone who is accustomed to driving in the USA and is moving to Canada or Europe. How fast is 100KPH really?

The first step is to break down the problem. This is called **decomposition**. I will decompose the problem into a series of steps that the computer needs to help me solve. 

1. The program needs to know the original unit and the converted unit. So, I need to know if we're going from MPH to KPH or KPH to MPH.

2. The program needs to know the original value. Is it 60? 100? 80? 

3. The program needs to contain the calculations in both directions. I'll look those up on Google. 

4. Based on the information the program needs to know, it will have two variables: the original unit and the original value.

Now I'm going to write up what is called a user story. This is part of the Agile software development paradigm, and it is the story of a user interacting with the program.

---
*My name is John, and I occasionally drive my vehicle from the United States to Canada. When I am there, I have a hard time with the speed limit conversion. So, I open the program, and it prompts me whether I want to convert **FROM** KPH or MPH. I am in Canada, so I need to convert from KPH to MPH. The program then prompts me for the speed limit. I enter it, and it prints out the speed limit in MPH. I really don't want to worry about decimals, so I need to make sure it rounds.* 

---

Ok, now that I have a sense of what the program needs to do, I need to create a file to hold this script. First I create a project directory and a file to hold my code. I'm not going to worry about a virtual environment because I don't anticipate this is going to be a very large project. Then I need to open the directory with VS Code.  

```
~$ mkdir speed && cd speed
~/speed/$ touch speed_converter.py
~/speed/$ ls
speed_converter.py
~/speed/$ code .
```

The first command, again, creates a directory and changes into that directory. The second command creates the file called speed_converter.py. It is a python script. The name is arbitrary but logical. Next, I use the ```ls``` command to show you that the file was created. I wouldn't probably actually do this in real life, and it's not necessary to check every time you create a file. You can always do it if you want, but not required. Finally, I open VS Code with the ```code``` command. I pass that command an argument: ```.``` which means open the local directory. A VS Code window opens and I click on my python script in the file explorer pane to open it in the text editor pane. You'll see it is empty, so I'm going to start writing in a bunch of comments to help me code. 

_speed\_converter.py_

```python
#!/usr/bin/env python3

# Prompt user for original limit and save to variable.
# Prompt user for original value and save to variable.
# If the original limit is KPH use this expression.
#   output = value * 0.62137
# If the original limit is MPH use this expression.
#   output = value * 1.60934
# convert output to integer
# print output
```

Okay, so I now have all the steps that I need my program to take. I will walk through each of these and turn them into code. For the book here, I will do them all at once, but in practice, I go through step by step. If I don't know how to do something, I will search for it on Google. For instance, if I don't know how to get input from a user, I might search for "get user input in python3". 

_speed\_converter.py_
```python
#!/usr/bin/env python3

# Prompt user for original units and save to variable.
units = input("Are you converting from KPH to MPH? (Y/n)")
# Prompt user for original value and save to variable.
value = input("What is the original speed limit? ")
# If the original limit is KPH use this expression.
if units != "n" or units != "N":
    output = value * 0.62137
# If the original limit is MPH use this expression.
if units == "n" or units == "N":
    output = value * 1.60934
# convert output to integer
output = int(output)
# print output
print(output)

```

Okay, so I have workable code. I can run it now and see how it works. 

```
$python3 speed_converter.py
Are you converting from KPH to MPH? (Y/n)Y
What is the original speed limit? 100
Traceback (most recent call last):
  File "speed_converter.py", line 9, in <module>
    output = value * 0.62137
TypeError: can't multiply sequence by non-int of type 'float'
```

Ok, so I have an error. I need to look at the error. I see that I have a type error, which means that my data in the expression ```output = value * 0.62137``` is the wrong type. The issue is either with ```value``` or the floating point number. I'm guessing it is probably the value because I know that I can multiply integers with floats. I need to look at the ```input()``` function and see what kind of data is getting stored in ```value``` when I get data from the user. You can look it up if you like.

Welcome back. The problem, of course, is that ```input()``` returns a string. This means that the data type stored in ```value``` is a string. I know that strings cannot be multiplied by decimals. Instead, I need to convert whatever I'm getting from the input function from a string to a float or integer. Let's do some revision, or **refactoring** of the code. I'm also going to adjust a couple other things with my logic checks at the same time.

_speed\_converter.py_
```python
#!/usr/bin/env python3

# Prompt user for original units and save to variable.
units = input("Are you converting from KPH to MPH? (Y/n)")
# Prompt user for original value and save to variable.
value = int(input("What is the original speed limit? "))
# If the original limit is MPH use this expression.
if units == "n" or units == "N":
    output = value * 1.60934
# If the original limit is KPH use this expression.
else:
    output = value * 0.62137
# convert output to integer
output = int(output)
# print output
print(output)
```

Now we run it again and see that it works this time. 

```
$ python3 speed_converter.py
Are you converting from KPH to MPH? (Y/n)y
What is the original speed limit? 100
62
```

I'll quickly walk through the code. 

* Line one is the shebang line, but since I run the script with the python interpreter from my command, I don't need this.

* Line two prompts the user for input. I let them know that the default is "Y" for KPH to MPH. 

* Line three prompts the user for the original speed limit and immediately converts their response to an integer.

* Line four checks if the user entered either "n" or "N" into the prompt on line two. If so, we're converting from MPH to KPH. The calculation is run.

* Line 6 is "else" which is the default condition if the user didn't enter "n" or "N". In that case, we calculate from KPH to MPH. 

* Finally, regardless we convert from the floating point value in output to an integer so that we don't have to worry about a decimal, and print out the results. 

So that's your first Python script that does some decision making. In the next chapters we'll dive into decision making, but for now, you can see we have already built a pretty cool program that could be applied to any sort of conversion problem. In the next section, as we discuss conditions there will be a great deal to say regarding concerns of the Humanities and human culture. Until then, practice and enjoy! Can you maybe modify our code to convert for something else (currency? temperature? etc.) 