# Data Types

Any given program has two major components, whether that program is a web application, a simple website, a complex machine learning program, etc.

The program will have data, and it will have procedures. Data is the "stuff" of the program. It might be text, numbers, file locations, and so on. These are the "values" that are stored in memory that you have access to throughout the program (depending on their scope). 

![Data yawning](https://media.giphy.com/media/q8tdrdtO2FRsc/giphy.gif)

Every time you declare a variable, you're creating space in memory (RAM) to store some sort of data. When you run out of storage space (RAM), your program will freeze. So, if you're running a machine learning program on a small Digital Ocean droplet that gives you 500MB of RAM, and your program calls into memory a model that is 700MB, the program will freeze because there isn't enough space in memory.

Procedures on the other hand are the actions that are done by the program. If you want to compare programming to language, you might think of data as the nouns and actions as the verbs. Procedures can either be written out in a procedural style, bundled into functions, encapsulated into objects (next week), or a combination of the three. So far, we've looked at some data types, but have focused more on the procedures.

Now we can pause and look at some of the data types that Python provides you with. Data types are ways to hold information based on what that information is. These are either Primitive or Abstract.

## Primitive Data Types

You've encountered all of the primitive data types in Python. Primitive data types are whole pieces of data rather than collections of smaller pieces. So a number might be a single piece of data, and therefore it is a primitive data type.

* Integers--Whole numbers with no decimal points.

* Floats -- Non-whole numbers or numbers with decimal points (17.5, 17.0, etc.)

* Boolean -- This data type represents True or False and is what is returned when conditions from conditionals are evaluated
    
* Strings (sort of) -- Strings are weird in Python. They are kind of primitive in the sense that we can treat them as whole units, but in reality they are lists of characters. 

## Abstract Data Types:

Abstract Data types are generally larger storage structures that contain collections of smaller data types. These include **lists**, **tuples**, **sets**, and **dictionaries**. The reason we have abstract data types is because sometimes we have more than one datum that should be aggregated together in a logical way. For example, if you are looking at, say, a whole bunch of temperature readings for the month of March, you could save each one in it's own variable: that would look like this:

```python
m1 = 56
m2 = 57
m3 = 62
...
m30 = 68
m31 = 65
```

But that looks really inefficient and accessing all of those temperatures requires you to explicitly reference each individual variable. Wouldn't it be nice if we could put all of those temperatures in a list to hold all of the March temperatures? What if we could then get the temperature for a particular day by referencing the day number in the list? Well, we can. The data structure--a list--allows us to do exactly that. 

```python
march_temps = [56, 57, 62, ... , 68, 65]
```

To get the temperature from March 5th, you'd just need to access ```march_temps[4]```, which will give us the 5th element in the list. Abstract data types allow us to store data in larger structures in meaningful ways. 

### Lists--ordered, heterogenous, sequences of data

We've touched on lists briefly with strings. Unlike primitive data types that hold one piece of data (a number or a string or a boolean or an integer), lists hold a series of data. By heterogenous, I mean that each piece of data need not be the same, so you could have a list that contains integers, strings, lists, and so on. Though, I think this is not a great practice. For instance, what if I have a bunch of student names that I want to store. It doesn't make much sense to store them all in individual variables or else I'd have a bunch of variables to manage. Instead, I can use a list that will help me manage these names in one single variable.

```python
students = ['Joseph', 'Omar', 'Sue', 'Wendy', 'Natasha']
```

A list gives me a useful way to organize all those pieces of data. There are a few keys to remember about lists.

1. Lists are ordered by index. This means that each value corresponds to a particular position in the list. The first item in a list is index 0. The last is the n-1 where n is the length of the list. They never get out of order unless you explicitly change them.
   
2. Lists can contain different types of data at each index.
    
3. Lists can be sliced (you can grab a chunk of the list by index number), iterated over, and so on.
    
4. Lists are mutable. This means their values at each index can be changed. Also, they can be shrunk or expanded as you like.
    
5. You may have guessed, but all strings are lists of characters. This is not the same in all programming languages, but in Python, all of the list methods (see #6) can be used on strings.

6. Lists have many built-in methods. To read all about them, check out [this link](https://docs.python.org/3/tutorial/datastructures.html?highlight=list).


### Tuples--ordered, heterogenous, ummutable sequences of data

uples are one of the more confusing features for those new to Python. In form, a tuple looks very much like a list. Let's compare:
List:

```python
names = ['Sylvia', 'Eric', 'Bobby', 'Cassandra']
```

Tuple:

```python
names = ('Sylvia', 'Eric', 'Bobby', 'Cassandra')
```

I can iterate through both in the same way. They are both indexed and the order is constant. So what's the difference? The major difference is that lists can change, and tuples cannot. If I want to change the list names, I can run the append() method on it to add another item, or I can replace the values in any index, or I can pop off a value from my list without creating a new list. Tuples cannot change. They are what we call immutable. Once I've created a tuple, it will always retain the same length and values in the same indices.

What's the point? There are a few big reasons we might use a tuple rather than a list.

First, a tuple, being immutable, provides substantial optimization for your code. Check this out:

```bash
user1@DESKTOP-61VJ97U:~$ python3 -m timeit "['Sylvia', 'Eric', 'Bobby', 'Cassandra']"
10000000 loops, best of 5: 34.3 nsec per loop
user1@DESKTOP-61VJ97U:~$ python3 -m timeit "['Sylvia', 'Eric', 'Bobby', 'Cassandra']"
10000000 loops, best of 5: 34.2 nsec per loop
user1@DESKTOP-61VJ97U:~$ python3 -m timeit "('Sylvia', 'Eric', 'Bobby', 'Cassandra')"
50000000 loops, best of 5: 4.87 nsec per loop
user1@DESKTOP-61VJ97U:~$ python3 -m timeit "('Sylvia', 'Eric', 'Bobby', 'Cassandra')"
50000000 loops, best of 5: 4.9 nsec per loop
```

Timeit runs the code for n loops 5 times and gives you the best average. So, we created the list 10 million times and found the average per loop time was 34.3 nanoseconds and 34.2 nanoseconds. In the second case, we created the same series as a tuple, but this time we did it 50 million times and found that the average loop time was 4.87 adn 4.9 nanoseconds per loop. For a small list, this isn't a bit difference, but imagine if our sequence had a million items in it. 

Tuples provide a great performance boost, but they can't be changed, so if you want to alter the values stored in them, you can't. Tuples are most often used to store a sequence of related values, like a sequence of values pulled from a database. Additionally, tuples are hashable, so we can compare two tuples or use them as keys in a dictionary. 

### Sets--unordered collections of unique values

Sets are also collections of values like a list or a tuple, but they differ in a few important ways. First, they are unordered. This means that if you add a value to a set, you cannot know what index that value might be found at. Second, every value in a set must be unique. To create a set we use curly brackets:

```python
my_set = {'apples', 'bananas', 'grapefruits'}
```

Sets are useful for getting unique values. If I wanted to get unique values in a list, maybe the fastest way would be to add the elements in the list to a set. The resulting set would only keep the unique elements. Sets are also extremely fast for lookups to see if a particular value is present in the collection.

### Dictionaries--collections of key value pairs

A dictionary is another compound data type. It is used to store data in what's called key-value pairs. What this means is that each value has an identifying key or name that you can use to find that value easily. Remember with lists to find an item, you had to know its index, but with a dictionary, you just need to know its key. The basic syntax for a dictionary is {'key': 'value', 'key2': 'value2'...} This means each key and value are paired with each other. Let's take a quick look.

```python
classes = {'name': 'everyday coding', 'students': 'Matt', 'day': 'Wednesday', 'location': 'Admn 306'}
```
So, my classes dictionary keys are 'name', 'students', 'day', and 'location'. Each of these has a corresponding value. If I want to get the name of the class, I just need to call classes['name']. This is very useful for larger complex data sets where you want to be able to pluck out a specific value. Here are some keys to dictionaries:

1. Like lists, dictionaries are mutable. They can change length and any value in them can change.
    
2. Unlike lists, dictionaries are not strictly ordered. There's no guarantee that the first item in the list will always be first. Maybe it will, maybe it won't. So it's totally unreliable to try to grab an item by its index like you did with lists.

3. Dictionaries can hold any types of data as long as they are in key-value pairs. Keys are generally memorable strings. the value could be any type including lists, dictionaries, and tuples. In fact, I'd probably create the dictionary above as more complex.

```python
classes = {'everyday' : {'students':['Matt'], 'location': 'Admn 306', 'day': 'Wednesday'}, 'intro': {...}}
```

Please read the [following to learn more about dictionaries](https://docs.python.org/3/tutorial/datastructures.html?highlight=dictionaries#dictionaries)

You'll also notice that dictionaries look like data structures in other languages. In Javascript, they are similar to objects and in PHP they are the same as associative arrays. Be aware, if you're using Python to process JSON objects you need to parse the object into a dictionary before you can work with it.