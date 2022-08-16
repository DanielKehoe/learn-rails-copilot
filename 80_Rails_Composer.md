Rails Composer
==============

I'm going to show you how to skip all the work you already did, and
build a ready-to-use Rails application in less than five minutes. When
you're done with this chapter, you may wonder why you read the rest of
the book.

Watch the video for a demonstration of Rails Composer:

- [Rails Composer](https://tutorials.railsapps.org/videos/10)

## Building Starter Applications

This chapter is about [Rails Composer](http://www.railscomposer.com/), a
tool for building starter applications. Rails Composer makes building
applications so easy, it feels like a guilty pleasure.

In the introductory "Create the Application" chapter, you learned that
developers often use a starter application instead of assembling an
application from scratch. You've seen how the `rails new` command gives
you a rudimentary starter application. Developers typically add a
front-end framework, a testing framework, and a handful of favorite gems
before they get started on any custom development. Since most
applications start with the same basic components, it makes sense to
rely on an open source effort to stitch them together, so any
integration issues or update problems are quickly resolved by the
community. That's the idea behind the [RailsApps
project](http://railsapps.github.io/). The project provides a collection
of starter applications, plus Rails Composer, a tool that creates the
starter applications.

I've been leading the RailsApps project for several years because I
think the project saves time for developers and makes things easier.
I may be biased, so take a look and judge for yourself.

Build 'Learn Rails' in Less Than Five Minutes
---------------------------------------------

In less than five minutes, we can build our tutorial application using
Rails Composer. It will be identical to the application you've built,
but we'll call it "foobar-kadigan." It's a new application, so if you're
still in the **workspace/learn-rails/** project directory, move up a
level to the **workspace/** project directory:


```console
$ cd ../
$ pwd
/Users/danielkehoe/workspace
```

Or jump to it directly, if it's one level below your home directory:


```console
$ cd ~/workspace
$ pwd
/Users/danielkehoe/workspace
```

Use the "learn-rails" gemset we created earlier:


```console
$ rvm use ruby-2.4.1@learn-rails
```

Now create the "foobar-kadigan" application:


```console
$ rails new foobar-kadigan -m https://raw.github.com/RailsApps/rails-composer/master/composer.rb
```

We're using the `rails new` command and designating "foobar-kadigan" as
the name for the application. The `-m` flag applies an *application
template*, which is a script that generates an application. The
application template can be on your local computer, or retrieved from a
remote server. Rails Composer is an application template that is stored
on GitHub. When you run the `rails new` command as shown above, a new
Rails application is built and then modified by the Rails Composer
script.

Here's the first prompt you'll see:


```console
option  Build a starter application?
    1)  Build a RailsApps example application
    2)  Contributed applications
    3)  Custom application
choose  Enter your selection:
```

Options #2 and #3 are not for beginners. We'll skip any contributed
applications. And the "Custom application" option is strictly for
experts. Enter `1` to select "Build a RailsApps example
application." You'll see a list of available starter applications:


```console
option  Choose a starter application.
     1)  learn-rails
     2)  rails-bootstrap
     3)  rails-foundation
     4)  rails-mailinglist-activejob
     5)  rails-omniauth
     6)  rails-devise
     7)  rails-devise-roles
     8)  rails-devise-pundit
     9)  rails-signup-download
    10)  rails-stripe-checkout
    11)  rails-stripe-coupons
choose  Enter your selection:
```

We'll explore the list later. For now, enter `1` to select
"learn-rails".

Here's your chance to get news and announcements about Rails Composer:


```console
        Get on the mailing list for Rails Composer news?
option  Enter your email address:
```

Enter your email address (if you want news) or press "return" to
skip it (if you're shy).

In less than the time it took me to
write a few sentences, you'll have a new Rails application. Look for it in
your folder:


```console
$ ls -1
foobar-kadigan
learn-rails
```

You've just created a new application named "foobar-kadigan" that is
almost identical to the "learn-rails" application you created from
scratch. If you have a file compare tool on your computer, you can
compare the folders and see that the only differences are the
application name embedded in the application, plus a few configuration
settings such as the secret keys in the **config/secrets.yml** file.

Move into the project directory:

```console
$ cd foobar-kadigan
```
As soon as you move into the **foobar-kadigan/** folder, RVM will
automatically begin using the gemset named "foobar-kadigan." That's
because Rails Composer created hidden **.ruby-gemset** and
**.ruby-version** files.

Run `bundle install` to install the necessary gems in the RVM gemset:

```console
$ bundle install
```

Try running the application.

```console
$ cd foobar-kadigan
$ rails server
=> Booting Puma
.
.
.
```

Open a web browser window and navigate to
[http://localhost:3000/](http://localhost:3000). Try it out. You'll see
our new home page with the placeholder photo and the "sign up" form.

The application will be almost identical to the one you already built.
Compare the project files side-by-side in your editor. The files will be
nearly identical. In fact, if you made mistakes when you built the
tutorial application, Rails Composer will give you the newest and most
correct version of the application so you can check for your mistakes
with a file compare tool.

You are probably already aware that a perfect version of the tutorial
application is already on GitHub, in the [learn-rails GitHub
repository](https://github.com/RailsApps/learn-rails). You could use
`git clone` to get a copy to use as a starter application. The version
generated by Rails Composer differs in one important respect. Rails
Composer generates the application with any name you give it, so there's
no need to search and change every use of the name in the application.

I hope you're not irritated that I asked you to spend hours building the
"learn-rails" application, and then showed you how to build the same
application in less than five minutes. I promise you the time you spent
with the book is worthwhile, because you've gained a knowledge of Rails
you can't get from using Rails Composer.

A Collection of Starter Applications
------------------------------------

Since you've already built the "learn-rails" application, the identical
"foobar-kadigan" application may not be interesting. Let's look at the
other applications you can generate with Rails Composer.

### Rails Bootstrap

The "rails-bootstrap" application provides an integration of Rails and
[Bootstrap](http://getbootstrap.com/), the popular front-end framework.
This application gives you everything you built in this book's chapters on
"Layout and Views" and "Front-End Framework," including flash messages
and navigation, set up for Bootstrap. It's a good beginning point for many
custom applications.

You can examine the example application on GitHub, in the
[rails-bootstrap](https://github.com/RailsApps/rails-bootstrap)
repository.

If you have subscribed for the Capstone Rails Tutorials, you can read the
[Bootstrap Quickstart Guide](https://tutorials.railsapps.org/tutorials/bootstrap-quickstart)
to understand the code.

### Rails Foundation

The "rails-foundation" application is just like the "rails-bootstrap"
application, only with the [Zurb Foundation](http://foundation.zurb.com/)
front-end framework instead
of Bootstrap. It's a stripped-down version of the "learn-rails"
application you just built, without the contact form or mailing list
sign-up, using Foundation. If you want to build a custom application, starting with
nothing more than Foundation and an "about" page, generate the
"rails-foundation" application.

You can examine the example application on GitHub, in the
[rails-foundation](https://github.com/RailsApps/rails-foundation)
repository.

There's a [Foundation Quickstart Guide](https://tutorials.railsapps.org/tutorials/foundation-quickstart)
with the Capstone Rails Tutorials.

### Rails Mailing List with Active Job

Rails 4.2 added the [Active
Job](https://github.com/rails/rails/tree/master/activejob) feature for
background processing. The [Mailing List with Active
Job](https://tutorials.railsapps.org/tutorials/rails-mailinglist-activejob)
tutorial explains how to use it. You can use Rails Composer to generate the
[rails-mailinglist-activejob](https://github.com/RailsApps/rails-mailinglist-activejob)
starter application.

In the "Send Mail" chapter I wrote about "Asynchronous Mailing" which provides
a queueing system for background jobs. For a production website, it is smart to
use Active Job for better website performance for users. The [Mailing List with Active Job](https://tutorials.railsapps.org/tutorials/rails-mailinglist-activejob) tutorial in the
[Capstone Rails Tutorials](https://tutorials.railsapps.org/) series explains the code.

### Rails OmniAuth

[OmniAuth](https://github.com/intridea/omniauth/wiki) is a gem for
authentication. Most web applications need a way for users to sign in,
allowing access to some features of the application only for signed-in
users. OmniAuth allows a user to sign in using an account they already
have with a service such as Facebook, Twitter, or GitHub. If you're
building an application that needs quick and easy sign-in, this is a
useful starter application.

You can examine the example application on GitHub, in the
[rails-omniauth](https://github.com/RailsApps/rails-omniauth)
repository.

You can read the [OmniAuth Tutorial](https://tutorials.railsapps.org/tutorials/rails-omniauth)
in the [Capstone Rails Tutorials](https://tutorials.railsapps.org/) series to
learn about authentication with OmniAuth.

### Rails Devise

[Devise](https://github.com/plataformatec/devise) is the most popular
gem for authentication. Devise provides user management and
authentication, letting a user sign up to create an account and log in
with an email address and password. Most websites need email/password
authentication, so this is a popular starter application.

You can examine the example application on GitHub, in the
[rails-devise](https://github.com/RailsApps/rails-devise) repository.

You can read the [Devise Quickstart Guide](https://tutorials.railsapps.org/tutorials/devise-quickstart)
in the [Capstone Rails Tutorials](https://tutorials.railsapps.org/) series to
learn about user management and authentication with Devise.

### Rails Devise Roles

Devise is a popular gem for *authentication*, verifying a
user's registered identity. In conjunction with authentication,
*authorization* limits access to pages of a web application.
With role-based authorization, a user can be assigned a role such as
"user," "admin," or "VIP" (a "very important person"). If you want to
control access to features of the website by checking a user's role,
this is a useful starter application.

You can examine the example application on GitHub, in the
[rails-devise-roles](https://github.com/RailsApps/rails-devise-roles)
repository.

You can read the [Rails Authorization
Tutorial](https://tutorials.railsapps.org/tutorials/rails-devise-roles)
in the [Capstone Rails Tutorials](https://tutorials.railsapps.org/) series to learn about authorization.

### Rails Devise Pundit

To keep controllers skinny, Rails developers often use the
[Pundit](https://github.com/elabs/pundit) gem for authorization. It
improves upon simple role-based authorization to move access control
code from controllers to separate "policy objects." For complex
applications with elegant architecture, use the "rails-devise-pundit"
starter application.

You can examine the example application on GitHub, in the
[rails-devise-pundit](https://github.com/RailsApps/rails-devise-pundit)
repository.

You can read the [Pundit Quickstart Guide](https://tutorials.railsapps.org/tutorials/pundit-quickstart)
in the [Capstone Rails Tutorials](https://tutorials.railsapps.org/) series to
learn about authorization with Pundit.

### Other Starter Applications

Other applications in the Rails Composer collection include:

-   [rails-signup-download](https://github.com/RailsApps/rails-signup-download)
-   [rails-stripe-checkout](https://github.com/RailsApps/rails-stripe-checkout)
-   [rails-stripe-coupons](https://github.com/RailsApps/rails-stripe-coupons)

You can use the
[rails-signup-download](https://github.com/RailsApps/rails-signup-download)
application to build a website where a user can download a PDF file
after registering with an email address. Using the code in the [Signup and Download Tutorial](https://tutorials.railsapps.org/tutorials/rails-signup-download),
you could customize the "learn-rails" application so visitors could
download an ebook by Foobar Kadigan after they sign up for his
newsletter.

[Stripe](https://stripe.com/) is a popular service used to accept credit
card payments. Stripe offers two approaches to implementing payment
processing. Stripe Checkout is Stripe's entry-level approach. Stripe
Checkout competes with the button-based payment options from Google,
PayPal, or Amazon, adding a pop-up payment form to any web page. Stripe
Checkout is very limited because the pop-up payment form cannot be
customized for use with a Rails application. Our [Stripe Checkout Tutorial](https://tutorials.railsapps.org/rails-stripe-checkout)
in the [Capstone Rails Tutorials](https://tutorials.railsapps.org/) series
shows how to combine Stripe Checkout with Devise for simple applications.

[Stripe.js](https://stripe.com/docs/stripe.js) is optimal for use with a
Rails application, allowing full customization of a payment form and
integration with Rails form processing. The
[rails-stripe-coupons](https://github.com/RailsApps/rails-stripe-coupons)
application implements a payment feature using Stripe JS so a visitor
pays to download a PDF file. The application accommodates promotional
coupons and adds payment forms to landing pages, for real-world payment
processing. Our [Stripe JS With Coupons](https://tutorials.railsapps.org/rails-stripe-coupons) tutorial
in the [Capstone Rails Tutorials](https://tutorials.railsapps.org/) series provides the details.

Rails Composer Options
----------------------

If all Rails Composer did was copy example applications from GitHub
repos, it would be convenient but not very interesting. When you built
the "foobar-kadigan" application with Rails Composer, it simply built a
replica of our tutorial application. When you build the other starter
application, the options get more interesting. Rails Composer lets
developers customize their starter applications for their favorite stack
(we discussed stacks in the "Concepts" chapter in Book One).

Let's see what options we get when we build the powerful
[rails-devise-roles](https://github.com/RailsApps/rails-devise-roles)
starter application.

Jump to your **workspace/** folder so we can create a new application:


```console
$ cd ~/workspace
$ pwd
/Users/danielkehoe/workspace
```

It's okay to start with the "learn-rails" gemset. We have to start with
a gemset that already has the Rails gem installed. After that, Rails
Composer will create a new gemset for the new project.


```console
$ rvm use ruby-2.4.1@learn-rails
```

Now generate the "rails-devise-roles" starter application:


```console
$ rails new rails-devise-roles -m https://raw.github.com/RailsApps/rails-composer/master/composer.rb
```

Don't worry if some of the prompts are different from the ones I
describe here. Rails Composer changes often. At the time I wrote this, I
saw:


```console
option  Build a starter application?
    1)  Build a RailsApps example application
    2)  Contributed applications
    3)  Custom application
choose  Enter your selection:
```

Enter `1` to select "Build a RailsApps example application."


```console
option  Choose a starter application.
     1)  learn-rails
     2)  rails-bootstrap
     3)  rails-foundation
     4)  rails-mailinglist-activejob
     5)  rails-omniauth
     6)  rails-devise
     7)  rails-devise-roles
     8)  rails-devise-pundit
     9)  rails-signup-download
    10)  rails-stripe-checkout
    11)  rails-stripe-coupons
choose  Enter your selection:
```

Select "rails-devise-roles" (it was #7 when I wrote this, but the list
may have changed).


```console
        Get on the mailing list for Rails Composer news?
option  Enter your email address:
```

Another chance to get on the mailing list. Just hit "return" if you
already signed up.


```console
option  Web server for development?
    1)  Puma (default)
    2)  Thin
    3)  Unicorn
    4)  Phusion Passenger (Apache/Nginx)
    5)  Phusion Passenger (Standalone)
choose  Enter your selection:
```

Our first option! We've always used Puma since it is the Rails default. Choose "Puma" to keep things familiar.


```console
option  Web server for production?
    1)  Same as development
    2)  Thin
    3)  Unicorn
    4)  Puma
    5)  Phusion Passenger (Apache/Nginx)
    6)  Phusion Passenger (Standalone)
choose  Enter your selection:
```

We could get fancy for deployment. Choose "Same as development" to stay in our comfort zone.


```console
option  Database used in development?
    1)  SQLite
    2)  PostgreSQL
    3)  MySQL
choose  Enter your selection:
```

We haven't explored applications that use databases in this book, but
Devise and role-based authorization require saving a User model to a
database. Choose "SQLite," which is built-in and ready to run in the Mac
or Ubuntu environments. Developers prefer PostgreSQL for production
applications, but it takes extra effort to set up, so we'll stick with
SQLite for now.


```console
option  Template engine?
    1)  ERB
    2)  Haml
    3)  Slim
choose  Enter your selection:
```

In this book, all our view templates were written using the ERB template
language. In the "Concepts" chapter in Book One, you learned that components of
Rails can be mixed for different stacks. Some developers substitute
[Haml](http://haml.info/) or [Slim](http://slim-lang.com/) for ERB. I've
written an article on [Haml and
Rails](http://railsapps.github.io/rails-haml.html) if you'd like to know
more. Choose "ERB" for now.


```console
option  Test framework?
    1)  None
    2)  RSpec with Capybara
choose  Enter your selection:
```

You've had an introduction to testing with Minitest in the "Testing"
chapter of this book. [RSpec](http://rspec.info/) is popular among many
developers, so Rails Composer offers an "RSpec with Capybara" option.
Rails Composer will install a test suite for the
[rails-devise-roles](https://github.com/RailsApps/rails-devise-roles)
application when RSpec is selected. You can read the
[RSpec Quickstart Guide](https://tutorials.railsapps.org/tutorials/rspec-quickstart)
in the [Capstone Rails Tutorials](https://tutorials.railsapps.org/) series
to get started with RSpec. Choose "none" for now.


```console
option  Front-end framework?
    1)  None
    2)  Bootstrap 4.0
    3)  Bootstrap 3.3
    4)  Bootstrap 2.3
    5)  Zurb Foundation 5.5
    6)  Zurb Foundation 4.0
    7)  Simple CSS
choose  Enter your selection:
```

You learned to use Bootstrap 3 in this book. Let's stick with that. Choose "Bootstrap 3.3."


```console
option  Add support for sending email?
    1)  None
    2)  Gmail
    3)  SMTP
    4)  SendGrid
    5)  Mandrill
choose  Enter your selection:
```

Devise will need to send email for its "forgot password" feature.
Configuring email took some time for our tutorial application. Rails
Composer will instantly set up everything we need to send email using
our choice of services. Choose "SendGrid" for now.


```console
option  Devise modules?
    1)  Devise with default modules
    2)  Devise with Confirmable module
    3)  Devise with Confirmable and Invitable modules
choose  Enter your selection:
```

Choose "Devise with default modules." Devise has options, like a
Confirmable module that requires users to click a link in an email
message to confirm a new account. The Invitable module provides a
feature that allows administrators or other users to invite users to
establish accounts. We won't need these extra features.


```console
option  Admin interface for database?
    1)  None
    2)  Thoughtbot Administrate
choose  Enter your selection:
```

[Thoughtbot Administrate](https://github.com/thoughtbot/administrate) adds an
administrative interface to a database application. Choose "None" for
now.


```console
option  Use a form builder gem?
    1)  None
    2)  SimpleForm
choose  Enter your selection:
```

We could add the
[SimpleForm](https://github.com/plataformatec/simple_form) gem to make
it easy to build forms. We didn't use it in this book, so we'll choose "none."

Next you'll see a menu of page layout options from Rails Composer.
These are available if you use Bootstrap 3.

```console
option  Add Bootstrap page templates?
    1)  None
    2)  1 Col Portfolio
    3)  2 Col Portfolio
    4)  3 Col Portfolio
    5)  4 Col Portfolio
    6)  Bare
    7)  Blog Home
    8)  Business Casual
    9)  Business Frontpage
   10)  Clean Blog
   11)  Full Width Pics
   12)  Heroic Features
   13)  Landing Page
   14)  Modern Business
   15)  One Page Wonder
   16)  Portfolio Item
   17)  Round About
   18)  Shop Homepage
   19)  Shop Item
   20)  Simple Sidebar
   21)  Small Business
   22)  Stylish Portfolio
   23)  The Big Picture
   24)  Thumbnail Gallery
choose  Enter your selection:
```

You’ll get an option to install any of 23 different Bootstrap page templates.
Some of these are simple one page layouts. Others are complex, multipage websites.
If you’d like to see what all the templates look like, browse the
[Start Bootstrap](https://startbootstrap.com/template-categories/all/)
website to see the gallery of Bootstrap themes & templates.

I like the "Modern Business" template for several ready-made website pages, so
choose 14 to install the template.

```console
option  Install page-view analytics?
    1)  None
    2)  Google Analytics
    3)  Segment.com
choose  Enter your selection:
```

In our "Analytics" chapter, I said every application needs a way to
analyze traffic. Let's choose "Segment.com" since we learned about it
already.


```console
     option  Segment.com Write Key?
```

You can enter your Segment.com Write Key here, if you know it. Otherwise,
hit return and you'll get a placeholder you can replace later.


```console
option  Prepare for deployment?
    1)  no
    2)  Heroku
    3)  Capistrano
choose  Enter your selection:
```

This option sets up your starter application for deployment to Heroku.
Choose "no" for now.

Some developers find Rails Turbolinks annoying when they wish to integrate
JavaScript with their Rails applications.

```console
      option  Disable Rails Turbolinks? (y/n)
```

We're not adding any JavaScript so choose "n" to use Rails Turbolinks.

```console
      option  Set a robots.txt file to ban spiders? (y/n)
```

In the "Deploy" chapter you learned that you can leave your website out
of Google search results with the **robots.txt** file. Let's answer "y"
or "yes" and play it safe.


```console
      option  Create a GitHub repository? (y/n)
```

Rails Composer will create a GitHub repository for your starter
application if your credentials are set up correctly. Let's play it safe
and answer "n" or "no" to skip the repository option.

Rails Composer has all the answers it needs. On my computer, with a fast
Internet connection in the heart of San Francisco, Rails composer takes
about thirty seconds to build the starter application. It installs every
needed gem; sets configuration files; and generates views, models,
controllers, and routes. The developers who maintain the Rails Composer
project have worked out any tricky integration issues so you can expect
the starter application to work without any problems.

Try It Out
----------

You've added a new application to your collection of projects:


```console
$ ls -1
foobar-kadigan
learn-rails
rails-devise-roles
```

Let's examine the application.


```console
$ cd rails-devise-roles
$ git log --oneline
087167a rails_apps_composer: extras
6d4f710 rails_apps_composer: add Bootstrap page layouts
be68589 rails_apps_composer: navigation links
3126403 rails_apps_composer: set up database
53a029f rails_apps_composer: add README files
7c78031 rails_apps_composer: add analytics
99e9c0c rails_apps_composer: add pages
1886d2c rails_apps_composer: front-end framework
38242d7 rails_apps_composer: add roles to a User model
839749f rails_apps_composer: devise
62753db rails_apps_composer: set email accounts
0754893 rails_apps_composer: generators
09104b9 rails_apps_composer: Gemfile
b61cd18 rails_apps_composer: initial commit
```

Rails Composer set up a Git repository and committed files as it built
the application. We can see a list of Git commits with the
`git log --oneline` command.

When you move into the **rails-devise-roles/** folder, RVM will
automatically begin using the gemset named "rails-devise-roles" because
of the hidden **.ruby-gemset** and **.ruby-version** files.

Run `bundle install` to install the necessary gems in the RVM gemset:

```console
$ bundle install
```

Let's try running the application:


```console
$ rails server
=> Booting Puma
.
.
.
```

Open a web browser window and navigate to
[http://localhost:3000/](http://localhost:3000). You'll see a navigation
bar with "Sign in" and "Sign up" links that implement an authentication
feature using Devise.

Sign in with the email address "user@example.com" and the
password "changeme".  You'll see a link to the Users page in the
navigation bar that is only seen by administrators.
Click the "Users" link and you'll see a list of users (just one initially).
The first user (created by Rails Composer) is automatically assigned
administrator privileges.

Sign out and sign up to create a new account with your own email address
and password. You'll see a message "Welcome! You have signed up
successfully." You will not see the "Users" link.
Your new account is an ordinary user without administrator
privileges, so you are not allowed to see the list of all users. Notice
the navigation link "Edit account." It displays a page for account
management where you can change your name, email address, or password.

Sign out and sign in again with the administrative account
"user@example.com" and the password "changeme". Now you can view the
list of users. You can change the role of any user.

You've got a useful starter application. Without Rails Composer, an
experienced developer needs at least an hour or two to set up a similar
starter application (and possibly more time if version updates have
created integration issues).

Examine the application in your editor. Here's where a starter
application can be useful as a learning tool. Given what you've learned
so far, what do recognize as familiar? Every Rails application shares a
similar structure, so you will recognize files such as the Gemfile; and
folders such as **app/models/**, **app/controllers/**, and
**app/views/**. Explore the application. Try to guess the purpose of the
unfamiliar files and code.

If you're overwhelmed by unfamiliar files and code, try building one of
the simpler starter applications, such as
[rails-bootstrap](https://github.com/RailsApps/rails-bootstrap) or
[rails-devise](https://github.com/RailsApps/rails-devise). Every line of
code is explained in the [Capstone Rails Tutorials](https://tutorials.railsapps.org/) series
so there's no mystery code.

As a beginner, you can use Rails Composer for two purposes. You can
quickly build apps that are guaranteed to work and then pick them apart.
A "breakable toy" can be a wonderful instrument for learning. Make an
effort to understand everything in the [RailsApps example
applications](http://railsapps.github.io/) and you'll gain a solid
understanding of the basic components used in real-world Rails projects.
Secondly, start building custom applications based on the Rails Composer
starter applications. By starting with Rails Composer, you'll skip the
frustrating preliminaries of setting up a front-end framework,
authentication, or authorization and jump right into implementing your
ideas for new features. Rails Composer is often used at hackathons,
where teams race to build interesting applications for a prize, to avoid
the time sink of setting up a basic application.

A final word: Use Rails Composer judiciously. It's intended to be a tool
for experienced developers who already know how to build starter
applications from scratch using databases, front-end frameworks,
authentication, or authorization, and all the bells and whistles offered
in the Rails Composer options. Use it to pinpoint what you need to
learn, or use it to turbocharge your learning process, but don't use it
as a crutch to avoid learning the basics. To learn Rails, you must be
able to build every starter application from scratch, without Rails
Composer.

To learn more about Rails Composer, see the [Rails
Composer](http://www.railscomposer.com/) home page and the README for
the [Rails Composer
project](https://github.com/RailsApps/rails-composer/) on GitHub.
