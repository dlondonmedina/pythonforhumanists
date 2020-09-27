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

What's happening here is I'm getting a number from the user. Then I'm setting the first factor to test. Then we enter a while loop that will continue going until factor is 1. Then we try and see if factor is a factor of number. If so, we print "Not prime" and exit the while loop with the ```break``` keyword. 

## Loops: For Loop
