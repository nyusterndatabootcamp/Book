# Python fundamentals 2

---
**Overview.**   More core Python. Part 2 of 2.

**Python tools.**  Boolean variables, comparisons, conditionals (if, else), slicing, loops (for), tab completion, function definitions and objects.

**Buzzwords.**  Code block, data structures, list comprehension, objects, PEP8.

**Code.**  [Link](https://github.com/nyusterndatabootcamp/notebooks/blob/master/book_notebooks/python_fundamentals_two.ipynb).

---

We continue our overview of Python's core language, which lays a foundation for the rest of the course.  We go through the material quickly, since we're more interested in the general ideas than the details.  You will feel like you're drinking from a fire hose, but it will sink in if you **stick with it!**


## Reminders

Some things from previous chapters that we'll use a lot:

* Assignments and variables.  We say we assign what's on the right to the thing on the left:  `x = 17.4` assigns the number `17.4` to the variable `x`.

* Help.  We can get help for a function or method `foo` by typing `foo?` in the IPython console or `foo` in the Object explorer.  Try each of them with the `type()` function to remind yourself how this works.

* Data types and structures, e.g., **Number types: integers vs. floats**, **lists**, **strings**, and **dictionaries**, etc.  

* Built-in functions, such as `print()`, `type()` and `len()`. In particular, we learned several type conversions functions. For example, use `str()` to convert a float or integer to a string. Use `float()` or `int()` to convert a string into a float or integer.  Use `list()` to convert a string to a list of its characters.

* Error Messages. Have covered 4 common mistakes: **NameError**, **TypeError**, **Invalid syntax** and **KeyError**. Be familiar with them.

* Comments. Use the hash symbol `#` to add comments to your code and explain what you’re doing.

And while we're reviewing:  Start Jupyter, open a new file, and save as `bootcamp_class_pyfun2.py` in your `Data_Bootcamp` directory/folder.

## Comparisons

Sometimes we want to do one thing if a condition is true, and another if it's false.  For example, we might want to use observations for which the date is after January 1980, the country is India, or the population is greater than 5 million -- and not otherwise.

Python does this with **comparisons**, so called because they involve the comparison of one thing with another.  For example, the date of an observation with the date January 1980.  The result of a comparison is either `True` or `False`.  If we assign a comparison to a variable, we refer to it as a **Boolean**, a name derived from the 18th century mathematician and logician [George](https://espresso.economist.com/a3e8029408056a0791626262beb1e74d) [Boole](https://en.wikipedia.org/wiki/George_Boole). This gives us another type to add our collection:  float, integer, string, list, dictionary, and now Boolean.

Let's try some simple examples to see what we're dealing with.  Suppose we enter `1 > 0` in the IPython console.  What does this mean?  The input and output look like this:

```
In [1]:  1 > 0
Out[1]: True
```

The comparison `1 > 0` is interpreted as a question:  Is 1 greater than 0?  The answer is `True`.  If we enter `1 < 0` instead,the answer is `False`.

A comparison is a Python object, but what kind of object is it?  We can check with the `type()` function:

```python
type(1>0)
```

The answer in this case is `bool` (that is, Boolean), the name we give to expressions that take the values `True` and `False`.  (Actually, it says `<class 'bool'>`, but `bool` is enough to make the point.)

Python comes with a list of "operators" we can use in comparisons.  You can find the complete set in the [Python documentation](https://docs.python.org/3/library/stdtypes.html), but common ones include:

* Equals: `==`
* Greater than: `>`
* Greater than or equals: `>=`
* Does not equal: `!=` (not equals).

We can reverse comparisons (change true to false and vice-versa) with the word `not`.  For example:

```
In [2]: not 1>0
Out[2]: False
```
Think about that for a minute and evaluate it piece by piece. `1>0` returns `True` and `not True` is false. Additionally, remind yourself that spaces don't matter in Python expressions.

We can do the same thing with variables.  Suppose we want to compare the values of variables `x` and `y`.  Which one is bigger?  To see how this works, we run the code:

```python
x = 2*3
y = 2**3
print('x greater than y is', x > y)
```

Here `x = 6` and `y = 8`, so the expression `x > y` (is `x` greater than `y`?) is false.

**Exercise.**  What is `2 >= 1`?  `2 >= 2`?  `not 2 >= 1`? If you're not sure, try them in the IPython console and see what you get.

**Exercise.** What is  `2 + 2 == 4`? How about `1 + 3 != 4`?

**Exercise.**  What is `"Sarah" == 'Sarah'`?  Can you explain why?

**Exercise.**  What do these comparisons do?  Are they true or false?  Why?

```python
type('Sarah') == str
type('Sarah') == int
len('Sarah') >= 3
```

**Exercise (challenging).** What do you think this code produces?

```python
name1 = 'Chase'
name2 = 'Spencer'
check =  name1 > name2
print(check)
```

Run it and see if you're right.  What type of variable is `check`?  What is its value?  Is Chase greater than Spencer?

What did you find? The answer probably is a bit puzzling -- it was to us at first. But we used our "google fu" to figure out what as going on and we found this...

https://stackoverflow.com/questions/4806911/string-comparison-technique-used-by-python

Here is the quick run down, python compares strings in lexicographic ordering. OK...what does that mean? This means the following: First the first two items are compared, and if they differ this determines the outcome of the comparison; if they are equal, the next two items are compared, and so on, until either sequence is exhausted.

What determines the order? In this case note that "S" comes later in the alphabet than "C" thus is has a larger "value", thus "Chase > Spencer" is false.

When comparing uppercase vs. lower case, uppercase come before lower case, stuff like ``*&`` come before. How do I know exactly what is going on... here is a link to the unicode point ordering:

https://en.wikipedia.org/wiki/List_of_Unicode_characters

And scroll down to the Latin Script /Basic Latin table there. There is a number for each possible character. To see the number just type ``ord("z")`` and note how this should give back the value 122 and then look in the table it should have the value 122. In the comparison above, what it is doing is taking the number in this table for the given character and then comparing it to the number for the other character.

## Conditionals (`if` and `else`)

Now that we know how to tell whether a comparison is true or false, we can build that into our code.  "Conditional" statements allow us to do different things depending on the result of a comparison or Boolean variable, which we refer to as a **condition**.  The logic looks like this:

* if a condition is true, then do something.
* if a conditions is false, do something else (or do nothing).

To repeat:  a condition here is a comparison or Boolean variable and is either true or false.

<!--We use `if` to tell Python what to do if the condition is true, and `else` to do the same if the condition is false.  Picture a decision tree with two branches, one for true, one for false.  If Apple offers us a job, move to California.  If not, stay in New York.-->

**`if` statements**  tell the program what to do if the condition is true:

```python
if 1 > 0:    # read this like "if 1>0 IS TRUE, then do the thing on the next line"
    print('1 is greater than 0')
```

The syntax here is precise:

* The `if` statement **ends with a colon**. That's standard Python syntax, we'll see it again.  It's not optional.
* The code that follows is **indented exactly four spaces**. Also not optional. Jupyter does it automatically.

Both of these features -- a colon at the end of the first line, indent the rest four spaces -- show up in lots of Python code.  It's very compact, and the indentation makes the code easy to read.

**Exercise.**  Change the code to

```python
if 1 < 0:
    print('1 is less than 0')
```

What do you think happens?  Try it and see.

Here's another example.  Again, we do something if the condition is true, nothing if the condition is false.  In this example, the condition is `x > 6`.  If it's true, we print the number.  If it's false, we do nothing.  The code is

```python
x = 7       		# we can change this later and see what happens

if x > 6:
    print('x =', x)

print('Done!')
```

Here we've set `x = 7`, which makes the condition `x > 6` true.  The `if` statement then directs the program to print `x`.  The blank lines are optional; they make the code easier to read, which is generally a good thing.  The statement `print('Done!')` is just there to tell us that the program finished.

**Exercise.** What happens if we set `x = 4` at the top?  How do we know?

**`else` statements** tell the program what to do if the condition is false.  If we want to do one thing if a condition is true and another if it is false, we would use `if` for the first and `else` for the second.  The second part has been missing so far.  Here's an example:

```python
x = 7

condition = x > 6

if condition:
    print('if branch')             # do if true
    print(condition)
else:
    print('else branch')           # do if false
    print(condition)
```

The `else` statement adds the second branch to the decision tree:  what to do if the condition is false.  Try this with `x = 4` and `x = 7` to see both branches in action.


**Exercise.** Take the names `name1` and `name2`, both of them strings.  Write a program using `if` and `else` that prints the name that comes first in alphabetical order.  Test your program with `name1 = 'Dave'` and `name2 = 'Glenn'`.


## Slicing

We can access the elements of strings and lists by specifying the item number in square brackets. This operation is referred to as **slicing**, probably because we're slicing off pieces, like a cake.  The only tricky part of this is remembering that **Python starts indexing at zero**.

**Exercise.**  Take the string `a = 'some'`.  What is `a[1]`?

What just happened?  Python starts indexing at zero.  If we want the first item/letter, we use `a[0]`.  If we want the second, we use `a[1]`.  And so on.  We can summarize the numbering convention by writing the word `some` on a piece of paper.  Below it, write the numbers, in order:  0, 1, 2, 3.  Label this row "counting forward."

We can also count backward, but again Python has its own numbering convention.  If we want the last letter, we use `a[-1]`.  And if we want the one before the last one, we type `a[-2]`.  In this case we get the same answer if we type `a[2]`.  Both give us `'m'`.

Let's track this "backward" numbering system in our example.  Below the "counting forward" numbers, start another row.  Below the letter `e` writes -1.  As we move to the left, we type, -2, -3, -4.  Label this row "counting backward."

**Exercise.** Take the string `firstname = 'Monty'` and write below it the forward and backward counting conventions.  What integer would you put in square brackets to extract the third letter (`n`) under each system?


**Exercise.** Find the last letter of the string `lastname = 'Python'`.  Find the second to last letter using both the forward and backward counting conventions.

We can do the same thing with lists, but the items here are the elements of a list rather than the characters in a string.  The counting works the same way.  Let's see if we can teach ourselves.

**Exercise.** Take the list `numberlist = [1, 5, -3]`.  Use slicing to set a variable `first` equal to the first item.  Set another variable `last` equal to the last item.  Set a third variable named `middle` equal to the middle item.


We've seen how to "slice" (extract) an item from a string or list.  Here we'll show how to slice a range of items. For example, slice the last five characters from the string `c = 'something'`.

Recall that in Python we start counting at zero. If we want the first letter in `c`, we use `c[0]`.  If we want the second, we use `c[1]`.

If we want more than a single letter, we need to specify both the start and the end.  Let's try some examples and see what they do:

```python
c = 'something'
print('c[1] is', c[1])
print('c[1:2] is', c[1:2])
print('c[1:3] is', c[1:3])
print('c[1:] is', c[1:])
```

Let's go through this line by line:

* The first print statement gives us `o`, the second letter of `something`. It's element 1 because we start numbering at zero.
* The next one does the same.  Why not two letters?  Let's try another one and see.
* The following line gives us `om`, the second and third letters.  Why?  Perhaps you figured it out.  If not, this is the logic:  the second number in `1:3`, namely `3`, is **one more than the end**.  So the range `1:3` gives us the second and third letters.  Confusing, for sure, but that's how it works.
* The last line has no second number.  By convention it goes all the way to the end.  The slice `c[1:]` goes from the second letter (the first number 1) to the end, giving us `omething`.

Some practice:

**Exercise.** Set `lastname = 'Python'`. Extract the string `'thon'`.

**Exercise.** Set `numlist = [1, 7, 4, 3]`. Extract the middle two items and assign them to the variable `middle`. Extract all but the first item and assign them to the variable `allbutfirst`.  Extract all but the last item and assign them to the variable `allbutlast`.

**Exercise.**  Take the string `c = 'something'`.  What is `c[:3] + c[3:]`?


## Loops over lists and strings (`for`)

There are lots of times we want to do the same thing many times, either on one object or on many similar objects.  An example of the latter is to print out a list of names, one at a time.  An example of the former is to find an answer to progressively higher degrees of accuracy.  We repeat an operation as many times as we need to get a desired degree of accuracy.  Both situations come up a lot.

Here's an example in which we print all the items in a list, one at a time:

```python
namelist = ['Chase', 'Dave', 'Sarah', 'Spencer']    # creates the list "namelist"
# below, the word "item" is arbitrary. End the line with a colon.
for item in namelist:    # goes through the items in the list one at a time
   print(item)    # indent this line exactly 4 spaces
# if there is code after this, we'd typically leave a blank line in-between
```

This produces the output

```python
Chase
Dave
Sarah
Spencer
```

<!--
Let's go through the code line by line:

* The first line creates the list `namelist`.  Nothing new here.
* The `for` statement goes through the items in the list one at a time.  As with `if` statements, it ends with a colon.  The variable name `item` is arbitrary.
* The line that follows is indented exactly four spaces.
* If there's code after this, we would typically leave a blank line in between.  That's convention, not necessity.
-->

Note that `item` changes value as we go through the loop.  It's a variable whose value actually varies.

We say here that we **iterate** over the items in the list and refer to the list as an **iterable**:  that is, something we can iterate over.  The terminology isn't important, but that's what it means if you run across it.

**Exercise.** What happens if we replace `item` with `banana` in the code above?

**Example.**  We use a loop to compute the sum of the elements of a list of numbers:
```python
numlist = [4, -2, 5]
total = 0
for num in numlist:
    total = total + num

print(total)
```
The answer (of course) is 7.

**Exercise.** Adapt the example to compute the average of the elements of `numlist`.

We can also run loops over the characters in a string.  This one prints the letters in a word on separate lines:

```python
word   = 'anything'
for letter in word:
    print(letter)
```

(You might think we could come up with a more interesting example than this.  Sadly no, but we welcome suggestions.)

**Example.**  Here's one that combines a `for` loop with an `if` statement to identify and print the vowels in a word:

```python
vowels = 'aeiouy'
word   = 'anything'
for letter in word:
    if letter in vowels:
        print(letter)
```

(Adapted from [SciPy lecture 1.2](https://scipy-lectures.github.io/intro/language/control_flow.html#advanced-iteration).)  Describe what each line does as well as the overall result.

**Example.** What about the consonants?  Note the word `not` below:

```python
vowels = 'aeiouy'
word   = 'anything'
for letter in word:
    if letter not in vowels:
        print(letter)
```

**Exercise.**  Take the list `stuff = ['cat', 3.7, 5, 'dog']`.

* Write a program that prints the elements of `stuff`.
* Write a program that tells us the `type` of each element of `stuff`.
* *Challenging.* Write a program that goes through the elements of `stuff` and prints only the elements that are strings; that is, the print the elements where function `type` returns the value `str`.


<!--
* Create another list `more_stuff = ['Sarah', 75, 42.5]`. Remember `append()`? Write a program to add the items from stuff to list `more_stuff` using `append()`.
-->

<!-- See [reddit](http://www.reddit.com/r/Python/comments/35ubwo/newbie_for_programming_i_am_working_on_this/).
?? also:  extract vowels, string what's left together.
-->


## Loops over counters (`range()`)

We now know how loops work.  Here's another version in which we loop over something a fixed number of times. For example, we might want to sum or average the values of a variable.  Or value a bond with a fixed number of coupon payments.  Or something.

The new ingredient is the `range()` function. `range(n)` gives us all the integers (whole numbers) from `0` to `n-1`.  (If that sounds strange, remind yourself how slicing works.)  And `range(n1, n2)` gives us all the whole numbers from `n1` to `n2-1`.  We can use it in lots of ways, but loops are a prime example.

Some examples illustrate how this works:

**Example.** This is one of the simplest uses of `range()` in a loop:

```python
for number in range(5):     # the variable "number" can be anything
    print(number)
```

It prints out the numbers 0, 1, 2, 3, and 4.  (Ask yourself:  Why doesn't it go to 5?)  This is like our earlier loops, but `range(5)` has replaced a list or string as the "iterable."

Here's a minor variant:

```python
for number in range(2, 5):
    print(number)
```

It prints out the numbers 2, 3, and 4.

**Example.** We compute and print the squares of integers up to ten.  ([Paul Ford](http://www.bloomberg.com/graphics/2015-paul-ford-what-is-code/) comments:  "Just the sort of practical, useful program that always appears in programming tutorials to address the needs of people who urgently require a list of squares.")   We do that with a `for` loop and the `range()` function:

```python
for number in range(1, 11):
    square = number**2
    print('Number and its square:', number, square)
```

Here we have `number` start at one and work its way up to ten.

**Example.** Here we compute the sum of integers from one to ten:

```python
total = 0
for num in range(1, 11):
    total = total + num

print(total)
```

The answer is 55.

**Example.** Here's one that combines a loop and an `if` statement:

```python
for num in range(10):
    if num > 5:
       print num
```

**Exercise.**  Write a loop that computes the first five powers of two.

**Example.**  Consider a bond that pays annual coupons for a given number of years (the maturity) and a principal of 100 at the end.  The yield-to-maturity is the rate at which these payments are discounted.  Given values for the coupon and the yield, the price of the bond is

```python
maturity = 10
coupon = 5
ytm = 0.05 				# yield to maturity

price = 0
for year in range(1, maturity+1):
    price = price + coupon/((1+ytm)**year)

price = price + 100/((1+ytm)**maturity)
print('The price of the bond is', price)
```

The answer is 100, which we might know because the coupon and yield are the same once we convert the latter to a percentage.  Python gives us `99.99999999999997`, which is the computer's version of 100.

**Digression.**  When we originally wrote this code, we used the variable name `yield` instead of `ytm`.  This was problematic for the following reason: evidently the name `yield` is reserved for [something else](https://pythontips.com/2013/09/29/the-python-yield-keyword-explained/).  As general rule, it's a good idea to pay attention to issues of this nature, e.g. don't name a variable the same as a built-in function/method, etc.

**Loop with condition.**  Sometimes we want to go through a loop until some condition is met.  This combination of a loop and a condition requires an extra level of indenting.  It also introduces a new ingredient:  the `break` statement, which tells Python to exit the loop.

**Example.** Suppose we want to compute the sum of integers until the sum reaches 100.  We could use the code

```python
maxnum = 20 			# guess of number above our limit

total = 0
for num in range(maxnum):
    total = total + num
    if total > 100:
        break  			# exit loop

print('At num =', num, 'we had total =', total)
```

The `if` statement starts with a colon and the statement following it (`break`) is indented four spaces more (eight in total).  `break` is a special command that ends a loop early.

Let's review:

**Exercise.** In Portugal and Greece, policymakers have suggested reducing their debt by cutting the coupon payments and extending the maturity.  How much do we reduce the value of the debt if we reduce the coupons to 2 and increase the maturity to 20?

**Exercise.**  Consider the list `namelist = ['Chase', 'Dave', 'Sarah', 'Spencer']`.  Write a loop that goes through the list until it reaches a name than begins with the letter `S`.  At that point it prints the names and exits the loop.


## List comprehensions

That's a mouthful of jargon, but the idea is that we can create lists (and do related things) using implicit loops that we refer to as **list comprehensions**.  "Implicit loops" essentially means that they are doing the same thing as a loop, but that the syntax is more compact.  This shows up a lot in Python code.

**Example.** Consider the loop above that prints out the elements of the list `namelist` one at a time:

```python
namelist = ['Chase', 'Dave', 'Sarah', 'Spencer']
for item in namelist:
    print(item)
```

A list comprehension gives us more compact syntax for the same thing:

```python
[print(item) for item in namelist]
```

As with loops, the variable `item` is a dummy:  we can use any name we wish.  Replace `item` with your pet's name to see for yourself.

**Example.** Take the list `fruit = ['apple', 'banana', 'clementine']`.  Here's a list comprehension that creates a new list of capitalized fruits:

```python
FRUIT = [item.upper() for item in fruit]
```

Try it and see.  And think about the loop version a minute to see what we've avoided.

**Example.** We can do the same with a condition.  This one takes the list `fruit` and creates a new list that contains only those names with six letters or less:

```python
fruit6 = [item for item in fruit if len(item)<=6]
```

**Exercise.** Take the list `fruit` and create a new list with the first letter capitalized.  *Hint:* What method would you use to capitalize a string?


**Exercise.** Take the list of growth rates `g = [0.02, 0.07, 0.07]`.  Write a list comprehension that multiplies each element by 100 to turn it into a percentage.

Final point about this: List comprehensions are nice to use for simple cases. However, for more complicated situations, comprehensions be very hard to read and understand. Hence, a traditional ``for`` loop would be more appropriate. 


## Defining our own functions

It's easy to create our own functions -- experienced programmers do it all the time.  A common view is that we should never copy lines of code.  If we're copying, we're repeating ourselves.  What we should do instead is **write a function once and use it twice**.  More than that, breaking a long program into a small number of functions makes the code easier for others to read, which is always a good thing.  As we become more comfortable with Python we'll use functions more and more.

**Defining functions.** The simplest functions have two components:  a **name** (what we call it) and a list of **input arguments**.  Here's an example:

```python
def hello(firstname):               # define the function
    print('Hello,', firstname)

hello('Chase')                      # use the function
```

Let's go through this line by line:

* The initial `def` statement defines the function, names it `hello`, identifies the input as `firstname`, and ends with a colon (**:**).
* The following statement(s) are indented the usual four spaces and specify what the function does.  In this case, it prints `Hello,` followed by whatever `firstname` happens to be.  Python understands that the function ends when the indentation ends.
* The last line "calls" the function with input `Chase`.  Note that the name in the function's definition and its use need not be the same.

**Function returns.** Our function `hello` has a name (`hello`) and an input argument (`firstname`), but returns no output. Output would create a new value that Python could call later in the code, like when you set `x = 2` then used `x` later on. Here we print something but produce no other output.

In other cases, we might want to send output back to the main program.  We do that with a **return** statement, a third component of a function definition.  Here's an example

```python
def squareme(number):
    """
    Takes numerical input and returns its square
    """
    return number**2        # this is what the function sends back

square = squareme(7)        # assign the "return" to variable on left
print('The square is', square)
```

And here's another one:

```python
def combine(first, last):
	"""
	Takes strings 'first' and 'last' and returns new string 'last, first'
	"""
	lastfirst = last + ', ' + first
    return lastfirst                    # this is what the function sends back

both = combine('Chase', 'Coleman')      # assign the "return" to both
print(both)
```

Here we return the string `'Coleman, Chase'` and assign it to the variable `both`.  Note, too, the comment in triple quotes at the top of the function. That's standard procedure, we recommend it.

The return is an essential component of many functions.  Typically when we read the documentation for a function or method, one of the first things we look for is what it returns.

**Exercise.** Create and test a function that returns an arbitrary power of 2:  the input `n` (an integer) returns the output `2**n`.  Use `n=2` and `n=5` as test cases.

**Exercise.**  Create and test a function `nextyear` that takes an integer year (say 2015) and returns the following year (2016).

**Exercise.** Use the Object inspector to get the documentation for the built-in function `max`.  If the input is a list of two or more numbers, what does `max()` return?

**Exercise (challenging).**  Create and test a function that takes a string year (say, `'2015'`) and returns a string of the next year (say, `'2016'`).

## Objects

This is a key component of python, which is an [object oriented programming language](https://en.wikipedia.org/wiki/Object-oriented_programming). What does that mean? For us this means that every thing is really an object with associated **methods** and **attributes**. A method is like a function that already togo with the given object. Methods in python are always completed with `()` . Attributes are go-to-go attributes about the object that can be accessed easily. What this means is that there are simple built-in ways to get information and perform operations on objects without having to write our on functions. A typical example is the `dict()` object which has methods to grab its keys and values, etc.

Functions and methods differ primarily in their syntax:

* Syntax of a **function**: `function(object)`
* Syntax of a **method**: `object.method()`
* Syntax of a **attribute**: `object.attribute`

We used the former in the previous section and consider the latter two here.

What methods are available to work with a given object?  Take, for example, the list `numberlist = [1, 5, -3]`.  To get the list of available methods, type in a code cell:

```python
numberlist.[tab]    # here you hit the tab key, don't type in the word "tab"

```

This wonderful piece of technology is referred to as **tab completion**.  The ingredients here are the object (here `numberlist`), the period or dot, and the tab key.  When you hit tab, a window will pop up with a list of methods in alphabetical order.  In our example, the list starts like this:

```python
numberlist.append
numberlist.clear
numberlist.copy
numberlist.count
```

If we want more information about a method, we can type `object.method?` in a code cell.  For the method `numberlist.append`, we get the description

```python
Definition:  append(object)
Type:  Function of None module
L.append(object) -> None -- append object to end.
```

Well, that's pretty opaque, maybe we oversold this approach.  What `append` does is add an item to the end of a list.  Try using `append()`, then use `print()` to see the results:

```python
numberlist.append(7)
print(numberlist)
```

That's another way to get information about a method: try it and see what happens.

**Digression.**  We're trying to keep this simple, but we also want it to be accurate. Tab completion gives us a list of two things:  *attributes* (properties of the object) and *methods* (essentially functions with different syntax).  The distinction isn't important to us, although a method requires the use of parentheses `()` (just like functions); attributes do not. How to tell which is which...some of our teams approach is to try both and see what happens.

**Example.** Set `firstname = 'Chase'`.  The method `lower` converts it to lower case.  If we type `firstname.lower` into the object inspector, we see that it comes with parentheses for additional inputs.  So we type `firstname.lower()` into a code cell.  The response is `'chase'`.  The parentheses are there to provide additional inputs -- arguments, we call them.  Without the parentheses, it doesn't work.


**Exercise.** Find a method to convert `firstname` to all upper case letters.

**Exercise.** This one also came up in our work.  Suppose we have a variable `z = '12,345.6'`.  What is its type?  Convert it to a floating point number without the comma.  Hint:  Use tab completion to find a method to get rid of the comma.

<!-- z = z.replace(',', '') -->

**Exercise.**  Run the code

```python
firstname = 'John'
lastname  = 'Lennon'
firstlast = firstname + ' ' + lastname
```

Find a method to replace the n's in `firstlast` with asterisks.

---

## Review Questions

**Exercise.** What type is each of these expressions?  What length?

* `'abcd'`
* `[1, 3, 5, 7]`
* `{1: 'one', 2: 'two'}`
* `123`
* `123.0`
* `list('abcd')`
* `range(3)`
* `list(range(3))`

**Exercise.** Which of the following are `True` and which are `False`?

* `2 >= 1`
* `2 >= 2`
* `2 != 2`
* `'this' == "this"`
* `'Chase' < 'Dave'`
* `'Chase' < 'Dave' or 'Spencer' < 'Glenn'`
* `'Chase' < 'Dave' and 'Spencer' < 'Glenn'`


**Exercise.** Write a program that prints the last letter of each item in the list `names = ['Chase', Dave', 'Sarah', 'Spencer']`.  **Bonus (optional):** Print the last letter only if it's a vowel.


**Exercise.** Write a function `lastletter` that extracts the last letter from a string.  Use `'Gianluca'` as your test case.

<!--
**Exercise.** Run the statement `output = list(range(3))` and describe the output.  What does it do?
-->

**Exercise (challenging).** Take the list of bond yields `y = [0.01, 0.02, 0.03]` for maturities of one, two, and three years.

* What happens if you try to multiply all of them by 100 with `100*y`?
* How would you accomplish the same task (multiply all the elements of `y` by 100) with a loop?
* How would you accomplish the same task (multiply all the elements of `y` by 100) with a list comprehension?

**Exercise (challenging).** Start with the lists `l1 = [1, 2, 3]` and `l2 = ['one', 'two', 'three']`.

* What does `list(zip(l1,l2))` do?
* What does `dict(list(zip(l1,l2)))` do?
* Create a list that contains only the number names in `l2` that have three letters.
* Write a list comprehesion that constructs the list of tuples `[(1, 1), (2, 4), (3, 9)]`.
* Convert the list of tuples into a dictionary.


**Exercise.** Set `name = 'Jones'`.  Use (a) tab completion to find a method that coverts `name` to upper case (capital) letters and (b) the Object inspector to find out how to use that method. <!-- *Bonus:* How else can you get help in Spyder for methods and functions?-->

**Exercise (challenging).** Use tab completion and the Object inspector to find and apply a method to the string `name` that counts the number of appearances of the letter s.  Use `name = 'Ulysses'` as a test case.


## Summary

* **Boolean variable and its operations**: We conduct the comparison operation on the right: x = 3 > 2, and we can assign the boolean values (True or False) to the variable x. We also learned how to compare two strings.

* **"if" conditional statement**: it allows us to do different things depending on the result of a comparison or Boolean variable.

* **Slicing**: we learn **Forward** and **Backward** counting conventions in a list, do you know when to select which? We also cover using **`:`** operator to select groups of data.

* **"for" Loop**:
    * We can use `for` to loop through any iterable objects.
    * We talk a common built-in iterable object/data sturcture: `range` to help us with the data slicing/indexing.

* **Functions**: we learn how to define and use customized functions.

* **Objects**: a core concept in a object oriented programming language like python. It can help us understand how we can use **`.`** operations (**tab completion**) to call methods and attributes in an object.


## Resources

See the resources in the previous chapter, especially [Codecademy](https://www.codecademy.com/tracks/python).  If you work your way up to Advanced Topics, you'll be in good shape for anything that follows.

Additional resources:

* The official [Python Tutorial](https://docs.python.org/3.4/tutorial/controlflow.html) has a nice introduction to "control flow language" that includes comparisons, conditional statements, and loops.

* [CodingBat](http://codingbat.com/python) has a great collection of exercises.  Significantly more demanding than ours.  Runs online.

* Udacity has a free [Introduction to Computer Science](https://www.udacity.com/courses/cs101) course that covers Python from a more technical perspective.  Recommended for people who want to understand the structure and logic of the language.

* This is way [more about comprehensions](https://gist.github.com/bearfrieze/a746c6f12d8bada03589) than you ever wanted to know, but it's so beautifully done you might want to take a look.

One last one, but only if you're curious about floating point numbers.  Ok, that's approximately no one.  Try this anyway and think about what's going on (it also gives us an idea that we don't want to check for strict equality for floating point numbers -- Better to check whether they are close enough):

```python
0.1 + 0.2 == 0.3
```

False?  More [here](http://blog.reverberate.org/2016/02/06/floating-point-demystified-part2.html).
