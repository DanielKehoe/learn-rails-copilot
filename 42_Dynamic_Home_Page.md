Dynamic Home Page
=================

Earlier, we saw how Rails can deliver simple static web pages.

Here we'll build a dynamic home page, illustrating basic concepts you'll
need to understand Rails.

User Story
----------

We'll plan our work with a user story:


```cucumber
*Birthday Countdown*
As a visitor to the website
I want to see the owner's name
I want to see the owner's birthdate
I want to see how many days until the owner's next birthday
In order to send birthday greetings
```

This silly home page will help us explore Rails and learn about the Ruby
language.

Our goal is to build a practical web application that you can really
use. Later we'll replace this silly home page with a useful web page
that encourages visitors to sign up for a mailing list.

## Routes, Model, View, and Controller

We'll use the model-view-controller design pattern as we build our new
home page.

First, we'll set up a route so a request URL gets directed to the appropriate controller.

We'll set up a model so we obtain data we need for the home page.

We'll set up a view that contains the HTML needed to display our home page.

And finally, we'll create a controller that responds to the request, obtaining data from the model and rendering the view, sending a response to the web browser.

We can create the routes, model, view, and controller in any order. All must exist before our web application will respond to a request for a home page. In this tutorial, I've chosen to create the routes, model, view, and controller in an order that is convenient for learning.

The Name Game
-------------

Much of the art of programming lies in choosing suitable names for our
creations.

We'll need a model as a source for data about the site owner. Choosing
the most obvious name, we'll call it the Owner model:

-   Owner - the file will be **app/models/owner.rb**

What about a name for the controller that will render our home page? How
about "Home controller" or "Welcome controller?" Those names are
acceptable. But if we consider our user story, the name "Visitors
controller" is best. A visitor is the actor, so "Visitors controller" is
appropriate:

-   VisitorsController - the file will be **app/controllers/visitors_controller.rb**

Later we'll see this is a good choice because we'll create a Visitor
model to handle data about the website visitor. In Rails, there is often
a model with the same name as a controller (though a controller can use
data from multiple models).

Naming Conventions
------------------

Rails is picky about class names and filenames. That's because of the
"convention over configuration" principle. By requiring certain naming
patterns, Rails avoids complex configuration files.

Before we look at class and filename conventions, here's a note about
typographic terminology:

-   a [string](http://en.wikipedia.org/wiki/String_(computer_science)) is a sequence of characters
-   you're looking at an example of lowercase strings separated by spaces (words!)
-   Titlecase means there is an Initial Capital Letter in a string
-   [CamelCase](http://en.wikipedia.org/wiki/CamelCase) contains a capital letter in the middle of a string
-   snake_case combines words with an underscore character instead of a space

When you write code, you'll follow rules for class names:

-   `class Visitor` - the model class name is capitalized and singular
-   `class VisitorsController < ApplicationController` - for a controller, combine a pluralized model name with "Controller" in CamelCase

Here are the rules for filenames. They are always lowercase, with words
separated by underscores (snake_case):

-   the model filename matches the model class name, but lowercase, for example **app/models/visitor.rb**
-   the controller filename matches the controller class name, but snake_case, for example **app/controllers/visitors_controller.rb**
-   the views folder matches the model class name, but plural and lowercase, for example **app/views/visitors**

At first the rules may seem arbitrary, but with experience they will
make sense. The rule about no capital letters or spaces in filenames has
its origins in computer antiquity.

If you stray from these naming conventions, you'll encounter unexpected
problems and frustration.

Routing
-------

We'll create the route before we implement the model and controller.

Open the file **config/routes.rb**. Replace the contents with this:


```ruby
Rails.application.routes.draw do
  root to: 'visitors#new'
end
```

Any request to the application root
([http://localhost:3000/](http://localhost:3000/)) will be directed to
the VisitorsController `new` action.

Don't be overly concerned about understanding the exact syntax of the
code. It will become familiar soon and you can look up the details in
the reference documentation, [RailsGuides: Routing from the Outside
In](http://guides.rubyonrails.org/routing.html).

In general, when you change a configuration file you must restart your
application server. However, the **config/routes.rb** file is an
exception. You don't need to restart the server after changing routes.

If you need to start the server:


```console
$ rails server
```

Visit the page [http://localhost:3000/](http://localhost:3000). You'll
see an error message because we haven't implemented the controller. The
error message, "uninitialized constant VisitorsController," means Rails
is looking for a VisitorsController and can't find it.

Model
-----

Most Rails models obtain data from a database. When you use a database,
you can use the `rails generate model` command to create a model that
inherits from the ActiveRecord class and knows how to connect to a
database.

To keep things simple, our tutorial application doesn't need a database. Instead of inheriting
from ActiveRecord, we create a Ruby class with methods that return the
owner's name, birthdate, and days remaining until his birthday. This
simple class provides an easy introduction to Ruby code.

Create a file **app/models/owner.rb** (don't include the colon punctuation that follows):


```ruby
class Owner

  def name
    name = 'Foobar Kadigan'
  end

  def birthdate
    birthdate = Date.new(1990, 12, 22)
  end

  def countdown
    today = Date.today
    birthday = Date.new(today.year, birthdate.month, birthdate.day)
    if birthday > today
      countdown = (birthday - today).to_i
    else
      countdown = (birthday.next_year - today).to_i
    end
  end

end
```

This is your first close look at Ruby code. The oddest thing you'll see
is the owner's name, "Foobar Kadigan." Everything else will make sense
with a bit of explanation.

Keep in mind that we are using a text file to create an abstraction that
we can manipulate in the computer's memory. Software architects call
these abstractions *objects*. In Ruby, everything we create and
manipulate is an *object*. To distinguish one object from another, we
define it as a *class*, give it a *class name*, and add behavior in the
form of *methods*.

The first line `class Owner` defines the class and assigns a name. At
the very end of the file, the `end` keyword completes the class
definition.

We define three methods, starting with `def` (for "method definition")
and ending with `end`.

-   `def name` … `end`
-   `def birthdate` … `end`
-   `def countdown` … `end`

Each method contains simple Ruby code that assigns data to a variable.
Later, we'll retrieve the data for use in our view file by
*instantiating* the class and *calling* a method. Don't be discouraged
by the software architects' terminology; the concepts are simple and
we'll soon see everything in action.

Ruby makes it easy for a method to *return* data when called; the value
assigned by the last statement will be delivered when the method is
called.

Looking more closely at the Ruby code inside the method definitions,
you'll see Ruby uses the `=` (equals) sign to assign values to a
variable. The variable is named on the left side of the equals sign; a
value is assigned on the right side. We call the equals sign an
*assignment operator*.

We can assign any value to a variable, including a *string* (a series of
characters that can be a word or name) such as "Foobar Kadigan." Ruby
recognizes a string when characters are enclosed in single or double
quotes. Not surprisingly, a number also can be assigned to a variable,
either a whole number (an *integer*) or a decimal fraction (a *float*).

More interestingly, any Ruby object can be assigned to a variable. That
helps us "move around" any object very easily, giving us access to the
object's class methods anywhere we use the variable. We can create our
own objects, as we have by creating the Owner class. Or we can use the
library of objects that are supplied with Ruby. Ruby's prefabricated
objects are defined by the Ruby API (*application programming
interface*); essentially the API is a catalog of prebuilt classes that
are building blocks for any application. The Rails API gives us
additional classes that are useful for web applications. Learning the
syntax of Ruby code gets you started with Ruby programming; knowing the
API classes leads to mastery of Ruby.

The `Date` class is provided by the Ruby API. It is described in the
[Ruby API reference documentation](http://apidock.com/ruby/Date). The
`Date` class has a `Date.new` method which *instantiates* (creates) a
new date when supplied with year, month, and day *parameters*. You can
see this syntax when we assign `Date.new(1990, 12, 22)` to the
`birthdate` variable.

Note that Ruby has specific expectations about the syntax of numbers.
The `Date.new(...)` method expects integers. Imagine a September
birthday. You must use `Date.new(1990, 9, 22)`. If you enter a date in
the format `Date.new(1990, 09, 22)`, you'll get a syntax error "Invalid
octal digit" when you test the application. Ruby expects numbers that
begin with zero to be [octal
numbers](http://en.wikipedia.org/wiki/Octal); you'll get an error
because octal numbers can't contain the digit "9."

Our `countdown` method contains the most complex code in the class.

First, we set a variable `today` with today's date. The `Date.today`
method creates an object that represents the current date. When the
`Date.today` method is called, Ruby gets the current date from the
computer's system clock.

Next we create a `birthday` variable and assign a new date that combines
today's year with the month and day of the `birthdate`. This gives us
the date of Foobar Kadigan's birthday this year.

The `Date` class can perform complex calendar arithmetic. The variables
`birthdate` and `today` are *instances* of the `Date` class. We can use
a greater-than operator to determine if Foobar Kadigan's birthday is in
the future or the past.

The `if ... else ... end` structure is a *conditional statement*. If the
birthday is in the future, we subtract `today` from `birthday` to
calculate the number of days remaining until the owner's birthday, which
we assign to the `countdown` variable.

If the birthday has already passed, we apply a `next_year` method to the
birthday to get next year's birthday. Then we subtract `today` from
`birthday.next_year` to calculate the number of days remaining until the
owner's birthday, which we assign to the `countdown` variable.

The result might be fractional so we use the utility method `to_i` to
convert the result to a whole number (integer) before assigning it to
the `countdown` variable.

This shows you the power of programming in Ruby. Notice that I needed 16
paragraphs and over 600 words to explain 15 short lines of code. We used
only seven Ruby abstractions but they represent thousands of lines of
code in the Ruby language implementation. With knowledge of Ruby syntax
and the Ruby API, a few short lines of code in a text file gives us
amazing ability.

In an upcoming chapter, we'll look more closely at the syntax and
keywords of the Ruby language. But without knowing more than this, we
can build a simple web application.

Let's see how we can put this functionality to use on a web page.

View
----

The Owner model provides the data we want to see on the Home page.

We'll create the markup and layout in a View file and add variables that
present the data.

View files go in folders in the **app/views/** directory. In a typical
application, one controller can render multiple views, so we make a
folder to match each controller. You can make a new folder using your
file browser or text editor. Or use the Unix `mkdir` command:


```console
$ mkdir app/views/visitors
```

Create a file **app/views/visitors/new.html.erb** (don't include the colon punctuation that follows):


```erb
<h3>Home</h3>
<p>Welcome to the home of <%= @owner.name %>.</p>
<p>I was born on <%= @owner.birthdate %>.</p>
<p>Only <%= @owner.countdown %> days until my birthday!</p>
```

We've created a **visitors/** folder within the **app/views/**
directory. We have only a single `new` view but if we had more views
associated with the Visitors controller, they'd go in the
**app/views/visitors/** folder.

We name our View file **new.html.erb**, adding the **.erb** file
extension so that Rails will use the ERB templating engine to interpret
the markup.

There are several syntaxes that can be used for a view file. In this
tutorial, we'll use the ERB syntax that is most commonly used by
beginners. Some experienced developers prefer to add gems that provide
the [Haml](http://railsapps.github.io/rails-haml.html) or
[Slim](http://slim-lang.com/) templating engines. As you might guess, a
View that uses the Haml templating syntax would be named
**new.html.haml**.

Our HTML markup is minimal, using only the `<h3>` and `<p>` tags. The
only ERB markup we add are the `<%= ... %>` delimiters. This markup
allows us to insert Ruby code which will be replaced by the result of
evaluating the code. In other words, `<%= @owner.name %>` will appear on the page as Foobar Kadigan.

You may have noticed that we refer to the Owner model with the variable `@owner`. It will be clear when we create the Visitors controller why we use this syntax (a variable name that begins with the `@` character is called an *instance variable*).

Obviously, if all we wanted to do was include the owner's name on the page, it would be easier to simply write the text. The Rails implementation becomes useful if the name is retrieved from a database or created programmatically.

We can better see the usefulness of the Owner model when we look at the use of `<=
@owner.countdown %>`. There is no way to display a calculation using
only static HTML, so Rails gives us a way to display the birthday
countdown calculation.

If you're a programmer, you might wonder why we only output the variable
on the page. Since we can use ERB to embed any Ruby code, we could
perform the calculation right on the page by embedding
`<%= (Date.new(today.year, @owner.birthdate.month,
@owner.birthdate.day) - Date.today).to_i %>`. If you've used JavaScript
or PHP, you may have performed calculations like this, right on the
page. Rails would allow us to do so, but the practice violates the
"separation of concerns" principle that encourages us to perform complex
calculations in a model and only display data in the view.

Before we can display the home page, we need to create the Visitors
controller.

Controller
----------

The Visitors controller is the glue that binds the Owner model with the
VisitorsController#new view.

*Note:* When we refer to a controller action, we use the notation
"VisitorsController#new," joining the controller class name with the
action (method) that renders a page. In this context, the `#` character
is only a documentation convention.

*Note:* `VisitorsController` will be the class name and
**visitors_controller.rb** will be the filename. The class name is
written in [camelCase](http://en.wikipedia.org/wiki/CamelCase) (with a
hump in the middle, like a camel) so we can combine two words without a
space.

Unix commands get messy when filenames include spaces so we create a
filename that combines two words with an underscore (sometimes called
"snake_case").

Create a file **app/controllers/visitors_controller.rb** (don't include the colon punctuation that follows):


```ruby
class VisitorsController < ApplicationController

  def new
    @owner = Owner.new
  end

end
```

We define the class and name it `class VisitorsController`, inheriting
behavior from the ApplicationController class which is defined in the
Rails API.

We only need to define the `new` method. We create an *instance
variable* named `@owner` and assign an instance of the Owner model. Any
instance variables (variables named with the `@` character) will be
available in the corresponding view file.

If we don't instantiate the Owner model, we'll get an error when the
controller `new` action attempts to render the view because we use the
`@owner` instance in the view file.

Keep in mind the purpose of the controller. Each controller action
(method) responds to a request by obtaining a model (if data is needed)
and rendering a view.

You've already created a view file in the **app/views/visitors** folder.
The `new` action of the VisitorsController renders the template
**app/views/visitors/new.html.erb**.

The `new` method is deceptively simple. Hidden behavior inherited from
the ApplicationController does all the work of rendering the view. We
can make the hidden code explicit if we wish to. It would look something
like this:


```ruby
class VisitorsController < ApplicationController

  def new

    @owner = Owner.new
    render 'visitors/new'
  end

end
```

This is an example of Rails magic. Some developers complain this is
black magic because the "convention over configuration" principle leads
to obscurity. Rails often offers default behavior that looks like magic
because the underlying implementation is hidden in the depths of the
Rails code library. This can be frustrating when, as a beginner, you
want to understand what's going on.

Revealing the hidden code, we see that invoking the `new` method calls a
`render` method supplied by the ApplicationController parent class. The
`render` method searches in the **app/views/visitors** directory for a
view file named **new** (the file extension **.html.erb** is assumed by
default). The code underlying the `render` method is complex.
Fortunately, all we need to do is define the method and instantiate the
Owner model. Rails takes care of the rest.

As a beginner, simply accept the magic and don't confound yourself
trying to find how it works. As you gain experience, you can dive into
the Rails source code to unravel the magic.

Scaffolding
-----------

This tutorial aims to give you a solid foundation in basic concepts. The
model–view–controller pattern is one of the most important. I've found
the best way to understand model–view–controller architecture is to
create and examine the model, view, and controller files.

As you continue your study of Rails, you'll find other tutorials that
use the *scaffolding* shortcut. For example, [Rails Guides: Getting
Started with Rails](http://guides.rubyonrails.org/getting_started.html)
includes a section "Getting Up and Running Quickly with Scaffolding"
which shows how to use the `rails generate scaffold` command to create
model, view, and controller files in a single operation. Students often
use scaffolding to create simple Rails applications.

In practice, I've observed that working Rails developers seldom use
scaffolding. There's nothing wrong with it; it just seems that
scaffolding doesn't offer much that can't be done as quickly by hand.

Test the Application
--------------------

We've created a model, view, and controller. Now let's run the
application.

Enter the command:


```console
$ rails server
```

Open a web browser window and navigate to
[http://localhost:3000/](http://localhost:3000). You'll see our new home
page.

![Dynamic home page shows days until a birthday.\label{fig:home-page}](images/figures/learn-rails-42-home.png)

It's a very simple web page but it uses Ruby to calculate the countdown
to the birthday. And the underlying code conforms to the conventions and
structure of Rails.

Git
---

At this point, you might have the Rails server running in your console
window. We're going to run a git command in the console now.

You might think you have to enter Control-c to shut down the server and
get the command prompt. But that's not necessary. You can open more than
one console view. Your terminal application lets you open multiple
windows or tabs. If you open multiple tabs, you can easily switch between console views
without using a lot of screen real estate. If you haven't tried it, now is a good time.
On the Mac, Command+t opens a new tab in the terminal application. It is
convenient to have a console tab open for the server and another for
various Unix commands.

Let's commit our changes to the Git repository and push to GitHub:


```console
$ git add -A
$ git commit -m "dynamic home page"
$ git push
```

Now let's take a look at troubleshooting.
