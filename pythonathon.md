What Even
=========

Some of us are born to python, some rise to python, and others have python thrust upon 'em. Let's learn you a python.

This document assumes you've seen computer programming before, but tries to be kind in how it is paced. Everything here is for Python 3.

A note about Abstraction
------------------------

In some sense, the two core actions of computer programming are *abstraction* and *naming*. That is: we're going to try and make code that expresses an idea; we have to give that code and its constituents clear and meaningful names. This is, I think, a tricky idea to get your head all the way around without thorough exposure. My intention is that this document will point out some places where we abstract ourselves from something so the ideas sink in well.

Types
=====

We've briefly covered the notion of a type. Python offers us some foundational types to work with:

| Type    | Specification                          | Example              |
|---------|----------------------------------------|----------------------|
| int     | Integer; effectively unlimited size    | 1, 5, 12,487,129,420 |
| float   | Double-precision floating point number | 0.219, 50.6          |
| complex | Complex numbers                        | 2i                   |
| bool    | Boolean                                | True/False           |
| str     | String                                 | 'cat', 'house boat'  |

Python is a *strongly, dynamically typed* language. This means we almost never have to care about what the type of a thing is when we declare or receive it, but we *cannot* use types interchangeably in some contexts. For instance:

``` example
>>> 2 + 2
4
>>> 'cat' + 'dog'
'catdog'
>>> 2 + 'dog'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

Between ints, `+` means "addition"; between strings, it means "concatenation". But between an int and a string, python cannot and will not guess what `+` means, and throws a type error. We must "cast", changing the type of one operand to match the other, so that python knows how to `+` everything together correctly:

``` example
>>> str(2) + 'dog'
'2dog'
```

Identifiers
===========

Ok, so we're going to name things. In python, we name things by giving them an *identifier*. A valid identifier in python follows these rules:

1.  It can be any combination of upper and lowercase letters, numbers, and the `_` character.
2.  It must start with a letter.

So, `my_swe3t_l33t_IdEnTiFi3r` is valid (but don't ever do that); `3rd_item` is not.

Python usually follows these conventions:

1.  Identifiers used for variables are in *snake case*: all lower-case letters with words separated by the underscore character. E.G. `a_variable_named_foo`
2.  Identifiers for classes are in *title case*: each word with its first letter capitalized, no spaces or underscores. E.G. `MyFooClass`

Statements
==========

Python code is made up of *statements*. A statement can be a whoooole lot of things. A statement might be variable assignment, or creating a function. Simply listing a type or an object *isn't* a statement.

So, in an interpreter:

``` example
>>> 5     # not a statement
5
>>> x = 5 # statement
```

Variables
=========

Variable assignment is one of the most standard features a programming language can have. In python, variable assignment is as simple as can be:

``` python
x = 5
print(x)
```

Put another way: we're binding the *value* 5 to the *identifier* x. We can bind any value we want to any valid identifier this way.

Now: it's important that you understand that there is a thing called *scope*, which affects when and how variables can be accessed. We're going to get to *scope* soon, but we need a few more ideas before we can fully explain it.

Reserved Words
==============

Before we get too far, there's a thing about Python you should know -- which is a thing that's true of many programming languages, so it's useful to be clear on. This is the notion of *reserved words*. It goes like this:

When we write code, we express to a computer what we want it to do. The language we use to express ourselves is our programming language. That language has some syntax, made of words and symbols, that allows us to get our ideas and intentions written down. Certain words and symbols are baked in to the language, very deeply -- their meaning cannot be changed by us, and we have to respect and use these words only in very specific ways.

(*Nota bene*: in python, "reserved words" are typically referred to as "keywords." Same idea, slightly different name.)

What this means in practice is that we *cannot use a reserved word as an identifier*. For instance:

``` python
False = 5  # NOPE
import = 7 # SUPER NOPE
```

The python keywords are: `False`, `class`, `finally`, `is`, `return`, `None`, `continue`, `for`, `lambda`, `try`, `True`, `def`, `from`, `nonlocal`, `while`, `and`, `del`, `global`, `not`, `with`, `as`, `elif`, `if`, `or`, `yield`, `assert`, `else`, `import`, `pass`, `break`, `except`, `in`, `raise`

We will get in to what most of these do as we work through this document! Hang in there.

Boolean comparisons
===================

Let's say we want to make a logical statement about the comparison of two values. If we're dealing with numbers, python provides a set of built-in operators to help us do precisely this. We can explore this in the python interpreter:

``` example
>>> 5 < 6
True
>>> 1 > 100
False
```

Note our first two keywords: `True` and `False`.

Python also supports greater-than-or-equal to, so:

``` example
>>> 5 >= 9
False
>>> 9 >= 9
True
```

Or we can test equality:

``` example
>>> 10 == 10
True
```

Common in many languages, exclamation point captures the idea of negation in a symbol. So, "not equal" is written:

``` example
>>> 4 != 5
True
>>> 4 != 4
False
```

Python also provides the keyword `not`, which, as with `!`, negates any Boolean expression following it:

``` example
>>> not True
False
>>> not 4 == 5
True
```

Note that python also has nice English keywords for Boolean operators: `and` and `or`:

``` example
>>> False or True
True
>>> False and False
False
>>> False and True
False
>>> True and True
True
```

Equality versus Identity
------------------------

Along with equality operators (e.g. `==`), python provides an *identity* operator. While extremely useful, the identity operator can also lead to some very subtle bugs. This is in part because the identity operator is `is`, and thus has a much more natural language syntax than `==`. However, observe:

``` example
>>> a = 19998989890
>>> b = 19998989889 + 1
>>> a == b
True
>>> a is b
False
```

*Equality* compares the *value* of two things; *identity* checks to see if two things are literally the same object in memory.

As a general rule, `is` can always be used to compare with `True`, `False`, and `None`. This is because these three values (all keywords, notice) are *singleton objects* -- there is only one `True` object, ever, period, so equality and identity are effectively interchangeable. For more complex kinds of values, it's often better to stick to `==`. Thus:

``` example
>>> x = True
>>> x is True
True
>>> x is not False
True
>>> y = 10
>>> y == 10
True
```

Control Flow
============

If we have a notion of Boolean values and truthiness, we can now decide to change the way our program works based on some Boolean condition. This is called `control flow`, and it is very nice.

The single most common control flow structure is the `if / else` block. Python elides the common `else if` phrase in to `elif`, for no reason in particular.

``` python
x = 5

if x > 10:
    print('X is greater than 10!')
elif x == 10:
    print('X is exactly 10')
else:
    print('X must be less than ten')
```

These checks can get quite complex:

``` python
if x < 5 or y is 'cow':
    print('woah')
elif (x is 5 and y is 5 and z is 5) or skip_the_fives:
    print('okay double woah')
else:
    print('whew')
```

A thing to notice: instead of doing an explicit comparison, we can use the *Truthiness* of a term directly:

``` python
if 5:
    print('it must be 5')
```

Seen slightly less frequently, but still fairly common, is the `while` construct, which loops "while" some term is truthy:

``` python
x = 0
while x < 10:
    print(x)
    x = x + 1
```

Note two things:

1.  If `x` weren't mutated, the loop would loop forever.
2.  You can use a `while` loop to loop forever, on purpose.

\#2 is not uncommonly seen for the "main loop" of a program. That is: if we \#consider a computer "program" to be a thing that sits idle until some action \#occurs, then goes back to being idle, we could express that idea like so:

``` example
while True:
    if check_for_user_input():
        respond_appropriately()
```

Truthiness
----------

Python has a broad notion of what we often call "truthiness". That is: certain values are *implicitly* considered to be roughly equivalent to `True` or `False` when used in control flow expressions.

So:

Truthy Values are
-   `True`
-   Any string with length greater than 0
-   All numbers
-   All non-empty collections
-   Most object instances (we'll get in to what this is in a little bit)

Falsy Values are
-   `False`
-   Empty string
-   Empty collections
-   `None`

We use them like:

``` python
a_list = []

if not a_list:
    print('it is empty!')
else:
    print('it is full')
```

Or:

``` python
full_string = 'this is a string'
empty_string = ''

if full_string:
    print('there was some string!')

if empty_string:
    print('you should be surprised if this prints')
```

Collections
===========

A "collection" is, as the name implies, a kind of container or group of Things. Python comes with four main collection types built-in; in practice, we use two of them vastly more than the others. For every collection, python provides a *literal* syntax, which is a shorthand way of creating a new collection.

**Note**: all collections in python are *zero indexed*. This means that the very first element in a collection is the 0 element, the second is the 1 element, etc. This takes a little getting used to, but is also very common.

Also note: all python collections are *heterogeneous* -- they can contain Things of any combination of types, including other collections.

Tuples
------

A tuple is an immutable, and usually small, collection. It is used to group together a small number of things we implicitly assert are related to one another. The tuple literal is a set of parens `()`. We access the elements of a tuple by their index.

``` python
x = ('cat', 'dog', 'phone')
print(x[0])
print(x[1])
print(x[2])
```

Note a python oddity: to make a single-element tuple, a comma is needed after the first element -- e.g. `('cat',)`.

Lists
-----

A `list` is one of the data structures we interact with alllllll the time in python. We can make a list with the `list` function, but it's more common to do it with the list literal, which is a set of square braces `[]`.

Lists are ordered and mutable. We access the elements of a list by their index.

``` python
a_list = [5, False, 'gazpacho']

print(a_list[2])
```

Dicts
-----

A `dict` captures the notion of key-value pairs in python; the name is short for *dictionary*, which gives us a very good hit about its use. `Dicts` offer us *very fast* lookup of elements. There is a `dict` function, but we more commonly use the curly-brace literal, `{}`, with the internal format keyname, colon, space, value of key (E.G. `{name_of_key: value}`.)

The key of a `dict` is typically a string, but sometimes, tuples or integers are used.[^1]

We access a list of the keys in a `dict` using an instance[^2] method called `keys()`. We access values by the name of their key. Like so:

``` python
the_dict = {'googoo': 'cachoo',
            'hocus': 'pocus',
            'Marlon': 'Brando'}

print(the_dict.keys())
print(the_dict['hocus'])
```

Sets
----

A set is a very handy data type with a special property: *every element of the set is guaranteed unique*. Sets are, thus, used for uniquing, and for maintaining collections of unique elements. You can use the `set` function, or you can use the set literal, which is, slightly confusingly, also curly braces `{}`. (If there are no colons inside the braces, python knows it's a `set`, not a `dict.`)

When you create a set, all of the elements will be uniqued correctly. This is done by... wait for it... hashing each element, which means each element in a set must be hashable.

``` python
list_with_duplicates = [1, 1, 1, 2, 2, 3, 3, 3, 3, 3, 4, 5, 5, 5, 5, 5, 5]

the_set = set(list_with_duplicates)

print(the_set)
```

For those of you with a math bent, you might be thinking, "I wonder if we can take the union, difference, and intersection of Python's sets?" Good news! You absolutely can. The interface is exposed as instance methods on a given set.

``` python
first_set = {1, 2, 3}
second_set = {3, 4, 5}

# The union of two sets is all the unique elements of both sets together in one
print(first_set.union(second_set))

# The intersection is only those elements found in both sets
print(first_set.intersection(second_set))

# The difference is all the elements from the calling set not found in the
# argument set -- in this case, all the elements in first_set not found in
# second_set
print(first_set.difference(second_set))
```

Iteration and Comprehension
===========================

Collections can do a lot of handy things for us. It is, for instance, awfully useful to be able to group like units of stuff together. A common example of this is a settings file, which can be loaded in to your application as a `dict`. Wanna know the value of a setting? If all your settings are in a `dict`, you can access them by key. Easy peasy.

Another very common use case is the need to take some action of every Thing inside a collection. Python supports this through the `for` construct, like this:

``` python
a_list = [1, 2, 3, 4, 5]

for number in a_list:
    print(number * number)
```

`number` is an arbitrary name I chose; you can pick any valid python identifier here, so pick something descriptive for what's in your list.

So, how does python know what kinds of things can be used in a `for` loop? The answer is: much as anything with a `__hash__` method is hashable, anything with an `__iter__` method is iterable. (We'll cover this more when we go over *magic methods*.) In practice: all of the core python collection types -- *tuples*, *lists*, *dicts*, and *sets* -- are iterable.

The cagey observer might wonder: *what does it mean to iterate over a dict?* Great question. To control what we get when we iterate over a dict, we have several approaches:

``` python
demo_dict = {'first_key': 'first_value',
             'second_key': 'second_value',
             'third_key': 'third_value'}

# Iterating only the keys can be done two ways:
for key in demo_dict.keys():
    print(key)

# Iterating over the keys is also the "default" behavior if no method is
# called:
for key in demo_dict:
    print(key)

# But maybe you'd rather iterate over the values!
for value in demo_dict.values():
    print(value)

# Or maybe you want, wait for it, BOTH AT ONCE:
for key, value in demo_dict.items():
    print('The key: ' + str(key) + ' maps to value: ' + str(value))
```

This last example uses a technique we haven't talked about called *Tuple Destructuring*, which we will get to Soon™.

One last handy trick: sometimes you want to know the index of each value as you iterate. Observe!

``` python
a_list = ['cat', 'dog', 'butter']

tpl = '{} has index {}'
for idx, item in enumerate(a_list):
    strang = tpl.format(item, idx)
    print(strang)
```

(I've slipped in an early first example of python's *String Formatting* system. We'll get in to it more later!)

Comprehensions
--------------

Python has a rich and very powerful faculty called *comprehensions*, which combine the notion of iteration and collection creation in to a single tidy syntax.

Consider a contrived example: let's take all the numbers between 0 and 50, square them, and return only those numbers divisible by 2. We'll do this first with a `for` loop:

``` python
res = []

for i in range(0, 50):
    squared = i * i
    if squared % 2 == 0:
        res.append(squared)

print(res)
```

We're using a technique here called an *accumulator* -- as we go, when we find a number we want to keep, we keep it by appending it on to `res`, which we then return.

Or, we could write it like this:

``` python
print([i * i for i in range(0, 50) if (i * i) % 2 == 0])
```

Blam. Same result, but *much* shorter. Comprehensions allow us to create a new collection by iterating over any iterable; we can optionally filter as we go.

We can iterate two things at once:

``` python
print([(x, y) for x in ['a', 'b', 'c'] for y in [1, 2, 3]])
```

(Note that we generate *all combinations*, not just `[('a', 1), ('b', 2), ('c',
3)]`)

There are also comprehensions for other collection types. We can create a dict, from our earlier example, in which the key is the original number and the value is the square:

``` python
print({i : i * i for i in range(0, 50) if i * i % 2 == 0})
```

&lt;3 comprehensions. So good! Do note, however, that as a comprehension grows longer and more complex, it becomes less and less of a good idea. If you find you're packing a **lot** of logic in to a comprehension, consider switching back to a plain, easy to read for-loop.

Functions
=========

We've got a **ton** to work with so far. Heck -- we could write some pretty complex python scripts with just what we've done so far. We've got the notion of storing a thing to a variable; we've got the notion of a collection, a group of Things. The next item on our agenda is my personal favorite: the function.

Functions are created using the keyword `def`, like this:

``` python
def do_nothing():
    """
    An optional docstring
    """
    pass
```

So here's a function that... does nothing. (Our next keyword, `pass`, is the noop keyword -- pass means, "just keep on steppin'".) Sure? Check it out: it's time for our first real taste of *abstraction*. Say we want to multiply numbers by two, and we want to use functions. We could do it like this:

``` python
def one_times_two():
    return 1 * 2

def two_times_two():
    return 2 * 2

def three_times_two():
    return 3 * 2

def four_times_two():
    return 4 * 2
```

Perhaps you can see how quickly this will fall apart. It's functional, but not *practical*. We can do better. Let's make our function take an argument:

``` python
def times_two(integer):
    return integer * 2
```

We now have a function that takes *some argument* and returns that argument multiplied by two. Is this a super trivial example? Well, yes. And: it's also an easy demonstration. We are *abstracting* the notion of multiplying by two. By using a function argument, we can now multiply really anything by two! It's a small abstraction, but the idea is important -- the function is both a little more generic and a little more specialized.

The `return` keyword
--------------------

Most of the time, a function should be called and the give back some *value*. We do this, in most cases, with the `return` keyword.[^3] We can `return` multiple times, or not at all. Like so:

``` python
def check_out_this_x(x):
    if x > 500:
        return 'It is a biggish X'
    elif x < 250:
        return 'I guess it could be a kinda big X but probably it is not'
```

Let's think this through. If X is 600, we'll get back the string "It is a biggish X" -- all well and good. If X is, say, 5, we'll get back the second, much longer string. And if X is 300? What then?

Answer: we'll get back `None`. Any function which doesn't specify an explicit `return` returns `None`.

(Also notice: we didn't specify an `else` for our `if` block. This is poor form ;-P The correct way to write this function would be to explicitly return `None` from and `else`).

Docstrings
----------

Docstrings are optional, but great. Why are they great? One, using [Sphinx](http://www.sphinx-doc.org/en/stable/), you can generate very nice online documentation that includes your docstrings. For a great example of this, have a look at the documentation for an operations tool called [Fabric](http://www.fabfile.org). Here's a page of [clean, compiled documentation](http://docs.fabfile.org/en/1.13/api/core/context_managers.html); here is the [source code that generated the docs](https://github.com/fabric/fabric/blob/master/fabric/context_managers.py). Pretty cool, eh?

The other thing we can do is learn about functions and classes from inside the python interpreter. For instance, say you wanna know about the `len` function:

``` example
>>> help(len)
Help on built-in function len in module __builtin__:

len(...)
    len(object) -> integer

    Return the number of items of a sequence or collection.
```

Good stuff, eh?

Default Arguments
-----------------

Here's a trick I love: what if you *usually* want an argument to always have the same value, but *sometimes* you wanna change it?

``` python
def usually_multiply_by_two(integer, mult_by=2):
    return integer * mult_by
```

This function can be called as `usually_multiply_by_two(5)`, or it can be called with a second argument, which will then be used -- `usually_multiply_by_two(5, 5)` will return 25, not 10.

Now, a thing to pay attention to: if a function has multiple optional arguments, you can either specify them positionally, or using the name, but don't do both.

That is:

``` python
def multiple_optionals(foo=5, bar=6, baz=10, blep=123):
    tpl = """
    I was called with:
    - foo  = {foo}
    - bar  = {bar}
    - baz  = {baz}
    - blep = {blep}
    """

    return tpl.format(foo=foo, bar=bar, baz=baz, blep=blep)

print(multiple_optionals('hi', 'cow'))

# But, if I only want to change the value of baz:

print(multiple_optionals(baz='Cowabunga'))
```

Also note: it is a syntax error to list optional arguments before required arguments in a function:

``` python
# Do this:
def foo(bar, baz=None):
    pass

# Not this! No no no!
def foo(baz=None, bar):
    pass
```

`*args` and `**kwargs`
----------------------

Especially if you look at really any python documentation, you're gonna see a pattern over and over that will throw you off the first few times, like this:

``` python
def foo(bar, *args, **kwargs):
    pass
```

`args` and `kwargs` are a little weird at first, but they do cool things, and unlock cool powers. Let's dig in.

Both `args` and `kwargs` are for times when you aren't sure in advance what aruments your function will need to take. `args` is used when you aren't sure how many arguments there will be; `kwargs` is a dict containing any unspecified keyword arguments to your function. Let's see this in action:

``` python
def so_many_args(foo, bar, baz, *args, **kwargs):
    tpl = "The {}, the {}, and the {}".format(foo, bar, baz)
    print(tpl)
    print(args)
    print(kwargs)

so_many_args('this', 'that', 'the other')

so_many_args('hi', 'hi', 'hi', 'hi', 'hi', 'hi', 'hi!') # so man 'hi's!

so_many_args('hi', 'hi', 'hi', TheFroz='kazoo', Spork='nugget')
```

So our function arguments foo, bar, and baz are assigned the first three values; `*args` winds up with the rest -- thus we see it empty in the first invocation, but with four "hi"s in the second. `**kwargs` is empty in invocation one and two because we have no unexpected named arguments. In invocation three, we have no extra positional args, but we do have two spare keyword args.

If we truly don't care how many Things are handed to a function, we could use `*args` on its own and be done with is:

``` python
def add_em_up(*nums):
    res = 0
    for num in nums:
        res = res + num

    return res

print(add_em_up(1, 2, 3, 4, 5, 6, 7, 123))
```

**Plot twist**: I changed the name of `*args` to `*nums`! "args" and "kwargs" are names based *purely on convention*. Like any convention, you should both use it most of the time *and* feel free to bend it when it stops making sense.

Back to `**kwargs`, what about this:

``` python
def foo(**kwargs):
    tpl = '\t-{} with val {}'
    print('Hello! I was called with:')

    for key, val in kwargs.items():
        print(tpl.format(key, val))

foo(panda='panda', another_panda='yep it is another panda')
```

So this is nice and also completely terrible. On the one hand, this is *very* powerful -- we can write functions the effects of which we cannot even predict! On the other hand: we can write functions the effects of which we cannot even predict :/

Think of it another way: argument names to functions are themselves documentation. If you encounter a function called `save_an_item_to_a_database(item, database)`, you can form a pretty clear intuition about what that function *does*. On the other hand, a function called `save_an_item_to_a_database(**kwargs)` is... uh. What... do you give it? Now imagine that function has no docstring. Now imagine yourself with a migraine. Yeaaaaaaah.

These are good powers, but don't abuse them, yeah?

A last heckin' sweet use for \* and \*\*
----------------------------------------

`*` and `**` have a last cool use that kicks in when we use them to call functions. `*` can "explode" a list, turning it in to positional arguments in a function call; `**` can break apart a dict, matching the keywords inside it to named arguments of the function.

Whew, okay, that sounds weird. Let's see it in practice.

First `*`:

``` python
three_things = ['foo', 'bar', 'baz']

def print_three_things(first, second, third):
    print(first)
    print(second)
    print(third)

print_three_things(*three_things)
```

Each item has been "slotted in" to the function. Oooh!

Now `**`:

``` python
a_dict = {'foo': 'Hello from the foo!',
          'bar': 'The bar also says hello!'}

def print_a_dict(foo='Nope', bar='Also nope'):
    print(foo)
    print(bar)

print_a_dict(**a_dict)
```

Say it with me: ooooh! aaaaah!

Lambdas
-------

`lambda` is the python keyword for an *anonymous function*. Effectively, a lambda is kind of a magic instant throw-away function. To be honest, this technique isn't used super frequently in python outside of python's (somewhat limited) functional programming interface, which looks like this:

Say I want to multiply every number in a list by 7. Voila:

``` python
the_list = [1, 2, 3, 4, 5]

res = map(lambda x: x * 7, the_list)

print(res)
```

`map` takes a function and a list, and returns a new list that is the result of calling the function on every element of the input list. It is exactly equivalent to:

``` python
def times_seven(x):
    return x * 7

the_list = [1, 2, 3, 4, 5]

res = [times_seven(i) for i in the_list]

print(res)
```

Note that our `lambda` implicitly returns -- we don't use the `return` keyword.

What else are lambdas good for? Well, think a little more about what we just saw. We passed a lambda as the first argument to the `map` function! Neat! In python, functions are "first class" values, meaning they can be used anywhere, say, 5 can be used -- we can store a function to a variable, we can pass a function to another function as an argument, and we can return a function from a function. Here's a slightly less contrived use for a `lambda` using python's *String Formatting* system. We'll talk about it more in depth in a bit, but here's the salient points:

-   Curly braces in a string get replaced by arguments to `String.format`
-   If there's a name inside the curly brace, it becomes a keyword arg -- e.g., `Hi
       there, {name}` should be called with `format(name='Bartholomew')`.

``` python
def make_dict_formatter(template):
    return lambda the_dict: template.format(**the_dict)

one_template = 'The baz: {baz} The blep: {blep}'

a_dict = {'baz': 'I am the baz!', 'blep': 'I am the blep!'}

the_formatter = make_dict_formatter(one_template)

formatted_string = the_formatter(a_dict)

print(formatted_string)
```

Scope
=====

There's a little bit of a subtle shenanigan going on in our `make_dict_formatter` example; let's dig in to that. To get our heads around it, though, we need to understand the idea of *scope*. Let's consider:

``` python
assertion = 'Cats are mortal, Aristotle was mortal, therefore Aristotle was a cat.'

def how_about():
    print(assertion)


how_about()


def but_then():
    assertion = 'That whole Aristotle-cat thing is a syllogism.'
    correctly = "Cats are mortal, Aristotle was mortal, go home syllogisms, you're drunk."
    print(assertion)


but_then()
print(assertion)
print(correctly)
```

So, we start with an assertion. We call `how_about`. What happens?

Next, we define a function `but_then` that *also* defines an `assertion`. What value does it print?

Finally, we attempt to print the value of `correctly`. What happens?

What we're dealing with here is the question of *scope*, which is to say, "when does One Thing in a programming language have access to a particular set of variables and when doesn't it?" There is a *lot* more to say on this topic than we have time for. We're going to spend like four sentences on the theory behind what's going on, and then we're going straight to the pragmatics.

What's happening here on a theoretical level goes like this: python is *statically scoped* (this is the most "normal" kind of scoping you can have if you are a modern programming language). Further, it has *lexical* scope.

Static scope
as opposed to *dynamic* scope. In a statically scoped program, we know the values of our symbols at compile/interpretation time. In a *dynamically* scoped language, we don't know until *runtime*. (Note that this is **not** the same thing as, though it is analogous to, python being dynamically *typed*.)

Lexical scope
a subset of static scope, lexical scoping means that we have certain kinds of semantic blocks of code which create their own scope. The most important, and most common, example of this is functions, which always create their own scope, but which also always *inherit from the parent scope*.

Whew. Okay. Let's do that again, but in a much more pragmatic way:

First, we define `assertion`. `assertion` is in our "global" scope -- it is at the "top level" of the code snippet. It isn't inside a function or any other kind of lexical block -- it's just *there*.

Next, we define `how_about`. `how_about` creates a new scope, but it inherits from the parent scope -- so it has access to our "global" `assertion`. Great.

Now we define `but_then`. `but_then` *also* defines an `assertion`, and its `assertion` "wins", seamlessly overwriting the "global" value, but *only inside the function block*. We confirm this by calling `but_then`, and then immediately checking the value of `assertion`.

Finally, we attempt to access the value of `correctly` from inside the `but_then` function. We get an error, because the inheritance of scope goes one-way -- `but_then` inherits the parent scope, but the parent scope is unaltered.

Scope is a subtle, but important point -- it allows us to do things like safely re-use common variable names inside functions, and to not have our functions "leak", mutating the world outside of their intended purview.

Closures
--------

So, what's going on with our `make_dict_formatter` function? We're using scope to our advantage with a technique called a *closure*. `template` is an argument to the parent `make_dict_formatter` function; it is then available inside the body of a new function. Here -- it might be easier to see like this:

``` python
def make_dict_formatter(template):
    def formatter(the_dict):
        return template.format(**the_dict)

    return formatter
```

We open a new scope with `make_dict_formatter`, then we open *another* new scope with our inner function `formatter` (a lambda behaves identically, but never receives a name). The `formatter` function has access to `template` from its parent scope, but the `template` variable never leaks -- we have provided a private configuration to a function.

`global`
--------

Now, back to our `assertion` example. Sometimes, it *can* be handy to modify global state from inside a function. To this end, python provides the `global` keyword. We use it like this:

``` python
a_global = 'shazango'

def change_global(new_val):
    global a_global
    a_global = new_val


print(a_global)
change_global('woopwoop')
print(a_global)
```

Inside our function, we tell python, "we don't want to create a new local variable, we want the same variable we inherited from the main scope." Pow.

Classes
=======

Functions are how me model actions -- verbs, if you will -- in programming. Classes, then, are how we model nouns. Yes, there are gray areas -- nouns can sometimes take actions -- but as we'll see, they do that by having access to their own functions (verbs).

To really grok classes, we need to take a moment to understand *instances*. If a class models a noun, an *instance* represents an actual one of that noun. So for example: there is a class called `Dict`. When we make a dict using `{}` syntax, we are *instantiating* a new *instance* of the `Dict` class. The `Dict` class is *general*, the pattern on which all dicts are based; our instance is specific. We create instances either using normal-looking functions (as with the `dict()` method), or using a specialized kind of function called a *constructor*. Using a constructor looks like this:

``` example
foo = Foo()
```

To define a new class in python we use -- wait for it -- the `class` keyword:

``` python
class Fruit():
    """
    I am a model of a fruit!
    """

    carbon_based = True

    def __init__(self, name, taste, color, climate):
        """
        The constructor of new fruit!
        """
        self.name = name
        self.taste = taste
        self.color = color
        self.climate = climate

    def which(self):
        """
        I will print the name of this fruit!
        """
        print('I am a {}!'.format(self.name))
```

Let's take this a piece at a time. First, we declare our class and give it a name. By python convention, our class name will be in TitleCase -- in this instance, `Fruit`. The open-and-close parens following the name deal with *Inheritance*, which we'll get to next -- for now, just note we aren't inheriting anything here.

Next, we can, optionally, provide a docstring (always a good idea). And now: as many statements as we feel like making. We'll make three -- our assignment of `carbon_based` and two functions. **Terminology alert**: when a function belongs to a class, we call it a *method*.

Before we go much further, it'll help to see this in action:

``` example
>>> banana = Fruit('banana', 'awful', 'yellow', 'somewhere too hot')
>>> banana.carbon_based
True
>>> banana.taste
'awful'
>>> banana.which()
I am a banana!
```

So: we instantiate a new `Fruit` by calling its constructor, which is called... `Fruit()`. We give it arguments, which become part of our class instance (we'll explore the mechanism for this in just a moment, hang in there.)

From here, we can see that our statements have become part of our class instance. `carbon_based` is, as we'd expect, set to `True`. We set properties like `self.taste`, and now we can access them. We also have access to the `which` method, which tells us our instance is a banana. Great.

Static vs. Instance
-------------------

Now lets look at something:

``` example
>>> Fruit.carbon_based
True
>>> Fruit.name
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: class Fruit has no attribute 'name'
```

When we use the `Fruit` class directly, we can access the `carbon_based` property, but *not* the `name` property. What do?

The answer is in the difference between *static* and *instance* properties. `carbon_based = True` is a statement we make at the class level, and it becomes a *static* property of the class -- which means we can access it directly on the class definition. On the other hand, `name` is only assigned when we create an instance, and is thus not available on the class. We'll see a similar, but slightly more confusing, error if we try to call the `which` method on the class:

``` example
>>> Fruit.which()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unbound method which() must be called with Fruit instance as first argument (got nothing instead)
```

Note that the function signature of both `__init__` and `which` begin with the keyword `self`. `self` is a reference to the current instance, and in python, an instance method is defined by taking a `self` reference as its first argument.

Which brings us to: our constructor, `__init__`!

Constructors
------------

`__init__` is a python "magic method"; it identifies a special kind of function called a *constructor*. Constructors are used to create class instances. So, when we define an `__init__` method on a class, we have the power to specify exactly how that class gets created. Are properties set? Methods called? Songs sung? Only we get to say.

An `__init__` method can do anything to the `self` reference it wants to, but do be wary that *you are still creating the object*. For instance, this will asplode:

``` python
class OhNo():
    def __init__(self):
        self.beep = self.boop()

    def boop(self):
        return self.beep
```

``` example
>>> uh_oh = OhNo()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/Users/gastove/Code/pythonathon/pythonathon.org[*Org Src pythonathon.org[ python ]*]", line 3, in __init__
  File "/Users/gastove/Code/pythonathon/pythonathon.org[*Org Src pythonathon.org[ python ]*]", line 6, in boop
AttributeError: OhNo instance has no attribute 'beep'
```

We reference `self.beep` before it is given a value! Sad day.

Inheritance
-----------

"Inheritance" is a common design pattern in modern object oriented languages. It can be single or multiple; python is the latter, and we'll explore the ramifications of that *next*.

Inheritance works like this:

Imagine we're trying to create classes to model different kinds of vehicles. We could do it a buuuunch of different ways. Here's one:

``` python
class Car():
    wheels = 4
    has_engine = True

    def __init__(self, top_speed):
        self.top_speed = top_speed


class Motorcycle():
    wheels = 2
    has_engine = True

    def __init__(self, top_speed):
        self.top_speed = top_speed


class Bicycle():
    wheels = 2
    has_engine = False

    def __init__(self, top_speed):
        self.top_speed = top_speed
```

Hopefully, this smells a little funny to you. We're repeating ourselves a looooooot. Everything has the same init method! Properties are repeated! Erg. You know what we need? A way to abstract over the idea of a set of nouns in a hierarchy with shared properties.

Behold, inheritance:

``` python
class Vehicle():
    wheels = 0
    has_engine = True

    def __init__(self, top_speed):
        self.top_speed = top_speed


class Car(Vehicle):
    wheels = 4


class TwoWheeledVehicle(Vehicle):
    wheels = 2


class Motorcycle(TwoWheeledVehicle):
    pass


class Bicycle(TwoWheeledVehicle):
    has_engine = False
```

Woooooooah. What even is this. Let's investigate:

First we define a base `Vehicle`, which captures all the ideas we need to describe A Vehicle. Next, we define a `Car` -- the syntax `Car(Vehicle)` means that `Car` is *inheriting* from `Vehicle`. (This is often called an "is-a" relationship -- `Car` is-a `Vehicle`.[^4])

In our `Car` class, *all we do is specify the number of wheels*. Everything else is inherited from the parent, or *base*, class, including all methods. When we go to create a car, the `__init__` method from `Vehicle` will be called. Neat, eh?

Now we derive a class for `TwoWheeledVehicle`, and we derive two variants of it. A `Motorcycle` doesn't need to change anything at all -- two wheels, has engine, an init from the base class -- `Motorcycle` is all set. `Bicycle` just needs to set `has_engine` to `False`.

*Boom*.

Multiple Inheritance
--------------------

Python technically supports a property called "multiple inheritance." Mostly, this is very bad news, because it can be *very* confusing. You've already seen this in action, in our `http-demo`:

``` python
Base = declarative_base()


class IdPrimaryKeyMixin(object):
    id = Column(Integer, primary_key=True)


class DateTimeMixin(object):
    created_on = Column(DateTime, default=datetime.now)
    updated_on = Column(DateTime, default=datetime.now, onupdate=datetime.now)


class Person(Base, IdPrimaryKeyMixin, DateTimeMixin):
    __tablename__ = 'people'

    first_name = Column(String(20), nullable=False)
    last_name = Column(String(30), nullable=False)

    def __repr__(self):
        tpl = 'Person<id: {id}, {first_name} {last_name}>'
        formatted = tpl.format(id=self.id, first_name=self.first_name,
                               last_name=self.last_name)

        return formatted
```

Note: in Python 2, we had to explicitly inherit from `object` in order to make a correct, new object -- in Python 3, we don't have to do this.

So -- we make a set of classes labeled as `Mixins`, because you'd never instantiate them directly -- they're only useful to add Extra Properties to another class.[^5] Now, the `Person` class has an `id` property and both `created_on` and `updated_on` properties -- clean and tidy.

This can get really weird:

``` python
class Beep():
    def sound(self):
        return self.beep


class BeepPrinter():
    def print_beep(self):
        return 'I go: ' + self.sound()


class BeepBooper(Beep, BeepPrinter):
    def oh_no(self):
        print(self.print_beep())
```

``` example
>>> b = BeepBooper()
>>> b.oh_no()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/Users/gastove/Code/pythonathon/pythonathon.org[*Org Src pythonathon.org[ python ]*]", line 13, in oh_no
  File "/Users/gastove/Code/pythonathon/pythonathon.org[*Org Src pythonathon.org[ python ]*]", line 8, in print_beep
  File "/Users/gastove/Code/pythonathon/pythonathon.org[*Org Src pythonathon.org[ python ]*]", line 3, in sound
AttributeError: BeepBooper instance has no attribute 'beep'
```

In this example, the bug is that none of the three classes define a `beep` property. But which one should? Where is the bug? As the class hierarchy grows larger, this problem gets worse and worse and worse. Be careful of it!

Exceptions
==========

You've almost certainly hit exceptions before. Exceptions are how python -- and many, many other languages -- think about *errors* and error handling. They very often have the word "error" or "exception" in the name. For instance, in our discussion of *Multiple Inheritance*, we encountered an `AttributeError`, which happens when you attempt to access an atribute of an object that doesn't exist.

Language: exceptions are either *raised* or *thrown* when they are created, and *caught* when they are received within code. An exception *doesn't necessarily have to crash your program*, but it often will, and should. To handle exceptions, python uses the (very common) notion of a *try* block, which is created with the keyword -- wait for it -- `try`.

First, an uncaught exception:

``` python
def crasher():
    raise RuntimeError()

crasher()
```

This simply wont run -- it just asplodes every time. Which is, in all honesty, not a bad thing to have happen with an exception. A very common thing to need to do, however, is to provide some kind of output about the exception and take some form of emergency action -- exiting with an appropriate status code, for instance. For this, we can use a `try`:

``` python
def crasher():
    raise RuntimeError('OH YEAH!')

def elegant_crasher():
    try:
        crasher()
    except RuntimeError as e:
        print("Oh no.")
        raise e

elegant_crasher()
```

There's a series of things to note here. First, we can have as many `except` clauses as we like, each handling a different exception or set of exceptions -- we can also have a final catch-all that handles any exceptions we didn't think of. Also note that we can provide helpful error messages when we raise exceptions -- this is a very good practice indeed. Nothing ruins a day quite like hitting some garbage like:

``` example
IncomprehensibleException: a bad is there. No I don't know where. Stop asking.
```

Just to give a clear example of handling Lots of Bads, we could have something like:

``` python
def foo(arg):
    try:
        db_conn = db.get_connection()
        db.query(arg)
    except ConnectionError:
        print('Arg, failed to connect to the db')
        return None
    except ValueError, KeyError:  # This'll catch either of these errors
        print('DB failed to find what we need somehow for arg {}'.format(arg))
    except Exception as e:  # This case catches anything we haven't anticipated
        print('There was a bad!')
        print(e)
```

Now, let's imagine that there is, in fact, no exception! In that case, our `try` block skips straight over the `except` clauses.

A Thing To Seriously Avoid
--------------------------

Exceptions and error-handling are very real parts of programming in most languages. And, there are better and worse ways to use them. The very worst is a thing called "control flow by exception". The question you should ask yourself is: "am I using a try/catch block like an if/else?" If you are: stop and reconsider your choices.

Tuple Destructuring
===================

Here's a handy trick: python functions can return multiple values, which python can then "unpack" in to multiple variables.

``` python
def return_many():
    return 'cat', 'dog', 'horse'


first_thing, second_thing, third_thing = return_many()

print(first_thing)
print(third_thing)
```

String Formatting
=================

Python's docs refer to the string formatting system as a "mini language". This is... not great news. The docs aren't great either. Or rather -- they're so abstruse as to be nearly useless.

So, point the first: for a handy string format reference, check out <https://pyformat.info/>

The string format method lets us do a lot of handy stuff. Here's a short once-over:

``` python
print('Format fills in {} with {}'.format('curly braces', 'words'))
```

``` python
print('Words can be {verb} into position using {modifier} arguments; the {modifier} arguments can be repeated'.format(modifier='named or keyword', verb='put'))
```

``` python
print('Places can also be {0} and used as {1} args, even repeated so long as they are {0}'.format('numbered', 'positional'))
```

Need to print actual {}s? Escape them with a second set of {}:

``` python
print('Here are some curly braces: {{}}. Also, here is a {}'.format('cow.'))
```

String formatting can format damn near anything -- it's seriously ridiculously powerful. Which also means I have to always look it up. You might too. Remember: <https://pyformat.info>. Good stuff.

A closing example: formatting long numbers with thousands-place commas:

``` python
print('{:,}'.format(1239085830383))
```

wow

Context Managers
================

Context managers are a clean way of expressing this pattern:

``` python
open_file = open(path, 'r')

lines_of_file = open_file.readlines()

open_file.close()
```

We have some resource -- a file, a database, a URL -- which we want to open, interact with, and then close. To provide for this, python provides a mechanism called a *context manager*, and they are neat as heck. Context managers use the keyword `with`, and have the general form `with resource_name`; optionally, you can bind your new resource to an alias using `as alias`. It looks like this:

``` python
with open(file_path, 'r') as file_handle:
    lines = file_handle.readlines()
```

Python will handle making sure our resource is closed when execution leaves the `with` block.

Pythonisms and "magic methods"
==============================

We've seen a lot of things wrapped in "double underbars" -- often written *dunderbars* -- go by. Dunderbars are used to denote identifiers and method names of special significance to python itself. These methods, sometimes called "magic methods", are part of the neat internal glue that makes python work coherently. Many of the magic methods, as the name suggests, are attached to classes. For instance, `__init__` is a special method that tells python how to construct a new instance of a class.

Let's look at the `__str__` and `__repr__` methods with a motivating example. Imagine we have this class, and try to "see" it with two different kinds of printing:

``` python
class PrintingDemo:
    name = "The Printing Demo"

demo = PrintingDemo()

print(demo)
print('{!r}'.format(demo))
```

Blah! Both useless. When we print it, implicitly casting to string, we get the memory address of the instance; when we try to format it using its `__repr__` method, we... still just get the memory address of the instance. We can fix this:

``` python
class PrintingDemo:
    name = "The Printing Demo"

    def __str__(self):
        return 'Hello, my name is {name}'.format(name=self.name)

    def __repr__(self):
        return '<PrintingDemo name={name}>'.format(name=self.name)

demo = PrintingDemo()

print(demo)
print('{!r}'.format(demo))
```

Much better.

What if we want to know if two `PrintingDemo` objects are the same?

``` python
class PrintingDemo:
    name = "The Printing Demo"

    def __str__(self):
        return 'Hello, my name is {name}'.format(name=self.name)

    def __repr__(self):
        return '<PrintingDemo name={name}>'.format(name=self.name)


demo1 = PrintingDemo()
demo2 = PrintingDemo()

print(demo1 == demo2)
```

Right now, all python can do is glance at the memory address and say, "different addresses, different objects, not equal". We can fix it by defining the `__eq__` and `__ne__` methods:

``` python
class PrintingDemo:
    name = "The Printing Demo"

    def __str__(self):
        return 'Hello, my name is {name}'.format(name=self.name)

    def __repr__(self):
        return '<PrintingDemo name={name}>'.format(name=self.name)

    def __eq__(self, other):
        return self.name == other.name

    def __ne__(self, other):
        return not self.__eq__(other)

demo1 = PrintingDemo()
demo2 = PrintingDemo()

print(demo1 == demo2)
```

Yis.

There are... a **lot** of magic methods. As a general rule, if you think, "how do I define &lt;behavior&gt; for my class", the answer is often a magic method. For instance, here's a very very partial list:

| Method       | Purpose                                            |
|--------------|----------------------------------------------------|
| ****item**** | Handles things like dict\[key\] retrieval          |
| ****lt****   | "less than" operator behavior                      |
| ****gt****   | "greater than" operator behavior                   |
| ****add****  | plus operator behavior                             |
| ****and****  | Boolean `and` behavior                             |
| ****or****   | Boolean `or` behavior                              |
| ****call**** | Allows a class instance to be called as a function |

Run magics: the "if main" and `__main__.py`
-------------------------------------------

Imagine you have a directory full of code and you want to run it as a single Thing. We can do this with a `__main__.py` file, which tells python, "if this directory gets given to you to run, here's how to do it." We've actually seen this already, in passing, in `http-demo`. It has a `__main__.py` that looks like this:

``` bash
cat http-demo/__main__.py
```

:

``` example
import main
```

:

``` example
main.app.run()
```

``` example
#!/usr/bin/env python

import main

main.app.run()
```

Our `__main__.py` is found by python and is executed; it in turn imports and runs the main method of our app.

We can achieve this in scripts using an "if main" statement, which looks like this:

``` python
if __name__ == '__main__':
    do_the_thing()
```

A statement like that at the bottom of a file tells python how to run that file. Neat!

Generators
==========

Python has a mechanism you should know about but might not use for a while. The mechanism is called *generators*. Let's consider a motivating problem.

Say you wanna count all the lines in a file that have the word "http" in them. Our file -- we'll call it `somefile.txt` -- is small. The regular approach would look like this:

``` python
path = '/path/to/somefile.txt'

with open(path, 'r') as h:
    lines = h.readlines()
    matching = [line for line in lines if 'http' in line]

print(len(matching))
```

This approach works by reading the entire file in to memory, then counting all the lines. This works just great for small files. In fact, it works great as long as the file is small enough to fit in to RAM.

Now, what if the file is 46 gigabytes? We almost certainly don't have that much RAM. What now?

What if we could efficiently check one line at a time without ever pulling the whole file in to memory? Generators are for exactly this.

A generator is a special kind of function using the keyword `yield` instead of `return`. Python sees this keyword and converts the function in to a generator. A generator is like a list we can only read once; on every iteration, python calls the function, retrieving the next item.

It looks like this:

``` python
path = '/path/to/somefile.txt'

def line_reader():
    with open(path, 'r') as h:
        yield h.readline()

matching = [line for line in line_reader() if 'http' in line]
```

Generators take some work to get our brains around, but they are good when data gets big.

...in fact, they are so good that they are built in to the python file API ;-P You can actually solve the above like so:

``` python
path = '/path/to/somefile.txt'

with open(path, 'r') as h:
    matching = [line for line in h]
```

Decorators
==========

Decorators are not likely to be something you'll use a lot any time soon -- but they come up, and you'll see them out in the world, so you should know what they are. (The place where you're most likely to find them is during testing, particularly with the `py.test` library.)

First note: decorators are a design pattern you'll see in more languages than just Python -- Ruby, in particular, leaps to mind.

A decorator is an example of a *higher-order* function. A higher-order function takes a function as one of its arguments. In the decorator pattern, we define a function which we use to "decorate" some number of others, augmenting them with some Extra Behavior. In Python, we do this by defining out decorator, and then using an `@` when we define the function it should "decorate."

Here's a 100% contrived example:

``` python
def call_with_5(func):

    def new_func(*args, **kwargs):
        new_args = args + (5,)
        func(*new_args, **kwargs)
    return new_func

@call_with_5
def foo(*args, **kwargs):
    print(args)
    print(kwargs)


@call_with_5
def bar(the_cow, *args):
    print(the_cow)
    if args:
        print(args)


foo(arg='blerp')
bar('here is the cow')
```

OK so, definitely not the most useful example, but it demonstrates the machinery, which is a combination of many of the elements we've seen:

1.  We define a higher-order function, which will take the function we wanna decorate and return a new function with the new behavior.
2.  We use `*args` and `**kwargs`, because we don't know in advance what arguments our function will be called with -- and we'd rather not care.

We can decorate any number of functions. A decorator captures the notion of wrapping an existing function in a new behavior.

Now that we've seen the parts, let's consider a vastly more useful example. Say we're writing an application, and we know there exist a set of functions so important that we want to be emailed if they have any problems. Check it out:

``` python
def email_me_if_it_breaks(func):
    def responder(*args, **kwargs):
        try:
            func(*args, **kwags)
        except Exception as e:
            email_me(e)


@email_me_if_it_breaks
def super_important_func_one():
    did_it_work = do_the_super_important_thing()

    if not did_it_work:
        raise RuntimeError('It did not work')
    else:
        return did_it_work
```

Any function wrapped like this will email us! Woot. Woot? Woot.

Imports and Modules
===================

Let's say you're writing a script that will manipulate many paths to files. You think to yourself, "ah, I know that python has an excellent standard library". You find that there is a thing called `os` which contains a bunch of path utilities in a thing called `path`. Good start.

Let's get some clearer terminology. `os` is a module. Within `os` is another module called `path`. If we want to use it in our code, we can use the keyword `import`. We can do this a lot of different ways. Lets clarify our example like this: inside the `path` module is a function called `join`, which will correctly join elements together with slashes between them to form a valid file path, like this:

``` example
>>> path.join('/Users', 'gastove', 'Documents')
'/Users/gastove/Documents'
```

Let's look at all the ways we can import the `join` function.

First, we can import `os` and fully qualify the whole name:

``` python
import os

joined = os.path.join('/Users', 'gastove', 'Documents')
print(joined)
```

That's great, but a bit clunky. We can use `from ... import` syntax to bring just the `path` module in to scope:

``` python
from os import path

joined = path.join('/Users', 'gastove', 'Documents')
print(joined)
```

Also great. If we're really sure we only want the `join` function, we can import only it using the same syntax:

``` python
from os.path import join

joined = join('/Users', 'gastove', 'Documents')
print(joined)
```

Imagine we've already got a function called `join`, and we don't want the names to collide. We can alias anything we import using `as`:

``` python
from os.path import join as path_join

joined = path_join('/Users', 'gastove', 'Documents')
print(joined)
```

Perhaps we actually want to import several things? We can do that too. As the list gets longer, it's much easier to read if we use a set of parens and some newlines:

``` python
from os.path import (
    abspath as absolute_path,
    exists,
    expanduser
)
```

Modules
-------

Okay so: we can import things. Good! `os` is part of the python standard library. But what if we want to import code we wrote ourselves? What then?

The rules go like this:

First: if two files are in the same directory, one can import from another

If we have a file, `/tmp/demo/one.py`:

``` python
def foo():
    return 'foo'
```

And a second file, `/tmp/demo/two.py`:

``` python
import one

print(one.foo())
```

We're all set -- nothing special need me done.

Imagine now, however, we have a directory we want to put files in, `/tmp/demo/baz/`. To be able to import from the `baz` directory, we must make it in to a module. Don't worry! Making a module is not hard. We simply add a file named `__init__.py` to the directory that should now be importable. Our demonstration dirs should now look like this:

``` bash
tree /tmp/demo
```

We can now import `baz` in to `one.py` and `two.py`.

### Controlling visibility with `__init__.py` files

So: we've got these `__init__.py` files all over the place. They tell python a module is there; what else? Do they *do* anything?

It turns out: yes! `__init__.py` files control what Things in our modules get exposed, and how. Imagine we have a file called `song.py` in a directory called `song`, and it contains this:

``` python
class Song():
    def __init__(self, lyrics, score):
        """
        I am the singiest song
        """
        self.lyrics = lyrics
        self.score = score


def sing_a_song(song):
    print(song.lyrics)
```

If it's in a module with an empty `__init__.py`, we would import things like this:

``` python
from song.song import sing_a_song, Song
```

Directory name, file name, Thing (function or class) name.

Feels a little redundant, right? We could add this to our `__init__.py`:

``` python
from song import Song, sing_a_song
```

And now, we could do the import elsewhere like so:

``` python
from song import Song, sing_a_song
```

Shorter! Tidier! Also: optional. But good to know it's there.

Relative and Absolute Imports
-----------------------------

Imagine you have a project shaped a little like this:

``` bash
tree /tmp/demo
```

What if we want to import code from `scoot.py` into `poot.py`? Python provides two approaches you'll encounter: relative imports and absolute imports.

**Absolute imports** are based on where you'll eventually be *running the code from*. That is, if we will eventually be running a command in our terminal like `python
demo`, then we could think of imports as having `demo` as the root, and we import from there, like this:

``` python
# We are in poot.py
from demo.module_one import scoot
```

The other approach you'll see is **relative** imports. These will look very much like relative file paths, because in some sense, they are:

``` python
# We are in poot.py
from ../module_two import scoot
```

My usual habit is this: if I'm importing one module in to the other, I use absolute imports. If I'm importing one file within the same module in to another, or a submodule in the same dir, I use a relative import. For instance: if we are in `module_one/__init__.py`, our imports could look like this:

``` python
import scoot
import module_three as m3
from demo.module_two import groot, poot
```

Project Structure
=================

Let's have another look at your friend and mine, `http-demo`:

``` bash
tree -L 2
```

This is a pretty standard python project setup. It has an unusual number of requirements.txt files -- a habit of mine, because I like separating things. It's also missing a testing dir. The truly prototypical setup would look like this:

``` bash
tree -L 2
```

Now it has a `test` dir at the correct level, and the requirements files are just a little tidier, kept together in a dir.

[1] The key of a `dict` can be any *hashable* type. What types are hashable, you ask? Well: any of the primitive types, as well as any class defining the `__hash__` trait. Overwhelmingly, the most common thing to use as the key of a `dict` is a string. But note: we can also use a `tuple`, as long as all the elements inside are themselves hashable.

[2] We'll cover instance methods in *Classes*.

[3] We'll cover the exception to this when we talk about *Generators*

[4] Note however that is-a relationships are importantly one-way -- a `Vehicle` is **not** a `Car`.

[5] Multiple inheritance is an attempt to solve the same problem languages like Java solve with a technique called *interfaces*. Alas: interfaces are vastly superior. So it goes.
