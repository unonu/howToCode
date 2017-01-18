How to program.

First, I suppose it is important to note that I'm going to state some things
explicitly in this guide that almost everyone "knows." This is mainly to make
absolutely certain that we're on the same page.

Second, there's no better way to learn this stuff than by doing it. 

Okay.

Introduction
============

The most basic and most important thing to cover is how the computer works.
Every computer operates in the same general way. A program is loaded from memory
and given to the CPU. The program then executes its routine, taking in input,
producing some output and finally terminating.

In order to make this easier, we're going to make a couple of assumptions:
There is only one program running on the computer at a time and only one CPU,
and we have the  ability to do complex instructions like reading keyboard or
mouse input or sending graphics to the screen. In reality, there can be hundreds
of programs all sharing one CPU, and the instructions the CPU understands are
very simple (in terms of what they do, but they were very complicated to
create.)

So to give a little example, let's do a simple program that adds two and two and
gives us an answer. We'll approach this from a high level (more of an abstract/
conceptual way) to keep it focused. So first we write the code to describe what
we want the program to do:

`ADD 2, 2`

Okay so some more assumptions: in order to reduce the amount of typing we have
to do, we'll be using a shorthand method of writing code. This short hand is NOT
REAL CODE, but it will help us to describe the kind of code we want. We'll also
frequently make assumptions that the CPU will understand commands we give it,
like PRINT_TEXT "hello." In reality printing text is pretty involved process,
but we can assume that someone else has done the work of telling the computer
how to do it.

Now let's look back at the code: `ADD 2, 2`. So we're telling the computer to use
its ADD instruction on the two inputs 2 and 2. So we save this code to the
computer's memory and we tell the computer to run it (don't worry about how we
tell it just yet.) When the computer acknowledges what program it's supposed to
run, it will go through the following chain of events:

-Load the code onto the CPU.
-Prepare the CPU to perform the instruction.
-Take in any inputs and make the ready to be accessed.
-Execute the instruction while allowing it access to the input values.
-store the output into memory.

This process can be referred to as the execution pipeline. It's simply just the
order a program goes through to get a result. This result is typically called
the *return value* because you asked the computer to do something, it performed
some calculations and then returned the result to you.

Functions
=========

This leads us directly to what we call routines, methods or *functions*. See,
CPUs actually have a relatively small number of built in instructions compared
to all of the things we might want a computer to do. For instance, the CPU
doesn't have an instruction to calculate the area of a circle. However,
calculating the area of a circle is really just a series of mathematical steps;
things the CPU _does_ know how to do. So in order to make our lives easier,
people have created what is known as programming languages. These languages
allow us to express our ideas as sequences of high level steps which can later
be boiled down to sequences of low level steps that a CPU would understand. For
instance:

`CIRCLE_R 4`

represents our code, but this will get translated (for the CPU) to:

`MULTIPLY 2, 3.1415, 4, 4`

which is 2*pi*r².

Cool, so remember CPUs are sort of simple and limited, but by using a
programming language, we can express complex ideas in a way that is still easy
for humans to understand. The other really important thing to remember is that
we can essentially describe our _own_ CPU instructions by chaining together
functions. This is similar to how `CIRCLE_R` is defined to be a specific form of
`MULTIPLY`, but it can get a lot more powerful than that. Okay, next: variables!

Variables
=========

Variables are extremely useful because they can store data. To give a quick
example, say our `MULTIPLY` function from earlier could only take in two inputs.
Well ,that would make it impossible for our CPU to calculate the area of a
circle based on just the radius. We would have to convert the function to
something like:

`MULTIPLY 6.283, 16`

but if we're going to be doing most of the work ourselves, then what's the
point? Using variables allows us to get around this. Let's redefine how
`CIRCLE_R` works:

`a = MULTIPLY 2, 3.1415;
b = MULTIPLY 4, 4;
c = MULTIPLY a, b;
return c`

Now, `CIRCLE_R` is a sequence of three `MULTIPLY` commands. We also have three
variables inside this function: `a`, `b` and `c`. Variables `a` and `b` hold the
values of 2*pi and r², respectively. Variable `c` eventually holds the final
result, which is what we ultimately return in the last line of our code.
Nowadays, you can have as many variables as you want (depending on the language)    
and they can generally be called whatever you like. For the examples in this
tutorial, we're going to only use lowercase letters, numbers and the underscore
when we spell out variable names. This is to help emphasise the difference
between variable which are just holding data and functions (which are really
variables too, but the don't point to data, they point to a sequence of
instructions.) We'll be referring to functions in all caps, if you hadn't
noticed already.

Now, in addition to using variables as places to hold temporary data, you can
also use them to represent data that you as the programmer *did not know at the
time you wrote the code*. This is extremely powerful. To demonstrate, we return
to our favourite circle example once more. This time, we are going to define
`CIRCLE_R` so that it can take in any number as the radius and provide us with
the appropriate result. Let's see...:

`CIRCLE_R r :
	a = 6.283;
	b = MULTIPLY r, r;
	c = MULTIPLY a, b;
	return c`

This time, `a` was simply set to 6.283 since it is always going to be the same
(no need to waste valuable CPU time!) You can also so how `b` is now the result
of `r` squared, and result `c` is `a` times `b`. The most important thing to
note here is that because `r` is not given a value in this portion of code, `b`
*cannot be pre-determined* because it doesn't know the value of `r` and thus `c`
cannot be pre-determined because it doesn't know the value of `b`. It's a simple
thing to assign `r` a value however by... reading the next section!

Functions are useful not only because they let us easily represent a complex
portion of code, but also because they allow us to do it repeatedly. Ummm, if
you're coming off the previous paragraph, bear with me a moment, we'll get to
assigning `r` a value. But first...

Functions Pt. II: Calls
=======================

A *program* consists of a a single function. This might seem useless, because
what good is a program that can only do one thing? Well you've seen how you can
use the CPU's basic instructions inside of a function, but you can also use
other homemade functions inside of functions! This little trick is where much of
the power of programming lies.

Okay so say we had a program that runs a function called `MAIN`. Let's go ahead
and define that function:

`MAIN :
	area1 = CIRCLE_R 4;
	area2 = CIRCLE_R 5;
	PRINT area1;
	PRINT area2`

Our function `MAIN` essentially calculates the area of two different circles.
The first circle has a radius of four and the second has a radius of five. In
both cases, the function `CIRCLE_R` is exactly the same. We expect to get a
different answer in each case, but how can that be possible if the function is
exactly the same? Well, this is where the variable `r` comes back. `r` is a
special kind of variable called an argument. All this means is that, even though
the variable has no value assigned to it when it was defined, it will be given
a variable when the function it is associated with is called (when a function is
used, we say it gets _called_.) For the purposes of our examples, you'll be able
to identify argument type variables by their position next to a function name in
the definition.

Back to our example, `CIRCLE_R` is the same both times it's called, but when it
is called, we give it a different argument value both times. So the first time
`CIRCLE_R` is called, the first argument (which in `CIRCLE_R` we've called `r`)
is assigned a value of four. And now that `r` has a value, the variable `b` can
be solved, and then the variable `c` can finally be solved. Then the variable be
is "returned" as the result of the function. And, if `area1` is equal to the
result of `CIRCLE_R 4`, then `area1` is equal to `c`! Cool right? This whole
process happens again in the next line with `area2` and an argument value of
five. If you're wondering whether the variables might get mixed up between the
two times that `CIRCLE_R` is called, don't worry. Every time a function is
called, all of the variable related to the function get re-made. In other words,
the computer will know that `r` the first time `CRICLE_R` is called is a
different `r` from when `CIRCLE_R` is called a second time.

Let's take another look at our `MAIN` function from earlier:

`MAIN :
	area1 = CIRCLE_R 4;
	area2 = CIRCLE_R 5;
	PRINT area1;
	PRINT area2`

The `MAIN` function here is different from `CIRCLE_R` and even from `ADD` or
`MULTIPLY`. `MAIN` has (or "takes in," as we say) zero arguments, and returns no
value. Functions like this won't be super useful for now, but keep in mind that
its possible to take no input and return no value. The function `PRINT` is also
different because it takes in an argument, but doesn't return anything. This is
because `PRINT` is a function that somehow prints its argument's value to the
screen and no further output is necessary. This kind of function is useful for
performing some kind of output, such as printing or drawing something on-screen
or saving a file. And, of course, you've already been working with functions
like `CIRCLE_R` which both takes in an argument and has a return value.
Technically, this form of function can be used to accomplish anything, and the
other two forms are just there for convenience.

Quick Tips
==========

Now that variables and functions have been introduced, I'll share a couple of
tips about how they can be used. For instance, the majority of basic functions
like ADD, MULTIPLY, SUBTRACT etc. are so commonplace that most languages use
the usual symbols to represent those functions:

`ADD 2, 2` becomes `2 + 2`
`MULTIPLY a, b` becomes `a * b`

and so on. Depending on which language you choose, these symbols might change,
but you can usually count on +, -, *, / and ^ to do what you would expect.

Another tip is that you don't always have to store a return value to use it
somewhere else. E.g. :

`PRINT( CIRCLE_R 4 )`

The parentheses will make sure that `CIRCLE_R 4` is called first. In fact, just
like in algebra, parentheses will (usually) make sure that things are called in
the order you expect (things inside get evaluated first.)

If it wasn't clear from the last two lines in the `MAIN` function, variables can
be used as argument values too. So say I wanted to print the area of a circle
with a radius entered by the user, I could write a function:

`FOO :
	r = GET_INPUT;
	PRINT( CIRCLE_R r )`

assuming `GET_INPUT` is some function that gets input from the keyboard, and
that the user enters a number.

Okay only a few more things to cover before we get to the really interesting
stuff.

Control Structures
==================

Control structures are used to execute different portions of code based on
certain conditions. There are different schools of thought about how and when to
use control structures, but just remember that control structures can get you
out of any tough situations. There are three basic control structures that 99%
of languages implement:

-The if-then-else statement
-The while loop
-The for loop

If-then-else
------------

The if-then-else statement (usually we just call it the if statement) is very
useful for testing a condition and then executing code based on the value of the
condition. It works like this:

`if SOME_CONDITION:
	THEN DO SOMETHING
	...`

Now's probably a good time to mention *types* as well. Variables can hold
any kind of value, and these values have different kinds of "types". The common
types are *integers* (whole numbers without decimals,) *floats* (numbers *with*
decimals,) *strings* (a string of characters surrounded by quotes. These represent
literal words, because otherwise the computer would think the words were more
source code,) *functions* (which we covered,) *variables* (also covered) and
*booleans* (also called bools) which are what we care about right now. A boolean
value is simply the logical value true or false. In our fake example language,
we'll represent logical true with `TRUE` and logical false with `FALSE`.

So let's fill out the if statement template from above as a little example: 

`if TRUE:
	print "it was true"`

This example will print out "it was true" because TRUE is always logical true.
Because the if statement will execute it's code if its condition evaluates to
true, then it goes ahead and executes the print statement. Let's look at another
example:

`print "1"
if FALSE:
	print "2"
print "3"`

Because the if statement's condition is FALSE (or we say "evaluates to FALSE,")
then the code associated with it will *not* execute, and the code will output "1
3" .

Obviously it's kind of stupid to only use TRUE and FALSE as your conditions, so
typically you'll be putting a variable in there. If you need more control, you
can even put equations like `x > 10` or `y is TRUE and z*2 < -4`. And even more
importantly, if you want to use the result of a function without storing that
result first, you can do that too: `if (foo 4):` where `foo` is a function that
takes in one argument (a number) and returns some bool value TRUE or FALSE.

The last point about if statements is that instead of chaining a bunch of if
statements together, you can use `else`. Keep in mind, however, that else only
really makes sense *if the conditions you are trying to group or the results you
are trying to create are related*. So:

Good:
`if x == 10:
	y = 1
else if x == 12:
	y = 2
else
	y = 0
end`

Good:
`if x == 10:
	a = 1
else if x == 12:
	b = 2
else
	c = 0
end`

Good:
`if x == 10:
	a = 1
else if y == 12:
	a = 2
else
	a = 0
end`

Bad:
`if x ==10
	a = 1
else if y == 12:
	b = 2
else
	c = 0
end`

Notice in that last example how none of the statements are really related to
each other. Also I kinda slipped in the failsafe `else` that has no conditions.
If all of the other statements fail, then the failsafe `else` will execute its
code.

While Loop
----------

The loop is ultra powerful, allowing you to repeat code over and over again.
Loops will eventually be the core of our game development techniques. The basic
loop is the while loop. While loops check a condition, much like the if
statement, and then performs it's portion of code if the condition was true.
Once that portion of code is completed, the while statement evaluates its
condition again and, if the condition is true, repeat the process. Only if the
condition becomes false does the loop end allowing the program to continue after
the loop's code.

While loops are written sort of like this:

`while SOME_CONDITION:
	DO SOMETHING`

And by way of example:

`x = 0
while x < 10:
	x = x + 1
print x`

Will print out "10" . Just keep in mind that the loop condition needs to become
false *eventually*. Unless you _want_ an infinite loop...

For Loop
--------

The for loop is similar to the while loop, except it has built in limits for the
number of times it can loop. It's called a "for" loop because it loops once
*for* every item in a collection/set of things. Typically, the set of things is
going to be a set of numbers. In fact, in many languages, the basic for loop can
only deal with numbers. For loops look sort of like this:

`for x=START_VALUE, END_VALUE:
	DO SOMETHING`

or sometimes:

`for x in SOME_SET:
	DO SOMETHING`

The first form will make a variable `x` (which will only exist within the loop,
so don't try to use `x` once the loop has finished) and set it equal to
`START_VALUE`. Then the loop code will execute. After one execution, the loop
cycles back and increments `x` by 1. This process repeats until `x` is equal to
the `END_VALUE`. Once `x` reaches `END_VALUE`, the loop code exits and the
program continues on.

The second form makes a variable `x` and sets it equal to the first item inside
of `SOME_SET`. Then the loop code executes. After this, the loop cycles and `x`
is set to be the second item in the set. This repeats until `x` has been every
item in the set and the loop's code has run for each item. Also, just like in
the first form, `x` only exists within the loop, so don't count on using it in
other places.

Examples:

`for i=1, 10:
	print i`

will print "123456789"

`for i in [1,2,5,5,3,2,8]:
	print i`

will print "1255328"

Errors
======

No doubt you've heard of the horrors of "bugs" in the code, but once you
understand how bugs occur, it isn't so hard to deal with them. When you boil it
down, bugs can happen due to only three reasons. The first reason is when the
code you wrote doesn't handle a certain situation, and so your program crashes
or exhibits unexpected behaviour. These kinds of bugs are generally easy to deal
with. All you have to do is navigate to the portion of code that handles the
situation and add the necessary code. The other two cases result because of
errors.

There are two types of errors: syntax errors and semantic errors. A syntax error
is when you type code that doesn't follow the rules of the programming language.
These types of errors can range from not providing enough arguments to a
function or forgetting to add punctuation to a line of code. Semantic errors are
when there is nothing _syntactically_ wrong with your code, but you type code that
doesn't do what you intended it to do. This could be something like saying
`a * b` when you meant to say `a * c`. It's still technically correct, but your
program will behave differently than you expected it to.

Your program will always crash when a syntax error occurs, but it isn't
guaranteed to crash when a semantic error occurs ( although that's possible.) If
you _expect_ an error to occur, however, then many languages have ways to catch
an error and keep it from crashing your program. Although this might seem like a
useful thing, it's always better to write error-free code when possible. Since
so many errors are possible, suppressing an error from crashing your program
could lead you down any number of different paths where your program's state is
unpredictable.

Language
========

All right, now most of what I said above is true, but almost all of it is
simplified. I did this mostly because for now it doesn't really matter if you
know how these things work, just that you know they exist. The more practical
thing now is to choose a language to learn. As I stated earlier, languages are
what allow us to write easy to read code and still expect the computer to
understand us. There are very many languages and just like human language, many
of them are related to each other. That means there are similarities between
certain languages, and because they all are interfaces through which to talk to
the CPU, all programming languages have some commonalities. However, for the
sake of time, I'll go ahead and give you a shortlist of the most popular
languages (these aren't official by any means and in no particular order):

-C
-C++
-Python
-Java
-JavaScript
-Ruby

And then some other really popular ones:

-C#
-Go
-Haskell
-Erlang
-PHP
-Lua
-Prolog
-Fortran

Beyond these, the number of people actively using them drops off pretty quickly.
All the time, you'll hear someone mention a new language that's great at this or
that, but many of them come and go. You might have noticed that I didn't include
HTML or XML or any markup language in these lists. This is just because they're
markup languages, and are relatively "useless" (that is, they don't have very
many affects on the computer, and are really just a bunch of information instead
of a set of instructions.)

Starting out, I highly recommend the C++ Python combo. This is a very powerful
duo because most industry standards are C++, and Python is very quick for
prototyping. Python is also good enough for full on projects and has a mind
numbing number of extensions to use.

Another good duo is C C++. C is one of the lower level languages (it's not
_that_ low though,) and provides tons of power. The tradeoff is that it's a bit
less forgiving to learn and code, and there aren't as many cool libraries (
libraries are like bits of code other people have written to to a certain task
so that you don't have to.) Luckily C is very well documented, so it just takes
a bit of patience and some trial and error.

My favourite duo is C Lua. Lua is very much like Python from a code standpoint.
It's very easy to write and making prototypes can be very quick. It isn't nearly
as popular as Python, and so it doesn't have the vast number of libraries that
Python does, but it does have it's fair share. The other neat thing about Lua
is that with a little bit of work, you can write C code (which tends to run
faster and can be more powerful) and then use that code directly in Lua just as
if it was Lua code. This is very useful for increasing performance or if you
need access to a C library that doesn't have a Lua version. Actually... Python
can even do something like this, but it's a little different and not quite as
smooth.

I've been saying "powerful" and this really just means how much the language can
manipulate the system. This usually has to do with managing memory or making
"system calls" to the operating system. Don't worry about "power" too much for
now, because all of those languages in the list above are pretty "powerful."

For what it's worth, when I get into the game dev stuff from now on, I'll be
using Lua. If I switch languages, I'll tell you.

One last note: if I could only learn one language, it would have to be Python.
It's everywhere, from the web to super computers. Pretty much everyone speaks it
so it's like the English of computer science.