Troubleshoot
============

In the last chapter, we built a dynamic home page and learned about the
model–view–controller architecture of Rails. There was a lot to learn,
but the code was simple, and I hope it worked the first time you tried
it.

Before we do any more work on our tutorial application, we need to learn
about troubleshooting and debugging. As a software developer, you'll
spend a lot of time with code that doesn't work. You'll need tools and
techniques to diagnose problems.

Git
---

In this chapter we'll make changes to the application just for
troubleshooting.

Before you get started, make sure the work you've done is committed to
your git repository. Use the `git status` command to check:


```console
$ git status
```

You should see:


```console
On branch master
nothing to commit, working directory clean
```

If `git status` reports any uncommitted changes, go back to the last
step in the previous chapter and commit your work to the git repository
before continuing. At the end of this chapter, we're going to throw away
the work we've done in this chapter. We don't want to accidentally throw
away work from the previous chapter so make sure it is committed to the
repository.

Interactive Ruby Shell
----------------------

There will be times when you want to try a snippet of Ruby code just to
see if it works. Your tool will be IRB, the Interactive Ruby shell.

IRB is a Ruby interpreter that runs from the command line. It executes
any Ruby code and provides an immediate response, allowing you to
experiment in real-time.

Let's try it.


```console
$ irb
>>
```

The command `irb` launches the program and displays a prompt that shows
your Ruby version, a line number, and an arrow. I'll just show a
simple prompt in the examples, instead.

If you enter a valid
Ruby expression, the interpreter will display the result of evaluating
the expression.

Try simple arithmetic:


```console
>> n = 2
 => 2
>> n + 2
 => 4
```

Wow! You are using your computer for simple math. Maybe you can delete
the calculator app from your phone.

IRB will evaluate any Ruby expression and helps you quickly determine if
syntax and logic is correct.

### IRB for Blocks of Code

At first glance, it appears IRB works on just one line of code.

Actually, IRB can handle multiple lines of code. Try it:


```console
>> n = 10
=> 10
>> if n < 10
>>   puts "small"
>> else
?>   puts "big"
>> end
big
=> nil
>>
```

Here we set `n = 10` and then enter a conditional statement
line-by-line. After we enter the final `end`, IRB interprets the code
and outputs the result.

You'll often enter more than one line of code in IRB. If you find
yourself frustrated because you've entered typos and had to enter the
same code repeatedly, you can use IRB to load code you've saved in a
file:


```console
>> load './mytest.rb'
```

### Quitting IRB

It can be very frustrating to find you are stuck inside IRB. Unlike most
shell commands, you can't quit with Control-c. Enter Control-d or type
`exit` to quit IRB:


```console
$ irb
>> exit
```

### Learn More About IRB

Here's an entertaining way to learn about IRB:

-   [Why's (Poignant) Guide to Ruby (with a Basic Introduction to IRB)](http://poignant.guide/book/expansion-pak-1.html)

Here's a more conventional way to learn about IRB:

-   [The Pragmatic Programmer's Guide](http://ruby-doc.com/docs/ProgrammingRuby/html/irb.html)

### Beyond IRB

If you ask experienced Rails developers for help with IRB, they'll often
recommend you switch to Pry. [Pry](http://pryrepl.org/) is a powerful
alternative to the standard IRB shell for Ruby. As you gain experience,
you might take a look at Pry to see what the enthusiasm is all about.
But for now, as a beginner trying out a few lines of Ruby code, there's
no need to learn Pry.

Rails Console
-------------

IRB only evaluates expressions that are defined in the Ruby API. IRB
doesn't know Rails.

It'd be great to have a tool like IRB that evaluates any expression
defined in the Rails API. The tool exists; it's called the Rails
console. It is particularly useful because it loads your entire Rails
application. Your application will be running as if the application was
waiting to respond to a web request. Then you can expose behavior of any
pieces of the web application.


```console
$ rails console
...
Loading development environment (Rails 5.x.x)
>>
```

The Rails console behaves like IRB but loads your Rails development
environment. The prompt shows it is ready to evaluate an expression.

Let's use the Rails console to examine our Owner model:


```console
>> myboss = Owner.new
 => #<Owner:0x007fc18e91faf8>
```

We've created a variable named `myboss` and created a new instance of
the Owner class. The Rails console responds by displaying the unique
identifier it uses to track the object. The identifier is not
particularly useful, except to show that something was created.

If you're unsure about the difference between an *instance* and a
*class*, we've just seen that we can make one or more instances of a
class by calling the `Owner.new` method. When we specify the `Owner`
class, the class definition is loaded into the computer's working memory
(our development environment) from the class definition file on disk.
Then we can use the `Owner.new` method to make one or more instances of
the `Owner` class. Each instance is a unique object with its own data
attributes but the same behavior as other objects instantiated from its
class.

Let's assign the name of our boss to a variable called `name`:


```console
>> name = myboss.name
 => "Foobar Kadigan"
```

Our variable `myboss` is an instance of an `Owner` class so it responds
to the method `Owner.name` by returning the owner's name.

We want to show respect to our boss so we'll perform some *string
manipulation*:


```console
>> name = 'Mr. ' + name
 => "Mr. Foobar Kadigan"
```

We're done for now. When we quit the Rails console or shut down the
computer the `Owner` class definition remains stored on disk but the
instances disappear. The bits that were organized to create the variable
`name` will evaporate into the ether.

Actually, the bits are still there, in the form of logic states in the
computer's chips, but they have no meaning until another program uses
them.

Enter Control-d or type `exit` to quit the Rails console.

The Rails console is a useful utility. It is like a handy calculator for
your code. Use it when you need to experiment or try out short code
snippets.

Rails Logger
------------

As you know, a Rails application sends output to the browser that makes
a web request. On every request, it also sends diagnostic output to the
*server log file*. Depending on whether the application is running in
the development environment or in production, the log file is here:

-   **log/development.log**
-   **log/production.log**

In development, everything written to the log file appears in the
console window after you run the `rails server` command. Scrolling the
console window is a good way to see diagnostics for every request.

Here's what you see in the log after you visit the application home
page:


```console
Started GET "/" for ::1 at ...
Processing by VisitorsController#new as HTML
  Rendering visitors/new.html.erb within layouts/application
  Rendered visitors/new.html.erb within layouts/application (6.6ms)
Completed 200 OK in 650ms (Views: 634.4ms | ActiveRecord: 0.0ms)
```

You may have more than one console window open in the terminal
application. If you don't see your log output in your terminal, check if
you have tabs with other windows.

Here's the best part. You can add your own messages to the log output by
using the Rails logger. Let's try it out.

Modify the file **app/controllers/visitors_controller.rb**:


```ruby
class VisitorsController < ApplicationController

  def new
    Rails.logger.debug 'DEBUG: entering new method'
    @owner = Owner.new
    Rails.logger.debug 'DEBUG: Owner name is ' + @owner.name
  end

end
```

Visit the home page again and you'll see this in the console output:


```console
Started GET "/" for ::1 at ...
Processing by VisitorsController#new as HTML
DEBUG: entering new method
DEBUG: Owner name is Foobar Kadigan
  Rendering visitors/new.html.erb within layouts/application
  Rendered visitors/new.html.erb within layouts/application (1.1ms)
Completed 200 OK in 81ms (Views: 72.2ms | ActiveRecord: 0.0ms)
```

If you really needed to do so, you could add a logger statement at every
step in the application. You could see how the application behaves, step
by step. And you could "print" the value of every variable at every
step. You'll never need diagnostics at this level of detail in Rails,
but the logger is extremely useful when you are trying to understand
unexpected behavior.

Let's add logger statements to the `Owner` model. Modify the file
**app/models/owner.rb**:


```ruby
class Owner

  def name
    name = 'Foobar Kadigan'
  end

  def birthdate
    birthdate = Date.new(1990, 12, 22)
  end

  def countdown
    Rails.logger.debug 'DEBUG: entering Owner countdown method'
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

We added the `Rails.logger.debug` statement to the `Owner.countdown`
method.

Visit the home page and here's what you'll see in the console output:


```console
Started GET "/" for ::1 at ...
Processing by VisitorsController#new as HTML
DEBUG: entering new method
DEBUG: Owner name is Foobar Kadigan
  Rendering visitors/new.html.erb within layouts/application
DEBUG: entering Owner countdown method
  Rendered visitors/new.html.erb within layouts/application (0.7ms)
Completed 200 OK in 69ms (Views: 61.1ms | ActiveRecord: 0.0ms)
```

You'll often need to "get inside" the model or controller to see what's
happening. The Rails logger is the best tool for the job.

Here are some tricks for the Rails logger.

In a controller, you can use the method `logger` on its own. In a model,
you have to write `Rails.logger` (both class and method).

You can use any of the methods `logger.debug`, `logger.info`,
`logger.warn`, `logger.error`, or `logger.fatal` to write log messages.
By default, you'll see any of these messages in the development log. Log
messages written with the `logger.debug` method will not be recorded in
a production log file.

If you want your log messages to stand out, you can add formating code
for color:


```ruby
Rails.logger.debug "\033[1;34;40m[DEBUG]\033[0m " + 'will appear in bold blue'
```

For more about the Rails logger, see the [RailsGuide: Debugging Rails
Applications](http://guides.rubyonrails.org/debugging_rails_applications.html).

Revisiting the Request-Response Cycle
-------------------------------------

Earlier, when we investigated the request-response cycle, we looked in
the server log to see the response to the web browser request.

Now, with debug statements in the controller and model, we'll see
messages showing the server's traverse of the model-view-controller
architecture.


```console
Started GET "/" for ::1 at ...
Processing by VisitorsController#new as HTML
DEBUG: entering new method
DEBUG: Owner name is Foobar Kadigan
  Rendering visitors/new.html.erb within layouts/application
DEBUG: entering Owner countdown method
  Rendered visitors/new.html.erb within layouts/application (0.7ms)
Completed 200 OK in 69ms (Views: 61.1ms | ActiveRecord: 0.0ms)
```

Notice how the diagnostic messages in the console window match the
headers in the browser Developer Tools view. The browser's "Request
Method:GET" matches the server's "Started GET." The browser's "Status Code: 200"
matches the server's "Completed 200 OK" (you might have to clear the
browser's cache if the browser is showing "304 Not Modified").

We can see evidence of the model-view-controller architecture.
"Processing by VisitorsController#new" shows the program flow entering
the controller. Our debug statements show we enter the `new` method and
reveal the value of the Owner name. The next debug statement reveals the
flow has passed to the Owner model. A diagnostic message shows the
controller has rendered the **visitors/new.html.erb** view file.
Finally, the "Completed 200 OK" message indicates the response has been
sent to the browser.

As we learned, the model-view-controller architecture is an abstract
design pattern. We've seen it reflected in the file structure of the
Rails application directory. Now we can see it as activity in the server
log.

The Stack Trace
---------------

The Rails logger is extremely useful if you want to insert messages to
show program flow or display variables. But there will be times when
program flow halts and the console displays a *stack trace*.

Let's deliberately create an error condition and see an error page and
stack trace.

Modify the file **app/controllers/visitors_controller.rb**:


```ruby
class VisitorsController < ApplicationController

  def new
    Rails.logger.debug 'DEBUG: entering new method'
    @owner = Owner.new
    Rails.logger.debug 'DEBUG: Owner name is ' + @owner.name
    DISASTER
  end

end
```

Visit the home page and you'll see an error page:

![Error page.\label{fig:error-page}](images/figures/learn-rails-43-error.png)

You'll see this error page because we've installed the
[better_errors](https://github.com/charliesome/better_errors) gem.
Without the better_errors gem, you'd see the default Rails error page
which is quite similar.

In the console log, the stack trace will show everything that happens
before Rails encounters the error:


```console
Started GET "/" for ::1 at ...
Processing by VisitorsController#new as HTML
DEBUG: entering new method
DEBUG: Owner name is Foobar Kadigan
Completed 500 Internal Server Error in 8ms (ActiveRecord: 0.0ms)

NameError - uninitialized constant VisitorsController::DISASTER:
  app/controllers/visitors_controller.rb:7:in `new'
  .
  .
  .
```

To save space, I'm only showing the top line of the stack trace. I've
eliminated about sixty lines from the stack trace.

Don't feel bad if your reaction to a stack trace is an immediate, "TMI!"
Indeed, it is usually Too Much Information. There are times when it pays
to carefully read through the stack trace line by line, but most often,
only the top line of the stack trace is important.

In this case, both the error page and the top line of the stack trace
show the application failed (I prefer to say, "barfed") when it encountered an
"uninitialized constant" at line 7 of the
**app/controllers/visitors_controller.rb** file in the `new` method.
It's easy to find line 7 in the file and see that is exactly where we
added a string that Rails doesn't understand.

The point of this exercise is to encourage you to read the top line of
the stack trace and use it to diagnose the problem. I'm always surprised
how many developers ignore the stack trace, probably because it looks
intimidating.

Raising an Exception
--------------------

As you just saw, you can purposefully break your application by adding
characters that Rails doesn't understand. However, there is a better way
to force your program to halt, called *raising an exception*.

Let's try it. Modify the file
**app/controllers/visitors_controller.rb**:


```ruby
class VisitorsController < ApplicationController

  def new
    Rails.logger.debug 'DEBUG: entering new method'
    @owner = Owner.new
    Rails.logger.debug 'DEBUG: Owner name is ' + @owner.name
    raise 'Deliberate Failure'
  end

end
```

You can throw an error by using the `raise` keyword from the Ruby API.
You can provide any error message you'd like in quotes following
`raise`.

Here's the console log after you try to visit the home page:


```console
Started GET "/" for ::1 at ...
Processing by VisitorsController#new as HTML
DEBUG: entering new method
DEBUG: Owner name is Foobar Kadigan
Completed 500 Internal Server Error in 6ms (ActiveRecord: 0.0ms)

RuntimeError - Deliberate Failure:
  app/controllers/visitors_controller.rb:7:in `new'
  .
  .
  .
```

Before we continue, let's remove the deliberate failure. Modify the file
**app/controllers/visitors_controller.rb**:


```ruby
class VisitorsController < ApplicationController

  def new
    Rails.logger.debug 'DEBUG: entering new method'
    @owner = Owner.new
    Rails.logger.debug 'DEBUG: Owner name is ' + @owner.name
  end

end
```

Rails and the Ruby API provide a rich library of classes and methods to
raise and handle exceptions. For example, you might want to display an
error if a user enters a birthdate that is not in the past. Rails
includes various exception handlers to display errors in production so
users will see a helpful web page explaining the error.

Git
---

There's no need to save any of the changes we made for troubleshooting.

You could go to each file and carefully remove the debugging code you
added. But there's an easier way.

Check which files have changed:


```console
$ git status
# Changes not staged for commit:
#   (use "git add ..." to update what will be committed)
#   (use "git checkout -- ..." to discard changes in working directory)
#
# modified:   app/controllers/visitors_controller.rb
# modified:   app/models/owner.rb
#
no changes added to commit (use "git add" and/or "git commit -a")
```

Use Git to revert your project to the most recent commit:


```console
$ git reset --hard HEAD
```

The Git command `git reset --hard HEAD` discards any changes you've made
since the most recent commit. Check the status to make sure:


```console
$ git status
# On branch master
nothing to commit, working directory clean
```

We've cleaned up after our troubleshooting exercise.
