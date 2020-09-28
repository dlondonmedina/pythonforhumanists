# Flow Control: Loops

In the last chapter we looked at how we can create forks in the flow of our code that allow some instructions to be executed only if certain conditions are met. This means that we turned some of the decision making over to the computer and to our program. More complex programs can make more complex decisions, but those decisions are based on some condition or some data conforming to some condition. For example, a sentiment analysis program that detects the sentiment of a text (is it happy, angry, neutral, etc), looks at the input text and compares features of it to a model of what various texts look like. It predicts the sentiment of the text based on how much it fits the pattern. More complicated, certainly, than ```if user_input == "Yes"```, but the similar decision making principle. 

In this section, we are looking at how to have our program perform an action many times. Loops are incredibly useful in making our program more efficient. For example, if I had a list of student profiles and wanted to increment the age by one for each student, I'd need to either write an instruction for each profile, or I'd need to write the instruction once and set it to loop through all of the profiles automatically. 

There are two types of loops: indeterminate and determinate. Indeterminate loops are loops that repeat for an indeterminate number of iterations. Perhaps we have a guessing game that we want to continue playing until the user gets the answer right or exits the game. We don't know how many guesses the user will make, so we have the loop continue an indeterminate number of times until one of the end game conditions is met. Determinate loops iterate a known number of times. The example above with student profiles would be a determinate loop because there is a known set of iterations (one for each student). Indeterminate loops are controlled by the ```while``` keyword. Determinate loops are controlled by the ```for``` keyword. 

## Loops: While loop

"While" loops are loops that execute a block of code ntil a particular condition is met. A good problem that might use a while loop is finding if a number is prime using one of the brute force methods. A prime number is a number that is only divisible by 1 and itself. So 7 is prime. One way to test if a number is prime is to divide that number by all the whole numbers beneath it, and if one of those divisions does not yield a remainder, the number is not prime. Here's our code to do this:

```python
num = int(input("Enter a whole number: "))
factor = num - 1

while factor > 1:
   if num % factor == 0:
      print("Not prime")
      break
   factor -= 1
```

What's happening here is I'm getting a number from the user. Then I'm setting the first factor to test. Then we enter a while loop that will continue going until factor is 1. Then we try and see if factor is a factor of number. If so, we print "Not prime" and exit the while loop with the ```break``` keyword. Otherwise, if the value stored in ```factor``` is not a factor of ```num``` we decrease it by 1 and return to the condition. I'm going to write out the steps that occur when we run this script with the number six and the number 5. The lines in quotation marks are printed to the screen. The other lines are processes that the Python Interpreter performs.

```
Python Interpreter (PI): "Enter a whole number"
Me: "6"
PI: store 6 in the variable num.
PI: store 6 - 1 in the variable factor
PI: Is factor greater than 1? 5 > 1 is True
PI: Enter while block.
PI: Is the remainder of 6 / 5 equal to 0? False
PI: Skip if block
PI: Decrement factor by 1
PI: Return to top of while loop.
PI: Is factor greater than 1? 4 > 1 is True
PI: Enter while block.
PI: Is the remainder of 6 / 4 equal to 0? False
PI: Skip if block
PI: Decrement factor by 1
PI: Return to top of while loop.
PI: Is factor greater than 1? 3 > 1 is True
PI: Enter while block.
PI: Is the remainder of 6 / 3 equal to 0? True
PI: Enter if block
PI: "Not Prime" 
PI: Exit while loop at "break", end of program.
```

You'll notice that the ```while``` condition was tested exactly 3 times when factor what 5, 4, and 3. Once factor became 3, the ```if``` condition passed and the ```while``` loop was exited with ```break```. Let's try again, when the ```while``` condition fails and the loop is exited that way.

```
Python Interpreter (PI): "Enter a whole number"
Me: "5"
PI: store 5 in the variable num.
PI: store 5 - 1 in the variable factor
PI: Is factor greater than 1? 4 > 1 is True
PI: Enter while block.
PI: Is the remainder of 5 / 4 equal to 0? False
PI: Skip if block
PI: Decrement factor by 1
PI: Return to top of while loop.
PI: Is factor greater than 1? 3 > 1 is True
PI: Enter while block.
PI: Is the remainder of 5 / 3 equal to 0? False
PI: Skip if block
PI: Decrement factor by 1
PI: Return to top of while loop.
PI: Is factor greater than 1? 2 > 1 is True
PI: Enter while block.
PI: Is the remainder of 5 / 2 equal to 0? False
PI: Skip if block
PI: Decrement factor by 1
PI: Return to top of while loop.
PI: Is factor greater than 1? 1 > 1 is False
PI: Skip while loop. End of file, end of program.
```

The ```while``` condition was tested 4 times and failed on the last time because the ```factor``` was decreased to 1. The ```if``` condition was also tested 4 times and failed each time so the ```print()``` and the ```break``` were never executed. 

This, of course, is not the best way to find primacy of numbers, but it does illustrate that the ```while``` loop execution count is indeterminate. The action of the user or some external condition that the programmer does not have control of defines how many times the ```while``` loop runs. In fact, this leads us to an important consideration: what happens if the ```while``` condition never evaluates to ```False```? The loop will continue forever until the computer runs out of resources and freezes or the power is cut. Have you ever landed on a website that made your web browser freeze? Sometimes this is because there is a bug like this in the web page. Modern web browsers have become more sensitive to scripts that cause the page to slow down, but it used to happen sometimes. When you write a loop that has a condition that may never be satisfied, it is called an **infinite loop** and that is something to avoid. As a result, it is good to determine what has to occur to get the loop to end, and frequently it is a good idea to add a fail safe. So maybe the loop should run indefinitely, but less than one million times. I'd add a counter that will stop the loop automatically after one million revolutions if it hasn't stopped by then. 

```python
x = 27
count = 0
while x == 27 and count < 1000000:
   print("I could be an invinite loop")
   count += 1
```

In the loop above, since I'm not doing anything to change the value of ```x``` and it is set to 27 by default, the loop would never end. Fortunately, I've also added a counter variable that increases each time the loop runs. Eventually count will get to one million, at which point the loop will exit. This is a silly example, because the loop doesn't do anything, but sometimes you might create a loop like this: 

```python
while True:
   print("I am infinite")
```

We can add a counter to make sure that the ```while``` loop ends eventually like this:

```python
i = 0
while True and i < 1000000:
   print("I'm less than infinite")
   i += 1
```

The failsafe is not required, and sometimes it doesn't make sense, but as you solve problems with code, you should be trying to think of all the potential cases that could occur. Avoiding infinite loops is part of this concern.

## Loops: For Loop

The other type of loop is a **definite** loop. A definite loop is one that repeats a known number of times. For example, perhaps you have a list of values that you want to print. This list has a specific length, and so the loop will only continue for the length of the list. We will talk about definite loops more when we start looking at more complex data types, but for now you just need to know that a definite loop has a predetermined end. These loops use the ```for``` keyword in Python. I don't feel like the syntax is particularly clear; however, so I want to show you how these loops work in another language first that is a bit more obvious. This example is Java:

```Java
for (int i = 0; i < 10; i++) {
   println(i);
}
```

The condition says create a variable called ```i``` and set it equal to zero, repeate the loop until ```i``` is ten and then stop, increment or increase ```i``` by one each time.

The same loop in Python would look like this:

```python
for i in range(10):
   print(i)
```

Both the Java and the Python ```for``` loops will execute 10 times because i is 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, and then when i is 10, the the ```for``` block of code is skipped. For Java, we create an integer variable that holds a whole number that is increased with each iteration. Python creates a range object, which is a list of numbers from 0 to (but not including) the number that we pass to ```range()``` inside the parentheses. Then the ```for``` loop walks through each number in the list, assigns that number to i, and performs the instructions inside the ```for``` block. In this case, it will print the value stored in ```i``` to the screen. 

I'll give you a more extended example that tells Python to print the song [99 Bottles of Beer](https://en.wikipedia.org/wiki/99_Bottles_of_Beer).

```python
for i in range(99, 0, -1):
   print("{} bottles of beer on the wall".format(i))
   print("{} bottles of beer".format(i))
   print("take one down, pass it around")
   print("{} bottles of beer on the wall\n\n".format(i - 1))

print("No more bottles of beer on the wall")
print("No more bottles of beer")
print("There's nothing else to fall")
print("Because there's no more bottles of beer on the wall.")
```

Forgive the extra print statements. We could probably be a bit more efficient in our code, but let's look at the ```for``` condition. We have a range that starts with 99, ends with but does not include 0, and decreases by 1 each time. So the list would look like [99, 98, 97, ..., 2, 1]. For each value in that list, the ```for``` block is executed. Once the iterations of the ```for``` loop reach the end of the list, the loop is stopped, and we move on to the final sequence of 4 print statements.

As we move on to more complex data structures next chapter, you'll see that these flow control structures become extremely useful.