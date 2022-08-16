Just Enough Ruby
================

Experienced Rails developers debate whether beginners should study Ruby
before learning Rails.

By all means, if you love the precision and order of programming
languages, dive into the study of Ruby from the beginning. But most
people don't delay starting Rails while learning Ruby; realistically,
you'll retain more knowledge of Ruby if you learn it as you build things
in Rails. That is the approach we've taken in this book. You've already
built a simple Rails application and used Ruby as you did so.

Reading Knowledge of Ruby
-------------------------

What you need, more than anything, when you start working with Rails, is
reading knowledge of Ruby.

With a reading knowledge of Ruby you'll avoid feeling overwhelmed or
lost when you encounter code examples or work through a tutorial. Later,
as you tackle complex projects and write original code, you'll need to
know enough of the Ruby language to implement the features you need. But
as a student, you'll be following tutorials that give you all the Ruby
you need. Your job is to recognize the language keywords and use the
correct syntax when you type Ruby code in your text editor.

To that end, this chapter will review the Ruby keywords and syntax
you've already learned. And you'll extend your knowledge so you'll be
prepared for the Ruby you'll encounter in upcoming chapters.

Ruby Example
------------

To improve your reading knowledge of Ruby, we'll work with an example
file that contains a variety of Ruby expressions.

We won't use this file in our tutorial application, so you'll delete it
at the end of this chapter. But we'll approach it as real Ruby code, so
make a file and copy the code using your text editor.

First we have to consider where the file should go. It will not be a
model, view, controller, or any other standard component of Rails. Rails
has a place for miscellaneous files that don't fit in the Rails API.
We'll create the file in the **lib/** folder. That's the folder you'll
use for any supporting Ruby code that doesn't fit elsewhere in the Rails
framework.

Create a file **lib/example.rb**:


```ruby
class Example < Object

  # This is a comment.

  attr_accessor :honorific
  attr_accessor :name
  attr_accessor :date

  def initialize(name,date)
    @name = name
    @date = date.nil? ? Date.today : date
  end

  def backwards_name
    @name.reverse
  end

  def to_s
    @name
  end

  def titled_name
    @honorific ||= 'Esteemed'
    titled_name = "#{@honorific} #{@name}"
  end

  def december_birthdays
    born_in_december = [ ]
    famous_birthdays.each do |name, date|
      if date.month == 12
        born_in_december << name
      end
    end
    born_in_december
  end

  private

  def famous_birthdays
    birthdays = {
      'Ludwig van Beethoven' => Date.new(1770,12,16),
      'Dave Brubeck' => Date.new(1920,12,6),
      'Buddy Holly' => Date.new(1936,9,7),
      'Keith Richards' => Date.new(1943,12,18)
    }
  end

end
```

In some ways, this Ruby code is like a poem from Lewis Carroll:


```html
'Twas brillig, and the slithy toves
Did gyre and gimble in the wabe;
All mimsy were the borogoves,
And the mome raths outgrabe.

"Beware the Jabberwock, my son!
The jaws that bite, the claws that catch!
Beware the Jubjub bird, and shun
The frumious Bandersnatch!"
```

The poem corresponds to the rules of English syntax but is nonsense.

The code follows the rules of Ruby syntax, and unlike the poem, uses
meaningful words. But it is unclear how the author intends anyone to use
the code. If you're beginning a career as a Rails developer, this won't
be the last time you look at code and wonder what the author was
intending. In this case, I just want to give you some code that
illustrates typical Ruby syntax and structure.

Ruby Keywords
-------------

When reading Ruby code, the first challenge is determining which words
are Ruby keywords and which were made up by the developer. Code is only
strings of characters. But some strings have special meaning for
everyone and all others are arbitrary words that only have meaning to an
individual developer.

As you gain experience, you'll recognize Ruby keywords because you've
seen them before.

You'll also recognize a developer's made-up words because of their
position relative to other words and symbols. Some made-up words will be
obvious because they are just too idiosyncratic to be part of the Ruby
language. For example, you'll rightly guess that `myapp` or `fluffycat`
are not part of the Ruby language.

If you're reading a Lewis Carroll poem, you could look up words in a
dictionary to see if you find them.

There is only one way to be sure which words are part of the Ruby
language: Check the Ruby API.

As an exercise, pick one of the words from the example code that you
think might be a Ruby keyword and search the API to find it.

If you want to be a diligent student, you can check every keyword in the
example code to find out whether it is in the Ruby API. It is more
practical to learn to recognize Ruby keywords, which we'll do next.

### API Documentation

The Ruby API documentation lists every keyword in the language:

-   [ruby-doc.org](http://ruby-doc.org/) - the official Ruby API
-   [apidock.com/ruby](http://apidock.com/ruby) - Ruby API docs with usage notes

Ruby Files
----------

When we write code, we save it in files. We've added our miscellaneous
example file to the **lib/** folder.

By convention, Ruby files end with the file extension **.rb**.

### Using IRB

In the "Troubleshooting" chapter, you used IRB (the Interactive Ruby
Shell) to try out Ruby code. You can use IRB to try out the example code
in the console.


```console
$ irb
>> load 'lib/example.rb'
=> true
>>  require 'date'
=> true
>> ex = Example.new('Daniel',nil)
=> #<Example:0x007fb46c9eecd8 @name="Daniel", @date=#<Date: 2015-12-23 ...
>> list = ex.december_birthdays
=> ["Ludwig van Beethoven", "Dave Brubeck", "Keith Richards"]
>>
```

Entering the `load` directive and the filename brings the code into IRB.

The `require 'date'` statement loads the Ruby date library.

The statement `ex = Example.new('Daniel',nil)` creates an object from
the `Example` class.

The `ex.december_birthdays` method returns an array of names.

Remember you can use Control-d to exit from IRB.

Now, for practice, we'll read the Ruby code.

Whitespace and Line Endings
---------------------------

Whitespace characters such as spaces and tabs are generally ignored in
Ruby code, except when they are included in strings. There are several
special cases where whitespace is significant in Ruby expressions but
you are not likely to encounter these cases as a beginning Rails
developer.

Some programming languages (Java and the C family) require a semicolon
as a terminator character at the end of statements. Ruby does not
require a semicolon to terminate a statement. Instead, if the Ruby code
on a line is a complete expression, the line ending signifies the end of
the statement. If the line ends with a `+` or other operator, or a
backslash character, the statement is split into multiple lines.

Comments
--------

Ruby ignores everything that is marked as a comment. Use comments for
notes to yourself or other programmers.


```ruby
  # This is a comment.
```

You can also turn code into comments if you don't want the code to run.
This is a common trick when you want to "turn off" some part of your
code but you don't want to delete it just yet, because you are trying
out alternatives.

The Heart of Programming
------------------------

Three principles are at the heart of all programming:

-   syntax
-   conditional execution
-   transformation

Computers allow no ambiguity. Code must exactly follow the *syntax* of a
language. Typos, guesses, and code that is almost-but-not-quite right
will simply fail, often without any helpful error messages.

Computers seem intelligent because they can execute code
*conditionally*. You can write a program so that given one set of
conditions, certain parts of the code will execute, and given different
conditions, other parts of the code will execute.

Lastly, programs are written to transform abstractions from one form to
another. That's why computer programs look like math. When we learn
simple arithmetic, we learn we can take the symbols for numbers and add
them together to make a different number. Computer programs do more than
add numbers; a program can transform words and other abstractions.

Assignment
----------

In Ruby, like many other programming languages, the equals sign
indicates we are *assigning* a value.


```ruby
  name = 'Foobar Kadigan'
```

Assignment is the first step to transformation. Here `'Foobar Kadigan'`
is a string of letters. The equals sign is the assignment operator. And
`name` is a *variable* that stores the value so it can be easily reused.
We don't have to type `'Foobar Kadigan'` every time we need a name; we
can use `name` instead.

Just as we can assign a value to a variable, we can reassign a new value
whenever we want. That is why we call them variables; the value can
vary.


```ruby
  name = 'Mr. Foobar Kadigan'
```

Variables can be assigned strings of letters, numbers, or anything else.
"Anything else" is very broad because we can use Ruby to make complex
structures that contain data and also "do work." These complex
structures are *objects* and we say that Ruby is *object-oriented*
because it is easy to work with objects in Ruby.

Object-Oriented Terminology
---------------------------

Software architects use a common vocabulary to talk about programming
languages:

-   **class**
-   **instance** or **object**
-   **method**
-   **attribute** or **property**
-   **inheritance**
-   **class hierarchy**

There are three ways to learn what these words mean. You can memorize
the definitions. You can write code and intuitively grasp the meanings.
Or you can gain an understanding by applying metaphors.

### Houses

For example, some programming textbooks attempt to explain a *class*
like this: A blueprint for a house design is like a *class definition*.
All the houses built from that blueprint are *objects* of a class we
could call House.

### Vehicles

Or: The concept of "vehicle" is like a *class*. Vehicles can have
*attributes*, like color or number of doors. They have behavior, or
*methods*, like buttons that turn on lights or honk a horn. The concepts
of "truck" or "car" are also classes, *inheriting* common
characteristics from a *superclass* "vehicle." The blue car in your
driveway with four doors is an object, a particular *instance* of the
class "car."

### Cookies

I like the cookie metaphor the best.

A *class definition* is like a cookie cutter.

Bits in the computer memory are like cookie dough.

The cookie cutter makes as many individual cookies as you want. Each
cookie is an *instance* of the Cookie class, with the same shape and
size as the others. Cookies are *objects*.

You can decorate each cookie with sprinkles, which are *attributes* that
are unique to each instance. Some cookies get red sprinkles, some get
green, but the shape remains the same.

Running a program is like baking. The cookies change state from raw to
cooked.

Sticking a toothpick in a cookie is like calling a *method*. The method
returns a result that tells you about the state: Is it done?

### Limitations of Metaphors

Metaphors are imperfect.

If baking was like running a program, all the cookies would disappear as
soon as the oven was turned off.

When a software program contains a "car" model, it doesn't fully model
cars in the physical world. It represents an abstraction of
characteristics a programmer deems significant. Let's make a model for a
Person that contains an attribute Gender. What values are possible for
the attribute Gender? For many years, Facebook offered two choices, male
and female. In 2014, Facebook suddenly offered a choice of over fifty
gender terms. As Sarah Mei discusses in a blog post, [Why Gender is a
Text Field on
Diaspora](http://www.sarahmei.com/blog/2010/11/26/disalienation/), your
assumptions have consequences when you build a model.

Most classes in software APIs don't model anything in the real world.
They typically represent an abstraction, like an Array or a Hash, which
inherits characteristics from another abstraction, for example, a
Collection.

Given the limitations of metaphors, maybe it is easier to simply say
that software allows us to create abstractions that are "made real" and
then manipulated and transformed. Terminology such as *class* and
*instance* describe the abstractions and the relationships among them.

### Definitions

Here are definitions for some of the terms we encounter when we consider
Rails from the perspective of a software architect:

**class**
:   an abstraction that encapsulates data and behavior

**class definition**
:   written code that describes a class

**instance** or **object**
:   a unique copy of a class that exists only while a program is running

**inheritance**
:   a way to make a class by borrowing from another class

**class hierarchy**
:   classes that are related by inheritance

**method**
:   a command that returns data from an object

**attribute** or **property**
:   data that can be set or retrieved from the object

**variable**
:   a name that can be assigned a value or object

**expression** or **statement**
:   any combination of variables, classes, and methods that returns a
result

Some of these terms are abstractions that are "made real" in the Ruby
API (such as class and method); others are just terms that describe
code, much like we use terms such as "adjective" or "noun" to talk about
the grammar of the English spoken language.

Classes
-------

You don't have to create classes to program in Ruby. If you only write
simple programs, you won't need classes. Classes are used to organize
your code and make your software more modular. For the software
architect, classes make it possible to create a structure for complex
software programs. To use Rails, you'll use the classes and methods that
are defined in the Rails API.

There is one class at the apex of the Ruby class hierarchy:
[`BasicObject`](http://www.ruby-doc.org/core-2.4.1/BasicObject.html).
`BasicObject` is a very simple class, with almost no methods of its own.
The [`Object`](http://ruby-doc.org/core-2.4.1/Object.html) class
inherits from `BasicObject`. All classes in the Ruby and Rails APIs
inherit behavior from `Object`. `Object` provides basic methods such as
`nil?` and `to_s` ("to string") for every class that inherits from
`Object`.

We create a class `Example` and inherit from `Object` with the `<`
"inherits from" operator:


```ruby
class Example < Object
.
.
.
end
```

The `end` statement indicates all the preceding code is part of the
`Example` class.

In Ruby, all classes inherit from the Object class, so we don't need to
explicitly *subclass* from `Object` as we do here. The example just
shows it for teaching purposes.

Here is the `Example` class without the explicit subclassing from
`Object`:


```ruby
class Example
.
.
.
end
```

Much of the art of programming is knowing what classes are available in
the API and deciding when to subclass to inherit useful methods.

Methods
-------

Classes give organization and structure to a program. Methods get the
work done.

Any class can have methods. Methods are a series of expressions that
return a result (a value). We say methods describe the class behavior.

A method definition begins with the keyword `def` and (predictably) ends
with `end`.


```ruby
  def backwards_name
    @name.reverse
  end
```

Initializing the object and calling the method returns a result:


```ruby
ex = Example.new('Daniel',nil)
my_backwards_name = ex.backwards_name
  => leinaD
```

We can also *override* a method from the parent class.


```ruby
  def to_s
    @name
  end
```

Here we are *overriding* the `to_s` ("to string") method from the parent
`Object` class.

Ordinarily, the `to_s` method returns the object's class name and an
object id. Here we will return the string assigned to the variable
`@name`.

Most times you won't override the `to_s` ("to string") method. This
example shows how you can override any method inherited from a parent
class.

Dot Operator
------------

The "dot" is the method operator. This tiny punctuation symbol is a
powerful operator in Ruby.

It allows us to *call a method* to get a result.

Sometimes we say we *send a message* to the object when we invoke a
method, implying the object will send a result.

Some classes, such as `Date`, provide *class methods* which can be
called directly on the class without instantiating it first. For
example, you can run this in the Rails console:


```ruby
Date.today
 => Tue, 15 Oct 2013
```

More often, methods are called on variables which are instances of a
class. For example:


```ruby
birthdate = Date.new(1990, 12, 22)
 => Sat, 22 Dec 1990
birthmonth = birthdate.month
 => 12
```

We can apply *method chaining* to objects. For example, `String` has
methods `reverse` and `upcase` (among many others). We could write:


```ruby
nonsense = 'foobar'
 => "foobar"
reversed = nonsense.reverse
 => "raboof"
capitalized = reversed.upcase
 => "RABOOF"
```

It is easier to use method chaining and write:


```ruby
'foobar'.reverse.upcase
 => "RABOOF"
```

Classes create a structure for our software programs and methods do all
the work.

### Question and Exclamation Methods

You'll see question marks and exclamation points (sometimes called the
"bang" character) used in method names. These characters are simply a
naming convention for Ruby methods.

The question mark indicates the method will return a *boolean value*
(true or false).

The bang character indicates the method is "dangerous." In some cases it
means the method will change the object rather just return a result. In
Rails an exclamation point often means the method will throw an
exception on failure rather than failing silently.

Initialize Method
-----------------

Objects are created from classes before they are used. As I suggested
earlier, class definitions are cookie cutters; the Ruby interpreter uses
them to cut cookies. When we call the `new` method, we press the cookie
cutter into the dough and get a new object. All the cookies will have
the same shape but they can be decorated differently, by sprinkling
attributes of different values.

The `initialize` method is one of the ways we sprinkle attributes on our
cookie.


```ruby
  def initialize(name,date)
```

When we want to use an `Example` object and assign it to a variable, we
will instantiate it with `Example.new(name,date)`. The `new` method
calls the `initialize` method automatically. If we don't define an
`initialize` method, the `new` method still works, inherited from
`Object`, so we can always instantiate any class.

Method Parameters
-----------------

Methods are useful when they operate on data.

If we want to send data to a method, we define the method and indicate
it will accept *parameters*. Parameters are placeholders for data
values. The values that are passed to a method are *arguments*.
"Parameters" are empty placeholders and "arguments" are the actual
values. In practice, "parameters" and "arguments" are terms that are
used interchangeably and not many developers will notice if you mix up
the terms.

Our `initialize` method takes `name` and `date` arguments:


```ruby
  def initialize(name,date)
```

Ruby is clever with method parameters. You can define a method and
specify default values for parameters. You can also pass extra arguments
to a method if you define a method that allows optional parameters. This
makes methods very flexible.

We separate our parameters with commas. For readability, we enclose our
list of parameters in parentheses. In Ruby, parentheses are always
optional but they often improve readability.

Variable
--------

In Ruby, everything is an object. We can assign any object to a
variable. The variable works like an alias. We can use a variable
anywhere as if it were the assigned object. The variable can be assigned
a string, a numeric value, or an instance of any class (all are
objects).


```ruby
  name
```

You can assign a new value to a variable anywhere in your method. You
can assign a different kind of object if you want. You can take away
someone's name and give them a number. We can create a variable
`player`, assign it the string `'Jackie Robinson'`, replace the value
with an integer `42`, or even a date such as `Date.new(1947,4,15)`.

### Symbol

Obviously, we see many symbols when we read Ruby code, such as
punctuation marks and alphanumeric characters. But *symbol* has a
specific meaning in Ruby. It is like a variable, but it can only be
assigned a value once. After the initial assignment, it is *immutable*;
it cannot be changed.

You will recognize a symbol by the colon that is always the first
character.


```ruby
  :name
```

Symbols are efficient and fast because the Ruby interpreter doesn't have
to work to check their current values.

You'll often see symbols used in Rails where you might expect a
variable.

Attributes
----------

In an object, methods do the work and data is stored as variables. We
can use the `initialize` method to input data to the object. We can't
access data in variables from outside the object unless it is exposed as
*attributes*.

Classes can have attributes, which we can "set" and "get." That is, we
can establish a value for an attribute and retrieve the value by
specifying the attribute name.

Attributes are a convenient way to push data to an object and pull it
out later.

In Ruby, attributes are also called properties.

Here we use the `attr_accessor` directive to specify that we want to
expose `honorific`, `name` and `date` attributes.


```ruby
  attr_accessor :honorific
  attr_accessor :name
  attr_accessor :date
```

If we use `attr_accessor` to establish attributes, we can use the
attribute names as methods. For example, we could write:


```ruby
 ex = Example.new('Daniel',nil)
 my_name = ex.name
```

In Ruby, attributes are just specialized methods that expose data
outside the object.

Instance Variable
-----------------

Inside an object, an ordinary variable only can be used within the
method in which it appears. If you use a variable with the same name in
two different methods, it will have a different value in each method.
The *scope* of a variable is limited to the method in which it is used.

Often you want a variable to be available throughout an instance, within
any method. You can declare an *instance variable* by using an
`@` (at) sign as the first character of the variable name.

The instance variable can be used by any method after the class is instantiated.

```ruby
@name = name
```

The values assigned to instance variables are unique for every instance
of the class. If you create multiple instances of a class, each will
have its own values for its instance variables. Here we create two
instances of the `Example` class. The `@name` instance variable will be
"Daniel" in the first instance and "Foobar" in the second instance.


```ruby
  ex1 = Example.new('Daniel',nil)
  ex2 = Example.new('Foobar',nil)
```

An instance variable is not visible outside the object in which it
appears; but when you create an `attr_accessor`, it creates an instance
variable and makes it accessible outside the object.

### Instance Variables in Rails

In a Rails controller, you'll often see a model assigned to an instance
variable. Earlier we saw `@owner = Owner.new` when we instantiated an
Owner model. We use an instance variable when we want a model to be
available to the view template.

Rails beginners learn the simple rule that you have to use the
`@` (at) sign if you want a variable to be available in the view.
Intermediate Rails developers learn that the variable with the `@`
(at) sign is called an instance variable and is only available within
the *scope* of the instance (practically speaking, to other methods in
the class definition). That leads to a question: Why is an instance
variable available inside a view?

There is a good reason. A Rails view is NOT a separate class. It is a
template and, under the hood, it is part of the current controller
object. From the viewpoint of a programmer, a Rails controller and a
view are separate files, segregated in separate folders. From the
viewpoint of a software architect, the controller is a single object
that evaluates the template code, so an instance variable can be used in
the view file.

This example shows us that the programmer and the software architect
have different perspectives on a Rails application. Understanding Rails
requires an integration of multiple points of view.

Double Bar Equals Operator
--------------------------

I've suggested that the best way to get help is to use Google or Stack
Overflow to look for answers. But that's difficult when you don't know
what symbols are called. Try googling "||=" and you'll get no results.
Instead, try googling "bar bar equals ruby" or "double pipe equals ruby"
and you'll find many explanations of the "or equals" operator. This is
an example of mysterious shorthand code you'll often find in Rails.

"||=" is used for conditional assignment. In this case, we only assign a
value to the variable if no value has been previously assigned.


```ruby
  @honorific ||= 'Esteemed'
```

It is equivalent to this conditional expression:


```ruby
  if not x
    x = y
  end
```

Conditional assignment is often used to assign a "default value" when no
other value has been assigned.

Conditional
-----------

Conditional logic is fundamental to programming. Our code is always a
path with many branches.

When the Ruby interpreter encounters an `if` keyword, it expects to find
an expression which evaluates as true or false (a *boolean*).

If the expression is true, the statements following the condition are
executed.

If the expression is false, any statements are ignored, unless there is
an `else`, in which case an alternative is executed.


```ruby
  if date.month == 12
    .
    .
    .
  end
```

Sometimes you'll see `unless` instead of `if`, which is a convenient way
of saying "execute the following if the condition is false."

In Ruby, the conditional expression can be a simple comparison, as
illustrated above with the `==` (double equals) operator. Or `if` can be
followed by a variable that has been assigned a boolean value. Or you
can call a method that returns a boolean result.

Ternary Operator
----------------

A basic conditional structure might look like this:


```ruby
  if date.nil?
    @date = Date.today
  else
    @date = date
  end
```

We test if `date` is undefined (nil). If nil, we assign today's date to
the instance variable `@date`. If `date` is already assigned a value, we
assign it to the instance variable `@date`. This is useful in the
`initialize(name,date)` method in our example code because we want to
set today's date as the default value for the instance variable `@date`
if the parameter `date` is nil.

Ruby developers like to keep their code tight and compact. So you'll see
a condensed version of this conditional structure often, particularly
when a default value must be assigned.

This compact conditional syntax is named the *ternary operator* because
it has three components. Here is the syntax:


```ruby
  condition ? value_if_true : value_if_false
```

Here is the ternary operator we use in our example code:


```ruby
  @date = date.nil? ? Date.today : date
```

This is another example of Ruby syntax that you must learn to recognize
by sight because it is difficult to interpret if you have never seen it
before.

For more Ruby code that has been condensed into obscurity, see an
article on [Ruby Golf](http://www.sitepoint.com/ruby-golf/). Ruby golf
is the sport of writing code that uses as few characters as possible.

Interpolation
-------------

Rubyists love to find special uses for orthography such as hashmarks and
curly braces. It seems Rubyists feel sorry for punctuation marks that
don't get much use in the English language and like to give them new
jobs.

We already know that we can assign a string to a variable:


```ruby
  name = 'Foobar Kadigan'
```

We can also perform "string addition" to concatenate strings. Here we
add an honorific, a space, and a name:


```ruby
  @honorific = 'Mr.'
  @name = 'Foobar Kadigan'
  titled_name = @honorific + ' ' + @name
  => "Mr. Foobar Kadigan"
```

Single quote marks indicate a string. In the example above, we enclose a
space character within quote marks so we add a space to our string.

You can eliminate the ungainly mix of plus signs, single quote marks,
and space characters in the example above.

Use double quote marks and you can perform *interpolation*, which gives
a new job to the hashmark and curly brace characters:


```ruby
  @honorific = 'Mr.'
  @name = 'Foobar Kadigan'
  titled_name = "#{@honorific} #{@name}"
  => "Mr. Foobar Kadigan"
```

The hashmark indicates any expression within the curly braces is to be
evaluated and returned as a string. This only works when you surround
the expression with double quote marks.

Interpolation is cryptic when you first encounter the syntax, but it
streamlines string concatenation.

Access Control
--------------

Any method you define will return a result.

Sometimes you want to create a method that only can be used by other
methods in the same class. This is common when you need a simple utility
method that is used by several other methods.

Any methods that follow the keyword `private` should only be used by
methods in the same class (or a subclass).


```ruby
  private
```

You often see private methods in Rails. Ruby provides a *protected*
keyword as well, but the difference between *protected* and *private* is
subtle and *protected* is seldom seen in Rails applications.

Hash
----

Our example code includes a private method named `famous_birthdays` that
returns a collection of names and birthdays of famous musicians.

Computers have always been calculation machines; they are just as
important in managing collections.

One important type of collection is named a Hash. A Hash is a data
structure that associates a key to some value. You retrieve the value
based upon its key. This construct is called a *dictionary*, an
*associative array*, or a *map* in other languages. You use the key to
"look up" a value, as you would look up a definition for a word in a
dictionary.

You'll recognize a Hash when you see curly braces (again, Rubyists give
a job to under-utilized punctuation marks).


```ruby
  birthdays = {
    'Ludwig van Beethoven' => Date.new(1770,12,16),
    'Dave Brubeck' => Date.new(1920,12,6),
    'Buddy Holly' => Date.new(1936,9,7),
    'Keith Richards' => Date.new(1943,12,18)
  }
```

Rubyists also like to create novel uses for mathematical symbols. The
combination of an `=` (equals) sign and `>`
(greater than) sign is called a *hashrocket*. The `=>`
(hashrocket) operator associates a key and value pair in a Hash. You'll often see
hashrockets in code written before Ruby 1.9. Ruby 1.9
introduced a new syntax using colons instead of hashrockets.

Whether with colons or hashrockets, you'll often see Hashes used in
Rails.

With Ruby 1.9 and later, here's how we associate key and value pairs in a
Hash:


```ruby
  birthdays = {
    beethoven: Date.new(1770,12,16),
    brubeck: Date.new(1920,12,6),
    holly: Date.new(1936,9,7),
    richards: Date.new(1943,12,18)
  }
```

Here, instead of using a string as the key, we are using Ruby symbols,
which enable faster processing. The `:` (colon) character associates the
key and value.

Ordinarily, a symbol is defined with a leading colon character. In a
Hash, a trailing colon makes a string into a symbol.

If you want to transform a string containing spaces into a symbol in a
Hash, you can do it, though the syntax is awkward:

```ruby
  birthdays = {
    'Ludwig van Beethoven': Date.new(1770,12,16)
  }
```

Array
-----

An *Array* is a list. Arrays can hold objects of any data type. In fact,
arrays can contain a mix of different objects. For example, an array can
contain a string and another array (this is an example of a *nested
array*).

An array can be instantiated with square brackets:


```ruby
  born_in_december = [ ]
```

We can populate the array with values when we create it:


```ruby
  my_list = ['apples', 'oranges']
```

If we don't want to use quote marks and commas to separate strings in a
list, we can use the `%w` syntax:


```ruby
  my_list = %w( apples oranges )
```

We can add new elements to an array with a `push` method:


```ruby
  my_list = Array.new
  => []
  my_list.push 'apples'
  => ["apples"]
  my_list.push 'oranges'
  => ["apples", "oranges"]
```

In our example code, we use the `<<` *shovel operator* to add items to
the array:


```ruby
  born_in_december << name
```

A Ruby array has close to a hundred available methods, including
operations such as `size` and `sort`. See the [Ruby
API](http://www.ruby-doc.org/core-2.4.1/Array.html) for a full list.

Iterator
--------

Of all the methods available for a Ruby collection such as Hash or
Array, the *iterator* may be the most useful.

You'll recognize an iterator when you see the `each` method applied to a
Hash or Array:


```ruby
  famous_birthdays.each
```

The `each` keyword is always followed by a block of code. Each item in
an Array, or key-value pair in a Hash, is passed to the block of code to
be processed.

Block
-----

You can recognize a *block* in Ruby when you see a `do ... end`
structure. A block is a common way to process each item when an iterator
such as `each` is applied to a Hash or Array.

In our example, we iterate over the `famous_birthdays` hash:


```ruby
  famous_birthdays.each do |name, date|
    .
    .
    .
  end
```

Within the two pipes (or bars), we assign the key and value to two
variables.

The block is like an unnamed method. The two variables are available
only within the block. As each key-value pair is presented by the
iterator, the variables are assigned, and the statements in the block
are executed.

In our example code, we evaluate each date in the `famous_birthdays`
hash to determine if the musician was born in December. When we find a
December birthday, we add the name of the musician to the
`born_in_december` array:


```ruby
  famous_birthdays.each do |name, date|
    if date.month == 12
      born_in_december << name
    end
  end
```

When you use a block within a method, any variable in your method is
available within the block. That's why we can add `name` to the array
`born_in_december`.

Computer scientists consider a block to be a programming language
construct called a *closure*. Ruby has other closures, including the
*proc* (short for procedure) and the *lambda*. Though blocks are common
you'll seldom see procs or lambdas in ordinary Rails code. They are more
common in the Rails source code where advanced programming techniques
are used more frequently.

The key point to know about a block (or a proc or a lambda) is that it
works like a method. Though you don't see a method definition, you can
use a block to evaluate a sequence of statements and obtain a result.

Rails and More Keywords
-----------------------

We've looked at only a few of the keywords and constructs you will see
in Ruby code. The exercise has improved your Ruby literacy, so you'll
have an easier time reading Ruby code.

Nothing in the exercise is Rails. The example code only uses keywords
from the Ruby API.

Rails has its own API, with hundreds of classes and methods. The Rails
API uses the syntax and keywords of the Ruby language to construct new
classes and create new keywords that are specific to Rails and useful
for building web applications.

We say Ruby is a general-purpose language because it can be used for
anything. Rails is a *domain-specific language* (DSL) because it is used
only by people building web applications (in this sense, "domain" means
area or field of activity). Ruby is a great language to use for building
a DSL, which is why it was used for Rails. Unlike some other programming
languages, Ruby easily can be extended or tweaked. For example,
developers can redefine classes, add extra methods to existing classes,
and use the special `method_missing` method to handle method calls that
aren't previously defined. Software architects call this
*metaprogramming* which simply means clever programming that twists and
reworks the programming language.

When you add a gem to a Rails project, you'll add additional keywords.
Some of the most powerful gems add their own DSLs to your project. For
example, the Cucumber gem provides a DSL for turning user stories into
automated tests.

Adding Rails, additional gems, and DSLs provides powerful functionality
at the cost of complexity. But it all conforms to the syntax of the Ruby
language. As you learn to recognize Ruby keywords and language
structures, you'll be able to pick apart the complexity and make sense
of any code.

More Ruby
---------

To develop your proficiency as a Rails developer, I hope you will make
an effort to learn Ruby as you learn Rails. Don't be lazy; when you
encounter a bit of Ruby you don't understand, make an effort to find out
what is going on. Spend time with a Ruby textbook or interactive course
when you work on Rails projects.

### Collaborative Learning

The best way to learn Ruby is to actually use it. That's the concept
behind this site:

-   [Exercism.io](http://exercism.io/)

With Exercism, you'll work though code exercises and get feedback from
other learners.

### Online Tutorials

-   [TryRuby.org](http://www.tryruby.org) - free browser-based interactive tutorial from Code School
-   [Codecademy Ruby Track](http://www.codecademy.com/tracks/ruby) - free browser-based interactive tutorials from Codecademy
-   [Ruby Koans](http://rubykoans.com/) - free browser-based interactive exercises from Jim Weirich and Joe O'Brien
-   [Ruby in 100 Minutes](http://tutorials.jumpstartlab.com/projects/ruby_in_100_minutes.html) - free tutorial from JumpstartLab
-   [Code Like This](http://codelikethis.com/lessons) - free tutorials by Alex Chaffee
-   [RailsBridge Ruby](http://curriculum.railsbridge.org/ruby/ruby) - basic introduction to Ruby
-   [CodeSchool Ruby Track](https://www.codeschool.com/paths/ruby) - instructional videos with in-browser coding exercises

### Books

-   [Learn To Program](http://pine.fm/LearnToProgram/) - free ebook by Chris Pine
-   [Learn To Program](http://pragprog.com/book/ltp2/learn-to-program) - expanded \$18.50 ebook by Chris Pine
-   [Learn Code the Hard Way](http://ruby.learncodethehardway.org/) - free from Zed Shaw and Rob Sobers
-   [Beginning Ruby](http://beginningruby.org/) - by Peter Cooper
-   [Programming Ruby](http://pragprog.com/book/ruby4/programming-ruby-1-9-2-0) - by Dave Thomas, Andy Hunt, and Chad Fowler
-   [Eloquent Ruby](http://www.amazon.com/Eloquent-Ruby-Addison-Wesley-Professional-Series/dp/0321584104/) - by Russ Olsen
-   [Books by Avdi Grimm](https://shiprise.dpdcart.com/), including *Confident Ruby* and *Objects on Rails*.

### Newsletters

-   [Practicing Ruby](http://practicingruby.com/) - \$8/month for access to over 90 helpful articles on Ruby
-   [RubySteps](https://rubysteps.com/) - weekly lessons by email from Pat Maddox

### Screencasts

-   [RubyTapas](http://www.rubytapas.com/) - \$9/month for access to over 100 screencasts on Ruby

Git
---

There's no need to save the file **lib/example.rb** file we created to
learn Ruby.

You can simply delete the file:


```console
$ rm lib/example.rb
```

Check the Git status to make sure the file is gone:


```console
$ git status
# On branch master
nothing to commit, working directory clean
```

We've cleaned up after our Ruby exercise.

From here on, we're done with silly code examples. No more fooling
around. With the next chapter, we start building a real-world Rails
website.
