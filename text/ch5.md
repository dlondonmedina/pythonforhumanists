# Conditionals 

## Introduction to Flow Control

Thus far, we've basically told the computer what to do and it has done it basically as we requested. However, in programming, one of our goals is to turn over more of the work to computers. We saw this a little bit with our speed conversion program. Instead of writing two different programs, one for MPH to KPH and another for KPH to MPH, we wrote one program with a decision in it that allowed the computer to decide which calculation to perform based on the user's input. This ability of a computer to make decisions based on input is a central part of **flow control**. Flow control refers to the controls that we build into our program that tell the computer when and how many times to execute a particular group of instructions. There are two separate parts of flow control: conditionals, which tell the computer to execute instructions based on a set of conditions, and iterators or loops, which tell the computer to execute instructions while a particular condition is true or for a particular number of times. In this chapter, we'll look at the first. In the next chapter we'll look at the second. 

## Conditionals: An example

To set the stage, let's say my user wants to figure out if one number is a factor of another number. A number is a factor if the second number can be divided evenly by the first. So, 4 is a factor of 12 because 12 can be evenly divided by 4. Programming languages give us the % (mod) operator to help us out with that. So let me write the program. It will prompt the user for two numbers. It will print "x is a factor of y" if the second number is a factor, and "Is not a factor" if not. 

```python
mult = int(input("What is the multiple? "))
fact = int(input("What is the factor to check? ")) 

if mult % fact == 0:
   print("{} is a factor of {}".format(fact, mult))
else:
   print("{} is NOT a factor of {}".format(fact, mult))
```

When we run this program from our bash terminal we get something like this: 

```
~$ python factor.py
What is the multiple? 12
What is the factor to check? 4
4 is a factor of 12
~$
```

Then we can run it again with something we know should be false:

```
~$ python factor.py
What is the multiple? 12
What is the factor to check? 5
5 is NOT a factor of 12
~$
```

What's going on here? On our first two lines, we're prompting the user for input and storing those values to two separate variables. Then we use an "if" statement to check to see if the remainder of ```multi / fact``` is zero. If this is true, then we execute the code on the next line (line 5). Otherwise, we skip down to the "else" statement and execute that instruction. We can see, then, the first time we run the code, 12 / 4 has a remainder of 0, so the condition in the "if" statement is True. So you see the appropriate instruction is executed. On the other hand, in the second run of our code, 12 / 5 does have a remainder that is not equal to zero (it is equal to 2 specifically). As a result, the statement evaluates to False and we do not execute the code within the "if" block. Instead, we go down to the "else" and execute that code instead. Notice the instructions on the lines after ```if``` and ```else``` are indented one level. This signifies to the Python interpreter that they are part of the ```if``` or ```else``` block. A code block is a collection of code that only gets executed if some condition is met. In this case, the ```if``` block only gets executed when the condition we defined for if is True. Otherwise, the ```else``` block is executed. Regardless of the input (as long as it is valid input), either the ```if``` block will execute or the ```else``` block, but never both. 

We can also set up conditions with only an ```if``` block. Let's say we want a program to print "Happy Birthday" on a user's Birthday and not print anything else if it is not. That code would look like this:

```python
BIRTHDAY = "05/02"
today = input("What is the date today (mm/dd)? ")

if BIRTHDAY == today:
   print("Happy Birthday!")
```

Once again, I'll show you what it looks like when we run this code:

```
~$ python birthday.py
What is the date today (mm/dd)? 05/02
Happy Birthday!
~$ python birthday.py
What is the date today (mm/dd)? 03/12
~$
```

I set ```BIRTHDAY``` as a constant value. Then the program prompts the user for the date with a hint at the format. I check to see if what the user entered matches or is equal to the value stored in ```BIRTHDAY```. If it is, then the program prints "Happy Birthday!" and if it is not, then it does nothing. Once again, I show you what that looks like when we run the program in both cases. Sometimes it is useful to have code that only runs when a condition is satisfied. We can also use negative conditions, so if we wanted to congratulate the user that it's not their birthday, we'd need to change our condition to be ```if BIRTHDAY != today:```. 

Finally, we can set a series of conditions. Perhaps we want to help someone who is trying to decide whether to wear a jacket or not based on the temperature: 

```python
temp = int(input("What is the temperature? "))

if temp > 70:
   print("Wear Shorts")
elif temp > 50:
   print("Pants and a wind breaker")
elif temp > 40:
   print("Maybe a jacket?")
else:
   print("Bundle up, it's cold!")
```

In the above example, we have 4 conditions: warmer than 70 degrees, warmer than 50 degrees, warmer than 40 degrees, or colder than 40 degrees. This leads us to a cool design decision. In the ```if/elif/else``` or ```if/else``` structure only one of the blocks will be executed. Specifically, the first time the condition is True, the corresponding block is executed and the rest are skipped. So, in the above example, if the user inputs 75, only the first block will execute. It is true that 75 is also greater than 50 and 40, but Python stops at the first True condition and once we have a True condition none of the other blocks are executed. 

As a design decision, this allows us to check for warmer than 70, 50, and 40 without having to say ```elif temp > 50 and temp <= 70:``` for the second condition. **We know that if the Python interpreter is even evaluating that condition, then the first condition failed and the temperature is 70 or less.** The ```else``` acts as a fall through condition. If none of the specific cases is True, then the else block is executed. As you design your conditionals, you will find clever ways to short circuit the way you test truthiness that can make your code more efficient. 

Related to this, we can also test multiple conditions at the same time. For example, let's take our code from the last example and add a prompt for the rain. 

```python
temp = int(input("What is the temperature? "))
rain = input("Are you expecting it to precipitate?(y/n) ")

if temp > 70 and rain == "n":
   print("Wear Shorts")
elif temp > 50 and rain == "n":
   print("Pants and a wind breaker")
elif temp > 40 or rain == "y":
   print("Maybe a jacket?")
else:
   print("Bundle up, it's cold!")
```

You can see that we are testing two conditions each time. In the first two cases we use the key word ```and``` which means that the whole test or condition is True if--and only if--both conditions are true. In the third case, we use the key word ```or``` which means that at least one of the conditions must evaluate to True. So if it is warmer than 40 or it's raining or both, the code block is executed. There are other logical operators that can be used but mainly if we are testing truthiness for bits. I'll have a section at the end of this chapter discussing bitwise operations, but you can skip it if you're not interested.

Finally, we can "nest" our conditions within conditions. Sometimes this is more efficient than having a bunch of conditions with multiple logic tests. For example, I might like to refactor my code again so there are fewer logic tests:

```python
temp = int(input("What is the temperature? "))
rain = input("Are you expecting it to precipitate?(y/n) ")

if rain == "y":
   print("Maybe a raincoat")
else:
   if temp > 70:
      print("Wear Shorts")
   elif temp > 50:
      print("Pants and a wind breaker")
   elif temp > 40:
      print("Maybe a jacket?")
   else:
      print("Bundle up, it's cold!")
```

You hopefully notice that there are several different ways to do things. Generally the way that is the most clear is the best in Python. In this case, we know that regardless, if it is raining, the program should tell the user to wear a raincoat, so there's no point in wasting the processing power checking the rest of the conditions. We simply short circuit the ```if/else``` structure if it happens to be raining. Now that you have a sense of these structures, I'm going to talk a bit about Booleans.

### Booleans

Booleans are a primitive data type that is either True or False. Whenever we use a conditional, the condition returns a True or a False value. So ```9 == 10``` in Python asks the interpreter to assess whether nine equals ten. Obviously, this is not true so Python will return False. This is a particular type of data and False is not the same as the string "False". This data type is important to understand because it is the fundamental operation of the computer. At the level of the hardware, all of the operations of the computer are computed through boolean logic comparing binary bits. We can manipulate bits directly with Python using bitwise operators, and frequently the operation is much faster, but for our purposes here, we're not going to worry too much about that. 

Instead, we're going to focus on True and False and expressions that evaluate to True and False. True and False are the primitive data type for booleans, but other things can be evaluated by True and False through Truthiness tests. Here is a table of some examples:

| Expression | Boolean |
|---|---|
| ```True``` | True |
| ```False``` | False |
| ``` 1 == 1``` | True |
| ``` 1 == 2``` | False |
| ```1 != 2``` | True |
| ```""``` | False (empty strings are false) |
| ```"a"``` | True |
|```0``` | False |
| ```1``` | True |
| ```8 > 6``` | True |

And so on. As you design your programs and work with control, you will write code that evaluates conditions. These conditions will evaluate to True or False, and the code will execute the block that corresponds to the passing test. The key take away besides the syntax is to recognize that you'll want to spend some time thinking about what conditions you want to evaluate and then what should happen when those conditions evaluate to a certain boolean value. 

