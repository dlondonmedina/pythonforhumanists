# Encoding Identity

In this chapter we're going to really begin diving into Python. We'll start with a bit of review of the basic syntax using the Python CLI. Then we will move into writing scripts. As we go, I will try to highlight considerations that humanists might have as we start learning the coding. One of the more interesting things, I believe, about programming is that most programming occurs because someone has a problem. For example, I have a problem that I have to transcribe a bunch of video lectures so that they have subtitles. It is a critical task, but it is also a pain. One solution to the problem is the painful task of manually transcribing the audio with my headphones and a transcription pedal. I type fast, but it is still not fun. Alternatively, I could write some code to pipe my audio files into a speech recognition engine (which itself is code) that will return the text of the speech. I could even maybe write code to put in timestamps automatically. The question that we have to answer, then, is at what point is it worth the effort to write the code to avoid the pain of transcription? How accurate must that automatic transcription system be to be worth implementing? 

Now, to get to the place where we can solve problems, we need to know a bit about the programming language's syntax and how to run it. That is the work of this program. We also need to be able to consider how our code can translate the real problems that humans encounter into the computations that computers can do. That is, we must figure out how to render the world into code so that the computer can help us. In this chapter, we're focusing on the basic computations that a computer can do along with the kind of data it can store. This is the first step of encoding the world. After that we'll move into more complex stuff. 

## What is Programming?

Literally, programming is the process of writing a list of commands that a computer can execute in a programming language. The programmer uses some language that the computer can either interpret or understand directly. The list of instructions is the program. Pretty simple. Most programming languages have a set of known instructions built in. For example, when we write ```print("Hello, World")``` we are telling Python to use the instructions that cause the computer to write text to the terminal to write the string "Hello, World" to our terminal. Likewise, Python, and most programming languages, knows that ```8 * 8``` means that it should evaluate the integer **8** multiplied by the integer **8** and the result should be printed to the terminal. 

As programmers, we are given both these built in instructions and we get the opportunity to build our own sets of instructions by combining the built in ones. We can also overwrite the instructions that are part of the programming language, but for our purposes, we will not be doing that. The built in instructions are a combination of human readable words and math symbols. These words and symbols do specific things. Here is a list of the words that are part of the Python language as "reserved words" or words that are part of the language that you cannot use when naming new variables:

|  |  |  |  |  |
|---|---|---|---|---|
| and | del | global | not | with |
| as | elif | if | or | yield |
| assert | else | import | pass | break |
| except | in | raise | class | finally | 
| is | return | continue | for | lambda |
| try | def | from | nonlocal | while |

Python also has many built in "functions" or sets of instructions that accomplish a particular task. ```print()``` was an example that I used above. Likewise, the ```format()``` function allows us to format and add variables to a string. We'll talk about those in a bit, and I will not list all of the built in functions that are part of Python here as that would be too much. Instead it is better to know that built in functions exists, and when you're trying to do something new it's worth checking to see if there's already a built in function for that. 

Python also uses a bunch of "math" characters. These characters are called **operators** and they have special functionality in the language. Here are the major operators:

| | |
|---|---|
| +, -, *, / | Addition, subtraction, multiplication, and division operators. x + y returns the sum of x and y. |
| x**y | Exponent operator. The interpreter returns x raised to the yth power |
| x % y | The modulo operator returns the remainder of x divided by y |
| x == y | Equality operator. The interpreter returns True if x and y are equal |
| x != y | Not equal. Returns True if x is not equal to y |
| >, <, >=, <= | Greater than, less than, greater than or equal to, less than or equal to. The same as math.| 
| x = y | Assignment operator. **NOTE:** This isn't the same as math. It doesn't evaluate equality, but assigns the value of y to the variable x |

The first three sets of operators are used to perform calculations. The next 3 sets of operators ask the interpreter to evaluate equality and return True or False based on the evaluation. So ```2 == 2``` would return True, and ```2 > 20``` would return False. We use these to evaluate conditions and select which set of instructions to follow. The last operator ```=``` is important to pay attention to. In mathmatics, when we say 2 = 2, we are saying that "it is true that 2 is the same value as 2." A statement like "2 + 2 = 7" would not be true or valid in Math. In Python, the equals sign is an **assignment operator** and it means assign the value on the right to the entity on the left. So for example ```x = 2``` is assigning the value 2 to the variable x. When assignment happens, we evaluate the expression on the right of the equals sign **before** we assign the value to the variable. So, ```x = input("what is your name?")``` would first ask the user for input. Then once it receives input, that input would be assigned to the variable x. 

I would advice against trying to memorize all of these, but instead refer back to this document or the official Python documentation if you run into syntax errors. 

### Variables

Variables are a crucial concept in programming worth taking some time to think about. Anytime we have the computer do a calculation or some action, the data that is produced by that action needs to get stored somewhere. If you recall, our computer has two sites for storage: RAM (or system memory) and Long Term Storage (SSDs HDDS, etc). If I entered the following instruction into the python interpeter:

```python
>>> 2 * 2
4
>>> input("What is your name? ")
What is your name? Dylan
'Dylan'
>>>
```

I ask it to multiply 2 and 2. The computer complies and prints the value to the screen. Then I ask the computer to prompt me for a name. It does so and I respond with the string 'Dylan.' The interpreter then prints that value to the screen. Each time the interpeter responds, and gives me a new empty prompt, it has forgotten what data has been generated UNLESS I explicitly ask the interpreter to save the value to memory. We do this with variables. 

A variable is a named location in system memory (RAM). As long as our program is running and the variable is in scope (we'll explain scope later), the computer will remember the data stored in the memory location identified by that name (unless we overwrite it). A quick example: let me capture the result of 2 times two.

```python
>>> y = 2 * 2
>>> y
4
>>>
```

A variable can store a lot of different types of data. In a moment we'll look at data types. Python allows you to change the kind of data that is stored in a variable, but don't get in the habit of doing so. In other programming languages--specifically compiled languages--you have to define the data type in advance and then it cannot change. The key thing to remember is that in the context of a script, a variable stores data from line to line. Things get a little more complicated when we build functions, but don't worry about that yet. Likewise, when we use the Python CLI, variables stick around until you close that session. 

What happens once you close a session? Great question: once a script is finished running our you exit the session, the variables are tagged for deletion and you won't be able to access that data anymore. Likewise, if your computer loses power, the RAM is wiped and you lose anything that was only stored in that volatile memory. So, if you want some data to be retained after a sequence of instructions, you MUST write the data to some form of long term storage: either a file or a database or something else. We still have a ways to go before we get there. 

You'll see variables in the next chapter, and you by no means need to master them yet. You should start thinking of them as containers for data that can store various values, hence they are variable. For example, 2 is always 2 is always 2. Likewise the string ```"Dylan"``` is always a series of characters, specifically "D" "y" "l" "a" "n". They also have a static representation in binary, which is what the computer works with. The integer 2 is equivalent to 00000010 in binary. Likewise, "Dylan" is equal to "01000100 01111001 01101100 01100001 01101110" in binary when we use the ASCII/UTF-8 encoding (or the system for converting characters into binary). 

However, the variable ```x``` is just a name that you tell Python to remember that points to a particular address in memory that might hold 2 or "Dylan" or something else. Variables can be named whatever you like as long as you're not using reserved words, they don't start with anything but letters (upper or lower case), and they don't contain spaces. Generally, the name should have something to do with what kind of data it will store. For example, if I have a variable that will hold a number value, I'll probably call it ```num``` or if I have a variable holding a first name, I'd call it ```first_name``` or ```fname```. These are arbitrary choices. One of the stylistic rules of Python is that your code should be easy to read, and a major part of that is using logical and descriptive variable names. You can always identify a variable with a comment instead, but it's much better to identify the variable with it's own name and then you don't need a comment. 

### Data Types

Python has primitive datatypes and complex. Complex data types are combinations of primitive data types. In this section, I will only discuss primitive data types. 

* **Integer:** An integer is a whole number. It can be positive or negative. When we do math with integers, like division, for instance, and the result contains a decimal, the numbers after the decimal are dropped.

* **Float:** A number with a decimal place. It offers greater precision. 8 as an integer could be anything from 8 to 8.99... whereas 8. is exactly 8. 

* **String:** This is a sequence of characters. It can contain spaces, and it is always surrounded by single or double quotes (they must match). 

* **Boolean:** This is the True or False value. We use this regularly when we help teach a computer to make semi-autonomous decisions. 

Combinging these into groups and we can get complex data types. For now, however, it is simply worth knowing that they exist. **Important Note** You should know exactly what type of data a variable will contain. Python allows you to create a variable that could hold several different types of data. Other languages like C++ or Java do not. This has to do with how the compiler reserves memory for the variables. While you could allow a variable to contain at times a string and at other times and integer, it is bad practice. 

### Errors

**You will get errors.** Whenever you program, there will be times that you make mistakes. I'm not going to go into the kinds of mistakes right now in detail, but very frequently, the Python interpreter is smart enough to identify the mistake and throw and error message at you. These error messages were written by people and they're usually pretty terse. Let's look at a couple examples:

```python
$ python
Python 3.8.2 (default, Jul 16 2020, 14:00:26)
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> python --version
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'python' is not defined
>>> 2 .* 2
  File "<stdin>", line 1
    2 .* 2
       ^
SyntaxError: invalid syntax
>>>
```

The first error gives us a "Traceback" message followed by a "NameError". I read errors from bottom to top. The bottom is the error message. From there, the message can be read from bottom to top. If an error gets thrown as a result of a series of instructions, the traceback from the moment of error to initial call will be long. Our first instinct, perhaps, when seeing error messages is to throw our hands up and say, "OH! It's broken! I got it wrong." That's a totally normal instinct but it is not super helpful, and it will leave you feeling stressed out and unhappy. Instead, think of an error message as an invitation to learn. You're trying to do a thing, but Python, as much as it wants to understand you, can't understand you. You get to learn how to make yourself understood by the Python interpreter. I even sometimes read the error messages in a silly voice to make the Python interpreter seem more friendly. 

Let's look at the first error message. It says, "NameError: name 'python' is not defined." This is telling me that there is a problem with the word that I used. I used a word that the Python interpreter doesn't know. Specifically, the Python interpreter doesn't know the word "python" (ironic, I know). Now, I would be left to think, what is this "Python" name that I'm calling in the previous command? My command was ```python --version``` meaning I want to call the Python interpreter to give me the version number. Well, I can't call the Python interpreter from within the Python interpreter because it's already running. This means I need to make this call from a different environment. I then realize that I call the Python interpreter from Bash and I realize, oh, ```python --version``` is a Bash command, **not** a Python command. I fix this by exiting the Python interpeter and trying again. 

```python
(env) ~/Books/Python1$ python
Python 3.8.2 (default, Jul 16 2020, 14:00:26)
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> python --version
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'python' is not defined
>>> exit()
(env) ~/Books/Python1$ python --version
Python 3.8.2
(env) ~/Books/Python1$
```

The next error says, "SyntaxError: invalid syntax" which means that I wrote the code incorrectly. That's what a syntax error means. Python is great because look, it gives us exactly where the error is:

```python
2 .* 2
   ^
```

I accidentally added a period. Probably just a typo. I can fix this and be on my way. 

```python
>>> 2 * 2
4
>>>
```

I'm going over errors early because you'll encounter them a lot and how you respond will determine how much you struggle and suffer in learning Python. If you panic at error messages, the learning process will be less pleasant. If you take error messages as an opportunity to learn how to communicate with Python better, then it will be a more fun, but still challenging process. 

Now, you will definitely get error messages that you have no idea what they mean. I usually will then copy the error message and paste it into the Google search engine and see what other people did to solve this problem. Googling for answers is how programs **really** get written (even by the professionals), but learning how to search and read results on Google takes some time and practice. So practice now and be prepared for that. "Tech wiz" types frequently are not any more intelligent than anywone else. They usually just have a bit of experience and more importantly are really good at Googling. 

## Humanities Check-in

We've just gone through a good number of basic concepts in Python. We've looked at reserved words, operators, variables, primitive data types and errors. We also discussed how programming exists to solve problems or to train computers to help us solve problems. I want to focus for a while on how this relates to human culture. I want to start at data types. Every computer system has a set of data types it is able to work with. It must because the computer can only process calculations in binary, so the data we can store must be able to be represented in binary. If you remember the UTF-8 encoding of my first name (01000100 01111001 01101100 01100001 01101110) you'll see a series of 8 bit groupings, each grouping is a sequence of 1s and 0s that represent a letter. So "D" is encoded into binary as 01000100 using UTF-8 encoding. There are other codes that we might use, but UTF-8 is the common one. In turn, "Dylan" is an alphabetic encoding of a particular sequence of sounds that we've decided represent the human sitting here typing these words right now. So you can see, perhaps, that once we start using computers to help us with our lives, we have to be able to encode elements of our lives into the binary that computers store and run operations on.

This is all fine, but there are a few things to consider. When I say "Dylan Medina" I am using a name that represents a complex organism. Is everything I am represented by that sequence of sounds or letters on a page? Probably not. Consider being a student: one of the major complaints students have at large Universities is that they are frequently treated as a number (a student id number). This complaint stems from the fact that the students feel like they are unique and complicated individuals who have cares and interests, but the administrative system is designed to identify them as a number for registration and finance purposes, etc. The same is true in many complex human systems where we have to deal with a lot of people, and we use ID numbers for the sake of convenience. Computers take this a step further insofar as they can only deal with binary representations of stuff. So, when a student goes to an advisor in the University, the advisor can simply treat them as a number, but they can also choose to listen to the student, empathize with them, understand the possible extenuating circumstances and make moral and ethical situations based on the whole student. That would be a good advisor. A computer cannot do this unless they are explicitly programed to be able to process the data representation of the extenuating circumstances and emotions of the student and then have preprogrammed responses to that "whole student." 

We'll discuss this further when we get to flow control, but for now, what is important is how the world surrounding any given problem we are trying to solve with a computer gets encoded into something the computer can process. This means that we must be able to render the features of the world that we care about into either primitive data types or collections of primitive data types. Some things are quite easy to encode: things that are already numeric and have regular patterns. Other things are quite difficult to encode: the illocutionary force of a particular utterance--or the implied meaning of something someone says. 

Likewise, when we design a system, we make decisions on what kind of data we want to store. Strings, for example, require a considerable amount of memory, as do floats. Integers require less memory. Booleans are perhaps the most memory efficient because they can be stored in one bit (0 or 1). I want to consider an example that I think is interesting. Platforms that allow users to create profiles (e.g. social media) often have a field for gender. Early in social media days, they provided two options: male and female. This is because the people designing the system probably were not versed in or concerned about the notion of gender as a spectrum or non-binary or gender non-conforming individuals. Having a binary is convenient for developers because if I were designing a system that had to store data for billions of people, I would want to be as memory efficient as possible, and if we consider gender as a binary, the logical thing to do would be to store gender not as a string (male or female) but as a bit of binary (0 for male and 1 for female, for instance). Such a storage system then would only allow for a 0 or 1 and not any other option. Of course, people reasonably got upset by these kinds of systems and public outcry has forced change in interfaces and platforms to account for a more representative set of options, **but** that change required a redesign of both the frontend user interface (the website) AND the database structure. That is a considerable revision. This is not so say it isn't worth doing, but the most important point is that computers have limitations in how data can be represented and developers make choices based on the various strengths and limitations of their systems on which way to represent a particular kind of data. **<soapbox\>** Our job as Digital Humanists is to be at the table when systems are being designed because we have some sense of how computers can encode human life and the world **and** because we are trained in humanities and social theories. One of the major roles of digital humanitists, I believe is to participate in design and development discussions to help make sure the technology that we build is just and equitable and humane.**</soapbox\>**
