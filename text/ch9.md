# Decomposition

You've seen in the last couple weeks the way in which we need to divide up a particular task into steps if we want to make a computer program. This is crucial because the program can only perform one command at a time (unless we're multi-threading, but that's a topic for another class), and that one command has to be a single specific action. As a result, if we want to create computer programs that solve real-life problems, we need to be able to break those problems into a series of parts, and our solution needs to be a series of steps that the computer can perform sequentially.

This process of breaking a process down into its component steps is called Decomposition. In terms of programming, it's impossible to solve complex problems or build systems without doing this. In terms of general problem solving, decomposition can help us make complex situations and tasks more approachable. For instance, if I say, "write a 30 page essay that argues that technological capital is a better lens to understand technological inequality than the digital divide" you could just start writing, but that would be overwhelming. Instead, you'd be better to divide that problem into a bunch of individual components. For instance, you'll need a section that defines technological inequality, another set of sections that look at individual elements of that problem, another section that defines technological capital, and so on. Each of those sections is an approachable task. But I digress...

Let's think about a process that we might want to solve: I want to create a process that reads text and finds occurrences of particular words in a text. This could be useful for looking for jargon words or dog-whistles and slurs or vocabulary words in use. Look below at the way I've broken this process into some functions.

For this example, I've set myself up with the project of creating a program that reads a text, identifies if keywords are in the text, and returns a score based on frequency of those words. I might use this to score texts for the presence of racist or sexist language.

First I need to get the list of search words. This should either be passed as an argument or parameter, OR it could be entered directly from the terminal. I'll write this into my program in pseudocode, first. 

_myprogram.py_
```python
# function called get_search_words that takes a parameter, or it prompts the user in the cli.

# check and see if there's a parameter.
# if not prompt the user for a file or for direct input
# if file, open the file and read it in
# if not file, prompt user for a list of words. I better make sure there's a maximum number.
# if the user changes their mind, give them a way to quit. 
```

You'll notice that I start with a list of steps that I need to do. If I have no idea how to do any given step, I'll isolate that step and try to figure out how to do that one instruction. Let's start with the first bit. 

_myprogram.py_
```python
# fuction called search words with a parameter
def get_search_words(search_words):
   
   # check and see if there's a parameter, and if so return it.
   if search_words:
      return search words # this is the end of function in this branch
   
   # if we get to this point, the user is entering the words manually
   search_words = []
   # if not prompt the user for a file or for direct input
   # if file, open the file and read it in
   # if not file, prompt user for a list of words. I better make sure there's a maximum number.
   # if the user changes their mind, give them a way to quit.

   return search_words
```

Okay, so I have my function defined and the case where the search words are passed as a parameter. That's great news. Now I need to think about the instructions to prompt a user for how they want to enter the search words. I can do this next. Notice, if there are search words in the parameter, the parameter is returned and the function will exit. The only way the program ever gets to the line ```search_words = []``` is if ```search_words``` in the parameter is empty. So, let's get to prompting the user. 

_myprogram.py_
```python
# fuction called search words with a parameter
def get_search_words(search_words):
   
   # check and see if there's a parameter, and if so return it.
   if search_words:
      return search words # this is the end of function in this branch
   
   # if we get to this point, the user is entering the words manually
   search_words = []
   # if not prompt the user for a file or for direct input
   user_in = input("Entry method: (f)ile, (m)anual, (Q)uit")
   # if file, open the file and read it in
   if user_in.lower == "f":
      #do stuff for the file
      pass
   elif user_in.lower == "m":
      # do a manual entry instructions
      # make sure we have a maximum number.
      pass
   
   # I'm using Q as the default case. So if the user doesn't enter
   # "f", "F", "m", or "M", then the program quits.
   else:
      return None

   return search_words
```

You can see that now my program has 4 potential forks. The first tong is if there is a parameter. Then we just return that list. The second is if the user enters "f" or "F" for a file entry. We have used ```pass``` as a placeholder for now. The third is if the user enters "m" or "M" for manual entry. Again, we have a placeholder. The fourth condition is default, so if the user enters anything besides "f", "F", "m", or "M", the program will exit with a None value returned. That I create a default rather than check for "Q" is a design decision. I designed it that way so that the program exits if, say, the user enters a typo or a wrong letter. I use this default case to catch everything except the specific values I'm looking for. That is a good design strategy because now I don't have to worry about what happens if the user enters "X" or "47" or anything else. The program will just exit. Next, I'll do a big chunk, and create instructions for manual text entry. I'm going to limit the list arbitrarily to 10 search words. 

_myprogram.py_
```python
# fuction called search words with a parameter
def get_search_words(search_words):
   
   # check and see if there's a parameter, and if so return it.
   if search_words:
      return search words # this is the end of function in this branch
   # if we get to this point, the user is entering the words manually
   search_words = []
   # if not prompt the user for a file or for direct input
   user_in = input("Entry method: (f)ile, (m)anual, (Q)uit")
   # if file, open the file and read it in
   if user_in.lower == "f":
      #do stuff for the file
      pass
   elif user_in.lower == "m":
      # do a manual entry instructions
      count = 1
      more = True
      while count < 11 and more:
         word = input("Enter word # {}: (q to exit)".format(count))
         # make sure we have a maximum number.
         if word.lower() == "q":
            more = False
         else:
            search_words.append(word)
         count += 1
   
   # I'm using Q as the default case. So if the user doesn't enter
   # "f", "F", "m", or "M", then the program quits.
   else:
      return None

   return search_words
``` 
  

Okay, so that's pretty swell. Now I have a counter that limits my manual prompting to 10 words. I also have a variable ```more``` which is set to ```False``` if the user decides they want to quit. Then the word is added to the ```search_words``` list. If I needed to look at how to add to a list, I'd search for something on Google like, "Python3 add element to list." Now, I need to figure out how to open a file. I'm going to do that by searching "Python 3 open and read files." I'll find the [open() function](https://docs.python.org/3/library/functions.html?highlight=open#open) that's built in to Python that opens files. I see that it is a function that takes a file name as a parameter. By default, it will only read files, but I can change the mode to 'w' for writing. The function returns a file object, so if I store the output of the ```open()``` function to a variable, the variable will contain a handle to that file object. I'll start by playing around and seeing if I can write "Good Morning" to a file. I'll do this playing in the Python CLI before I return to my program.

```python
Python 3.8.5 (default, Jul 28 2020, 12:59:40)
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> f = open("test.txt")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
FileNotFoundError: [Errno 2] No such file or directory: 'test.txt'
>>> f = open("test.txt", 'w')
>>> f.write("Good Morning")
12
>>> f.read()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
io.UnsupportedOperation: not readable
>>> f.close()
>>> f = open("test.txt")
>>> f.read()
'Good Morning'
>>>
```

I see that I can open a new file in write mode. I can write some text to the file. Then I need to close the file and open it again before I can read from it. I do that, and when I read the file, I see that 'Good Morning' was added to the file. Next I do a little research and read about the ```with {} as {}:``` syntax. This allows me to open a file and close it with fewer lines of code. Let's test it out. 

```python
>>> with open('test.txt', 'w') as f:
...     f.write('Good Evening')
...
12
>>> with open('test.txt') as f:
...     f.read()
...
'Good Evening'
>>>
```

Cool, so now I have a bit of a sense of how to open, write, and read from files. I might go on and test how to read multiple lines of a file or how to iterate through a file line by line. I'll learn that by using ```readlines()``` instead of ```read()``` on the file, I can read each line into a list. Now I'll jump back to the code and add what I learned:

_myprogram.py_
```python
# fuction called search words with a parameter
def get_search_words(search_words):
   
   # check and see if there's a parameter, and if so return it.
   if search_words:
      return search words # this is the end of function in this branch
   # if we get to this point, the user is entering the words manually
   search_words = []
   # if not prompt the user for a file or for direct input
   user_in = input("Entry method: (f)ile, (m)anual, (Q)uit")
   # if file, open the file and read it in
   if user_in.lower == "f":
      #do stuff for the file
      file_name = input("Enter the name of the file: ")
      with open(file_name) as f:
         search_words = f.readlines()

   elif user_in.lower == "m":
      # do a manual entry instructions
      count = 1
      more = True
      while count < 11 and more:
         word = input("Enter word # {}: (q to exit)".format(count))
         # make sure we have a maximum number.
         if word.lower() == "q":
            more = False
         else:
            search_words.append(word)
         count += 1
   
   # I'm using Q as the default case. So if the user doesn't enter
   # "f", "F", "m", or "M", then the program quits.
   else:
      return None

   return search_words
``` 

This is all well and good. I'm going to read the lines of the file. This will basically work. My next step will be to write a driver that tests the function. 

_myprogram.py_
```python
# fuction called search words with a parameter
def get_search_words(search_words):
   
   # check and see if there's a parameter, and if so return it.
   if search_words:
      return search words # this is the end of function in this branch
   # if we get to this point, the user is entering the words manually
   search_words = []
   # if not prompt the user for a file or for direct input
   user_in = input("Entry method: (f)ile, (m)anual, (Q)uit")
   # if file, open the file and read it in
   if user_in.lower == "f":
      #do stuff for the file
      file_name = input("Enter the name of the file: ")
      with open(file_name) as f:
         search_words = f.readlines()

   elif user_in.lower == "m":
      # do a manual entry instructions
      count = 1
      more = True
      while count < 11 and more:
         word = input("Enter word # {}: (q to exit)".format(count))
         # make sure we have a maximum number.
         if word.lower() == "q":
            more = False
         else:
            search_words.append(word)
         count += 1
   
   # I'm using Q as the default case. So if the user doesn't enter
   # "f", "F", "m", or "M", then the program quits.
   else:
      return None

   return search_words

if __name__ == "__main__":
   words = ['apple', 'blueberry', 'mango']
   s_words = get_search_words(words)
   print("Original words: ")
   for w in words:
      print(w)
   
   print("Search Words")
   for w in s_words:
      print(w)
   
   s_words2 = get_seard_words()
   for w in s_words2:
      print(w)
``` 

I can run this and see what happens. Now to finish out my program, and I'll need to write a second function that uses the output from ```get_search_words``` that will take a block of text and list of search words, and return the total number of search words found, the total number of words, and percentage of total words the search words make up. 


_myprogram.py_
```python
# fuction called search words with a parameter
def get_search_words(search_words):
   
   # check and see if there's a parameter, and if so return it.
   if search_words:
      return search words # this is the end of function in this branch
   # if we get to this point, the user is entering the words manually
   search_words = []
   # if not prompt the user for a file or for direct input
   user_in = input("Entry method: (f)ile, (m)anual, (Q)uit")
   # if file, open the file and read it in
   if user_in.lower == "f":
      #do stuff for the file
      file_name = input("Enter the name of the file: ")
      with open(file_name) as f:
         search_words = f.readlines()

   elif user_in.lower == "m":
      # do a manual entry instructions
      count = 1
      more = True
      while count < 11 and more:
         word = input("Enter word # {}: (q to exit)".format(count))
         # make sure we have a maximum number.
         if word.lower() == "q":
            more = False
         else:
            search_words.append(word)
         count += 1
   
   # I'm using Q as the default case. So if the user doesn't enter
   # "f", "F", "m", or "M", then the program quits.
   else:
      return None

   return search_words


def text_scorer(text, search_words):
   # iterate through search_words and get the frequency of each
   # in the text. Also create a variable to store the count.
   word_counter = 0
   total_words = len(text.split(" "))
   
   for word in search_words:
      word_counter += text.count(word)
   
   output = (word_counter, total_words)


if __name__ == "__main__":
   words = ['apple', 'blueberry', 'mango']
   s_words = get_search_words(words)
   print("Original words: ")
   for w in words:
      print(w)
   
   print("Search Words")
   for w in s_words:
      print(w)
   
   s_words2 = get_seard_words()
   for w in s_words2:
      print(w)
``` 

That was pretty easy. I just use the built in ```count()``` function and keep a running total. Now I just need to modify the driver so that we can get it working as we like:

_myprogram.py_
```python
# fuction called search words with a parameter
def get_search_words(search_words):
   
   # check and see if there's a parameter, and if so return it.
   if search_words:
      return search words # this is the end of function in this branch
   # if we get to this point, the user is entering the words manually
   search_words = []
   # if not prompt the user for a file or for direct input
   user_in = input("Entry method: (f)ile, (m)anual, (Q)uit")
   # if file, open the file and read it in
   if user_in.lower == "f":
      #do stuff for the file
      file_name = input("Enter the name of the file: ")
      with open(file_name) as f:
         search_words = f.readlines()

   elif user_in.lower == "m":
      # do a manual entry instructions
      count = 1
      more = True
      while count < 11 and more:
         word = input("Enter word # {}: (q to exit)".format(count))
         # make sure we have a maximum number.
         if word.lower() == "q":
            more = False
         else:
            search_words.append(word)
         count += 1
   
   # I'm using Q as the default case. So if the user doesn't enter
   # "f", "F", "m", or "M", then the program quits.
   else:
      return None

   return search_words


def text_scorer(text, search_words):
   # iterate through search_words and get the frequency of each
   # in the text. Also create a variable to store the count.
   word_counter = 0
   total_words = len(text.split(" "))
   
   for word in search_words:
      word_counter += text.count(word)
   
   output = (word_counter, total_words)


if __name__ == "__main__":
   words = ['apple', 'blueberry', 'mango']
   search_words = get_search_words(words)
   text = "I like to eat apple, blueberry, and mango, but I don't like to eat them together. Apple is good. Blueberry is good, but blueberry and apple, not so good."
   
   scores = text_scorer(text, search_words)
   print("Search word frequency: {}".format(output[0]))
   print("Total words: {}".format(output[1]))
   print("Score: {}".format((output[0]/output[1] * 100), 2))
``` 

This is a fairly small program, but hopefully you can see the process we go through to break down the larger problem into a sequence of steps that can be solved by the computer. That is the essence of decomposition. 

## Approaches to Decomposition

### Procedural decomposition

Procedural decomposition looks at a complex tasks and sees it as a series of procedures or steps. One you're probably familiar with is cooking. Imagine you want to make a cake. If you read a cookbook like the Joy of Cooking, you'll see recipes that are a series of steps with the appropriate ingredients and actions listed with their corresponding step. So, to make, say, spaghetti carbonara,

* you'd begin by starting some water boiling

* then dice some bacon and start cooking it

* then add pasta to the boiling water

* then skim off some of the oil from the bacon pan

* then when the pasta is done, reserve some cooking water and strain the pasta

* then mix the cooking water with eggs and cheese (carefully so as to not curdle the eggs).

* then, add pasta to the bacon pan
    
* finally, pour egg and cheese mixture over pasta
    
* serve with grated parmesan

Most early programming was procedural, and many of the onboard programs for things like watches, printers, and so on remain to some extent procedural. Procedural programming is useful for systems where one task is going to be performed over and over again. It is also useful because you don't need a ton of memory to store complex objects or functions. You just have a list of commands that the machine operates.

Likewise, you might use procedural approaches in utility scripts that you write for your own purposes. Let's say you work in IT for a university department and you're tasked with helping faculty members clean up their file naming conventions. You could go through and manually rename all these files, but it would be much better to spend a bit of time writing a script and letting the computer do the work for you. That said, instead of writing a huge program with functions and objects, all you'd need is a short set of procedures that walks through the file tree and renames files ending with .docx or .pdf.

Of course, procedural programming is less effective if you have a complex program that requires a lot of different kinds of activities. In this case, you might move over to functional programming.

### Functional Programming

Last week I mentioned that programmers are lazy. In procedural programming, if I wanted to read through and open 100 files, read their content, and find the occurrences of the word "fish," I'd need to write

```python
with open("fileName") as f:
   fish_counter += f.read().count("fish")
```

100 times in my program. I'm lazy and I don't want to do all that typing. Plus, I don't like copy-and-pasting. If one of the copied items is wrong, I'd have to go through and fix 100 occurrences. Instead, I'm going to create a function to generalize that task of opening and reading a file.

```python
def count_fishes(file_list):
   fish_counter = 0

   for f in file_list:
      with open(f) as fhandle:
         fish_counter += f.read().count("fish")
   
   return fish_counter
```

Functional programming decomposes problems into a series of procedures, but then it takes those procedures and attempts to identify redundancies or general tasks. We take these redundant tasks and turn them into functions, or a set of commands that takes some input and returns some output after performing some process.

The general function for a recipe looks something like this:

![Tree diagram of function](img/recipe.png)

I see that in a recipe, I have a measure and add task that is repeated. I would probably want to create a function that can be used. In this case, I'd pass three parameters: 1. the ingredient to add, 2. how much to add, 3. when to add (this would interact with a global timer)

### Object-Oriented

Object-oriented programming goes a step further towards generalization and encapsulation. I don't want to introduce OO programming to much yet, because we're spending two weeks on it starting next week, but in short, an Object is a way to group a set of attributes or features with a set of actions.