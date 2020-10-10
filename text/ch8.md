# Introduction to functions

## Making it Generic

Programmers are inherently lazy. By this I mean, programmers write as little code as they possibly can. This is useful for a few reasons. First, the fewer lines of code you write, the less likely you are to have an error. Second, if you refactor your code, you have fewer places to make changes. Third, you get to spend less time writing code and more time working on other things.

How do we make something generic? Think about making a peanut butter and jelly sandwich. If I were to give you instructions they might include these steps (I've cut out a lot to not waste your time):

1. Use hand and turn peanut butter jar lid until the lid is loose.

2. Lift lid off jar.

3. Place the lid on the counter.

4. Use hand and turn jelly jar lid until the lid is loose.

5. Lift lid off jar.

6. Place the lid on the counter.

Notice that I have two series of steps that are basically the same, but are done on different kinds of jars. A much simpler way would be to first make sure you know what the generic sequence of steps is "Use hand to turn, lift lid, place lid on counter." We do this in our own language. Instead of telling someone all those steps, we'd say, "open the jar." The human audience would know that openning the jar involves more smaller actions, but they group those actions into openning the jar. The general activity of opening jars can be done on any sort of jar as long as it has a lid and is opened by turning. Computers give us the same thing, but we need to teach them what a group of general actions are called. What I would do is create a collection of actions called, "open ____ jar" and then my program becomes:

1. Open the jelly jar.

2. Open the peanut butter jar.

I cut the steps down from 6 to 2, and if I want to change the process, I just need to redefine what I mean by "Open." I took a series of steps and made them general enough to be applied to various types of jars.

Generalization in programming works very much like this. Let's say I want to test if a series of lists of numbers are even, and if they are add them to a list of numbers.

I could do something like this where I write out the instructions for each list:

```python
my_nums1 = [5, 2, 7, 8, 0]
my_nums2 = [10, 15, 8, 8, 4]
my_nums3 = [1, 7, 4, 5, 3, 6]
evenNums = []

for num in my_nums1:
  if num % 2 == 0:
    evenNums.append(num)

for num in my_nums2:
  if num % 2 == 0:
    evenNums.append(num)

for num in my_nums3:
  if num % 2 == 0:
    evenNums.append(num)
```

After Python executes these instructions ```evenNums``` will contain the even values from all three lists. However, it's not particularly efficient. Notice the code is exactly the same except for the name of the list that is to be iterated through. Wouldn't it be easier to write the instructions once in my code and then call the instructions on each of the lists? Totally. I'm going to build what is called a function that makes the instructions work on any list. 

```python
evenNums = []
my_nums1 = [5, 2, 7, 8, 0]
my_nums2 = [10, 15, 8, 8, 4]
my_nums3 = [1, 7, 4, 5, 3, 6]

def get_even(my_list):
   for num in my_list:
      if num % 2 == 0:
         evenNums.append(num)

# now I call the function on each of the lists. 

get_even(my_nums1)
get_even(my_nums2)
get_even(my_nums3)
```
This is cool because I took a specific set of instructions that were repeated, figured out how the action could be generalized, and finally wrote those instructions into a general function that can operate on many input values. Also, if I wanted to tweak this slightly, then I could change the 2 to a 3 or any other multiple to find the numbers that are multiples of that number. In fact, I could even generalize further expanding the functionality of my function. 

```python
evenNums = []
my_nums1 = [5, 2, 7, 8, 0]
my_nums2 = [10, 15, 8, 8, 4]
my_nums3 = [1, 7, 4, 5, 3, 6]

def get_mulitple(my_list, multiple):
   for num in my_list:
      if num % multiple == 0:
         evenNums.append(num)

# add to evenNums multiples of 5 from list 1
get_multiple(my_nums1, 5) 
# add to evenNums multiples of 2 from list 1
get_multiple(my_nums2, 2)
# add to evenNums multiples of 3 from list 1
get_multiple(my_nums3, 3)

```

Building functions is about taking instructions, identifying what variables you want to generalize out, and turning those into arguments that the function can receive from the user or another program calling this function.

### Anatomy of a function

Now that you've seen some functions in action, I want to point out the anatomy of a function. A function has three main parts: **the input**, **the output**, and **the block**. The input is anything that the function takes in from outside. This could be an argument or parameter--the things that go between the parentheses in the function definition and call. It could also be user input using the ```input()``` function, although I generally try to reserve this for a separate user interface unless the program is very small and single-purposed. Finally, the input could also come from files or other data streams that get opened in the body of the function.

The output is whatever the function returns to the scope outside the function. This could be printing or writing to some user interface or file. More commonly, the output is whatever is after the ```return``` statement. This keyword is the instruction that sends data from inside the function to outside. Think of it like a vending machine. You put money and data into the machine. The machine does some stuff internally (usually you can see that stuff through the window) and finally, it returns a candy bar to you. Once again, just like the input, I like to use the ```return``` statement for the output and create a separate user interface to print the data to the screen or otherwise share it with other processes or the user. 

Finally, the block is the set of instructions that are executed every time the function is called. Notice that there might be variables, operations, logic checks, branches, etc. within the function. Another thing to notice is that I might have a variable with the same name inside the function, inside the parameter of the function and in the instructions outside of the function. See ```search_words``` in the next chapter as an example. The variable, even if it has the same name, refers to a different space in memory. So if I have ```x``` as a variable outside of the function, and then I have ```x``` as the parameter of the function, and I have an ```x``` in the body of the function, you should think of them as three different variables that might hold different values. 

Here is the explanation again in code:

```python
# Here's a function with it's parts identified:

def my_crazy_function(x): # "def" is a keyword that means you're making a function. def is followed by the name of the function. It can either be camelCase or snake_case. Following the function name you have parentheses which contain all of the parameters for the function. 
  # The block--all the instructions that are part of the function.
  x = x ** x
  return x # This is what the function outputs to the rest of the program.

# Whenever you want to call a function, you simply include the function name with any parameters.
x = 7
output = my_crazy_function(x) #in this line, the program will do the instructions in the function.
```

The ```x``` in the parameter (```my_crazy_function(x)```) is a different variable than the ```x = 7``` variable. Finally, the line ```x = x ** x``` means "create a new variable called ```x``` that is local to the function (only exists inside the function) and save to it the value of the parameter ```x``` to the power of the parameter ```x```. I know this is confusing, perhaps, but it is worth taking some time to consider this and pay attention to it because it is very common for a program to have the same variable name used for different variables in different scopes.

### Scope

Not the mouthwash, scope refers to where different data is accessible. This is a complicated topic that leads to a lot of grief. We will spend a good deal of time discussing scope in class and in next week's module. For now, think of it as what container or block does a piece of data live in. If I have a variable "my_var" inside a function, I the program can only access that variable inside of the function. It cannot access the if I try to use it outside, or it would be a different variable.