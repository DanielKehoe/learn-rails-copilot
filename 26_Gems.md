Gems
====

The art of selecting gems is at the heart of Rails development. I
explained earlier that gems are packages of code, "software libraries,"
that have been developed and tested by other developers. Some gems add
functionality or features to a website. Other gems play a supporting
role, making development easier or implementing basic infrastructure.
Gems are open source. They are available at no charge and can be freely
copied and modified.

## Videos

Two short videos on YouTube introduce gems:

- [What Are Rubygems](https://www.youtube.com/watch?v=M4szKwqFHKs)
- [Find Rubygems](https://www.youtube.com/watch?v=MvcyW7i5Br4)

## RubyGems

It is a mark of honor to release a gem for public use, and a developer's
reputation can be established when a gem becomes popular and widely
used. Gems are often created when a developer has used the same code as
a component in more than one web application. He or she will take time
to release the code as a gem. That's how the Rails ecosystem was built,
gem by gem since 2004.

There is no evaluation or review process in publishing gems. Gems are
hosted on a public server, [rubygems.org](https://rubygems.org/). Gems
are mostly text files (like any other Ruby code), organized in a
particular format with some descriptive information (in a **gemspec**
file), and compressed and archived as a single file. A single command,
`gem push`, uploads a gem to the rubygems.org server for anyone to use.

Over 50,000 gems have been released since rubygems.org was established.
Some of these gems are used by one or two developers on their own
projects. Many others have been neglected and abandoned due to lack of
interest. Only a few thousand gems are popular and widely used. As a
Rails developer, you must master the art of finding and evaluating gems
so you can base your applications on the tried-and-true work of others.

There is no single authoritative source of recommendations for gems. The
[Ruby Toolbox](http://ruby-toolbox.com/) website categorizes and ranks
many gems by popularity, and it is a good place to begin hunting for
useful gems. Other than that, it is useful to study example applications
and search for blog posts to find which gems are most often recommended.
When you find an interesting gem, search [Stack
Overflow](http://stackoverflow.com/questions/tagged/ruby-on-rails) or
Google to see what people are saying. Look at the gem's GitHub
repository and check:

-   How many issues are open? How many are closed?
-   How recent are the commits of patches or updates?
-   Is there a CHANGELOG file?
-   Is the gem well-documented?
-   How many "stars" (people favoriting) or "forks" (people hacking)?

Popular gems are likely to have many reported issues, some of which are
trivial problems or feature requests. Gems that are actively maintained
will have many closed issues and, ideally, only a few open issues. When
you find a gem that has many open issues and no recently closed issues,
you've probably found a gem that has been abandoned. Also look at the
commit log, which you'll find on the GitHub project page in a tab at the
top of the page. Regular and recent activity in the commit log indicates
the gem is actively maintained.

Rails Gems
----------

Rails itself is a gem that, in turn, requires a collection of other
gems. This becomes clear if you look at the [summary page for
Rails](https://rubygems.org/gems/rails) on the rubygems.org site. On
that page, you'll see photos of the Rails core team. More importantly,
you'll see a list of gems that are required to use Rails:

-   [actioncable](https://github.com/rails/rails/tree/master/actioncable) - real-time communication using WebSockets
-   [actionmailer](https://github.com/rails/rails/tree/master/actionmailer) - framework for email delivery and testing
-   [actionpack](https://github.com/rails/rails/tree/master/actionpack) - framework for routing and responding to web requests
-   [actionview](https://github.com/rails/rails/tree/master/actionview) - view templates and rendering
-   [activejob](https://github.com/rails/rails/tree/master/activejob) - queueing slow tasks to run in the background
-   [activemodel](https://github.com/rails/rails/tree/master/activemodel) - architecture for model objects
-   [activerecord](https://github.com/rails/rails/tree/master/activerecord) - framework for connections to databases
-   [activesupport](https://github.com/rails/rails/tree/master/activesupport) - utility classes and Ruby library extensions
-   [bundler](http://gembundler.com/) - utility to manage gems
-   [railties](https://github.com/rails/rails/tree/master/railties) - console commands and generators
-   [sprockets-rails](https://github.com/rails/sprockets-rails) - support for the Rails asset pipeline

These are the "runtime dependencies" for Rails. Each of these gems has
its own dependencies as well. When you install Rails, a total of 63 gems
are automatically installed in your development environment.

Gems for a Rails Default Application
------------------------------------

In addition to the Rails gem and its dependencies, a handful of other
gems are included in every `rails new` default starter application:

-   [sqlite3](https://github.com/luislavena/sqlite3-ruby) - adapter for the SQLite database
-   [puma](https://github.com/puma/puma) - web application server
-   [sass-rails](https://github.com/rails/sass-rails) - enables use of the SCSS syntax for stylesheets
-   [uglifier](https://github.com/lautis/uglifier) - JavaScript compressor
-   [coffee-rails](https://github.com/rails/coffee-rails) - enables use of the CoffeeScript syntax for JavaScript
-   [turbolinks](https://github.com/rails/turbolinks) - faster loading of webpages
-   [jbuilder](https://github.com/rails/jbuilder) - utility for encoding JSON data

You may not need a SQLite database, SCSS for stylesheets, or the
others, but many developers use these tools so they are included in the
default starter application.

Where Do Gems Live?
-------------------

Gems are files saved in the computer's disk storage, containing someone
else's code that you can use in your own application.

When you run a Rails application, gems are loaded into the computer's
working memory immediately before your own custom code is loaded. Gems
are handled by the Ruby interpreter no differently than your own code.
It's all Ruby code, whether you or someone else wrote it. When you are
building an application in Rails, you don't need to think about where
gems are stored in your file system. It's all handled automatically.

Experienced programmers who have used software libraries in other
languages might wonder how it works. Here's the technical explanation
from the experts. Ruby has a `require` method that
allows you to import software libraries into your programs. RubyGems
extends the `require` method, adding gem directories to a `$LOAD_PATH`.
When Rails loads, it will automatically require each of the gems listed
in your Gemfile, finding the gems in the `$LOAD_PATH` directories.

If you're a curious person, you might like to see where the gems live.
You can run the `gem env` command to reveal the RubyGems environment
details which are normally hidden from you:


```console
$ gem env
RubyGems Environment:
  - RUBYGEMS VERSION: 2.6.4
  - RUBY VERSION: 2.4.1 (2016-04-26 patchlevel 112) [x86_64-darwin14]
  - INSTALLATION DIRECTORY: /Users/danielkehoe/.rvm/gems/ruby-2.4.1@learn-rails
  - USER INSTALLATION DIRECTORY: /Users/danielkehoe/.gem/ruby/2.3.0
  - RUBY EXECUTABLE: /Users/danielkehoe/.rvm/rubies/ruby-2.4.1/bin/ruby
  - EXECUTABLE DIRECTORY: /Users/danielkehoe/.rvm/gems/ruby-2.4.1@learn-rails/bin
  - SPEC CACHE DIRECTORY: /Users/danielkehoe/.gem/specs
  - SYSTEM CONFIGURATION DIRECTORY: /Users/danielkehoe/.rvm/rubies/ruby-2.4.1/etc
  - RUBYGEMS PLATFORMS:
    - ruby
    - x86_64-darwin-14
  - GEM PATHS:
     - /Users/danielkehoe/.rvm/gems/ruby-2.4.1@learn-rails
     - /Users/danielkehoe/.rvm/gems/ruby-2.4.1@global
.
.
.
```

If you use RVM, gems are saved to a hidden **.rvm** folder in your user
directory. A **global** subfolder contains the Bundler gem. If you've
followed the instructions in the "Get Started" chapter to install Rails,
the project-specific **learn-rails** subfolder contains the Rails gem.
If you use Chruby or Rbenv instead of RVM, your gems will be stored in a
different location.

Run the `gem which` command and you'll see where the gems live:


```console
$ gem which bundler
/Users/danielkehoe/.rvm/gems/ruby-2.4.1@global/gems/bundler-1.12.5/lib/bundler.rb
$ gem which rails
/Users/danielkehoe/.rvm/gems/ruby-2.4.1@learn-rails/gems/railties-5.1.2/lib/rails.rb
```

These are details you'll never need to know, because Ruby on Rails
handles it for you.

You'll never move or delete gems directly. Instead you'll manage gems
using the [Bundler](http://gembundler.com/) utility. The key to Bundler
is the Gemfile.

Gemfile
-------

Every Rails application has a Gemfile. Earlier, I described Rails from
the viewpoint of the "gem hunter," the developer who wants to assemble
an application from the best open source components he or she can find.
To the gem hunter, the Gemfile is the most important file in the
application. It lists each gem that the developer wants to use.

The Gemfile provides the information needed by the
[Bundler](http://gembundler.com/) utility to manage gems.

Bundler's `bundle install` command reads the Gemfile, then downloads and
saves each listed gem to the hidden gem folder. Bundler checks to see if
the gem is already installed and only downloads gems that are needed.
Bundler checks for the newest gem version and records the version number
in the **Gemfile.lock** file. Bundler also downloads any gem
dependencies and records the dependencies in the **Gemfile.lock** file.
Between the Gemfile, with its list of gems that will be used by the
application, and the **Gemfile.lock** file, with its list of
dependencies and version numbers, you have a complete specification of
every gem required to run the application. More importantly, when other
developers install your application, Bundler will automatically install
all the gems (including dependencies and correct versions) needed to run
the application. When you deploy the application to production for
others to use, automated deployment scripts (such as those used by
Heroku) install all the required gems.

Bundler provides a `bundle update` command when we want to replace any
gems with newer versions. If you run `bundle update`, any new gem
versions will be downloaded and installed and the **Gemfile.lock** file
will be updated. Be aware that updating gems can break your application,
so only update gems when you have time to test and resolve any issues.
You can run `bundle outdated` to see which gems are available in newer
versions.

If you want to prevent your fellow developers (or yourself) from
accidentally updating gems, you can specify a gem version number for any
gem in the Gemfile. The Gemfile gives fine-grained control over rules
for updating:

-   `gem 'rails', '5.0.0'` is "absolute" only version 5.0.0 will be
used
-   `gem 'rails', '>= 5.0.0'` is "optimistic" any version newer than
5.0.0 will be used
-   `gem 'rails', '\textasciitilde> 5.0.0'` is "pessimistic"

"Pessimistic" versioning needs some explanation. `\textasciitilde> 5.0.0` means use
any version greater than 5.0.0 and less than 5.1 (any patch version can
be used). `\textasciitilde> 5.0` means use any version greater than 5.0 and less than
6.0 (any minor version can be used).

In general, during development we only lock down any gem versions in the
Gemfile if we know newer versions introduce problems.

Let's take a look at the Gemfile created by the `rails new` command.

Gemfile for a Rails Default Application
---------------------------------------

Open the **Gemfile** with your text editor:


```ruby
source 'https://rubygems.org'

git_source(:github) do |repo_name|
  repo_name = "#{repo_name}/#{repo_name}" unless repo_name.include?("/")
  "https://github.com/#{repo_name}.git"
end


# Bundle edge Rails instead: gem 'rails', github: 'rails/rails'
gem 'rails', '~> 5.1.2'
# Use sqlite3 as the database for Active Record
gem 'sqlite3'
# Use Puma as the app server
gem 'puma', '~> 3.7'
# Use SCSS for stylesheets
gem 'sass-rails', '~> 5.0'
# Use Uglifier as compressor for JavaScript assets
gem 'uglifier', '>= 1.3.0'
# See https://github.com/rails/execjs#readme for more supported runtimes
# gem 'therubyracer', platforms: :ruby

# Use CoffeeScript for .coffee assets and views
gem 'coffee-rails', '~> 4.2'
# Turbolinks makes navigating your web application faster. Read more: https://github.com/turbolinks/turbolinks
gem 'turbolinks', '~> 5'
# Build JSON APIs with ease. Read more: https://github.com/rails/jbuilder
gem 'jbuilder', '~> 2.5'
# Use Redis adapter to run Action Cable in production
# gem 'redis', '~> 3.0'
# Use ActiveModel has_secure_password
# gem 'bcrypt', '~> 3.1.7'

# Use Capistrano for deployment
# gem 'capistrano-rails', group: :development

group :development, :test do
  # Call 'byebug' anywhere in the code to stop execution and get a debugger console
  gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
  # Adds support for Capybara system testing and selenium driver
  gem 'capybara', '~> 2.13'
  gem 'selenium-webdriver'
end

group :development do
  # Access an IRB console on exception pages or by using <%= console %> anywhere in the code.
  gem 'web-console', '>= 3.3.0'
  gem 'listen', '>= 3.0.5', '< 3.2'
  # Spring speeds up development by keeping your application running in the background. Read more: https://github.com/rails/spring
  gem 'spring'
  gem 'spring-watcher-listen', '~> 2.0.0'
end

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]

```

The file you see will be very similar. Some version numbers may be
different if a newer Rails version was released since this was written.

The first line, `source 'https://rubygems.org'`, directs Bundler to use
the [rubygems.org](https://rubygems.org/) server as a source for any
gems.

Notice that the second uncommented line directs Bundler to use Rails and
specifies a range of acceptable versions. In this case, the Gemfile indicates we can use
any version between 5.1.2 and 5.2.

In the Gemfile you'll see the gems for a Rails default application, such
as the sqlite3 database gem, which we described earlier. Other gems are commented out
(the lines begin with the `#` character). These are suggestions and we
can ignore them or remove them.

We won't use a database for our application but we'll keep the
`gem 'sqlite3'` entry. Configuring Rails for no database is complicated;
it is easier to keep the sqlite3 gem and not use it.

If you are developing your application on a computer using the Linux
operating system, you may need to uncomment and use the statement
`gem 'therubyracer', platforms: :ruby`. Linux doesn't have a built-in
JavaScript interpreter so you must install Node.js in your environment
or else add the therubyracer gem to each project Gemfile. For help, see
[Install Ruby on Rails -
Ubuntu](http://railsapps.github.io/installrubyonrails-ubuntu.html).

It's wise to specify the Ruby version we're using. This is needed
for automated deployment scripts such as those used by Heroku. We can
add that to the Gemfile:

```console
ruby '2.4.1'
```

If you add the Ruby version and remove the extra clutter in the **Gemfile** it will look like
this:


```ruby
source 'https://rubygems.org'
ruby '2.4.1'
gem 'rails', '~> 5.1.2'

# Rails defaults
gem 'sqlite3'
gem 'puma', '~> 3.7'
gem 'sass-rails', '~> 5.0'
gem 'uglifier', '>= 1.3.0'
gem 'coffee-rails', '~> 4.2'
gem 'turbolinks', '~> 5'
gem 'jbuilder', '~> 2.5'
group :development, :test do
  gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
  gem 'capybara', '~> 2.13'
  gem 'selenium-webdriver'
end
group :development do
  gem 'web-console', '>= 3.3.0'
  gem 'listen', '>= 3.0.5', '< 3.2'
  gem 'spring'
  gem 'spring-watcher-listen', '~> 2.0.0'
end

```

Try it now. Replace the Gemfile with the simplified code above.

Adding Gems
-----------

I've identified several gems that will be useful for our tutorial
application.

I learned about these gems from several places:

-   [Ruby Toolbox](http://ruby-toolbox.com/)
-   [RubyFlow](http://www.rubyflow.com/)
-   various blog posts
-   example code and starter apps on GitHub
-   recommendations from colleagues

We're adding these gems at the beginning of our development process
since we already know which gems we'll need. On a real project, you'll
often discover useful gems and add them to the Gemfile during the
ongoing process of development.

Here are gems we'll add to the Gemfile:

-   [bootstrap-sass](https://github.com/twbs/bootstrap-sass) - front-end framework
-   [gibbon](https://github.com/amro/gibbon) - access to the MailChimp API
-   [high_voltage](https://github.com/thoughtbot/high_voltage) - for static pages like "about"
-   [jquery-rails](https://github.com/rails/jquery-rails) - adds the [jQuery](http://jquery.com/) JavaScript library

\begin{aside}
\label{aside:jquery-update}
\heading{jQuery and Rails 5.1}

Versions of Rails prior to Rails 5.1 included the [jquery-rails](https://github.com/rails/jquery-rails)
gem by default. The gem was dropped from Rails 5.1. We'll add the jquery-rails gem because it is required by the Bootstrap front-end framework.

\end{aside}

We'll also add utilities that make development easier:

-   [better_errors](https://github.com/charliesome/better_errors) - helps when things go wrong
-   [rails_layout](https://github.com/RailsApps/rails_layout) - generates files for an application layout

Open your **Gemfile** and replace the contents with the following:


```ruby
source 'https://rubygems.org'
ruby '2.4.1'
gem 'rails', '~> 5.1.2'

# Rails defaults
gem 'sqlite3'
gem 'puma', '~> 3.7'
gem 'sass-rails', '~> 5.0'
gem 'uglifier', '>= 1.3.0'
gem 'coffee-rails', '~> 4.2'
gem 'turbolinks', '~> 5'
gem 'jbuilder', '~> 2.5'
group :development, :test do
  gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
  gem 'capybara', '~> 2.13'
  gem 'selenium-webdriver'
end
group :development do
  gem 'web-console', '>= 3.3.0'
  gem 'listen', '>= 3.0.5', '< 3.2'
  gem 'spring'
  gem 'spring-watcher-listen', '~> 2.0.0'
end

# learn-rails
gem 'bootstrap-sass'
gem 'gibbon'
gem 'high_voltage'
gem 'jquery-rails'
group :development do
  gem 'better_errors'
  gem 'rails_layout'
end
```

Notice that we've placed two gems inside a "group." Specifying a group
for development or testing ensures a gem is not loaded in production,
reducing the application's memory footprint. Rails let you specify
groups for *development*, *test*, or *production*.

About the Rails Version
------------------------

The version of Rails specified in your Gemfile should match the version
that is installed in your gemset.

If you've got Rails 5.1, there's no need to make additional changes to
the Gemfile. Any version beginning with 5.1, such as 5.1.1, will be fine.

If you have Rails 5.2 (which was not available when this was written),
you must get a new version of this book. The
newest available version of the book is listed on the README page of the
[learn-rails](https://github.com/RailsApps/learn-rails) GitHub repository.
If a newer version of the book is not available, you can install Rails 5.0.
See the articles [Install Rails](http://railsapps.github.io/installing-rails.html)
and [Updating Rails](http://railsapps.github.io/updating-rails.html)
for details about installing and switching between Rails versions.

Install the Gems
----------------

Each time you edit the Gemfile, you will run `bundle install` and restart your
web server.

You've edited the Gemfile. Install the required gems on your computer:


```console
$ bundle install
```

The `bundle install` command will download the gems from the
[rubygems.org](https://rubygems.org/) server and save them to a hidden
directory that is managed by the RVM gemset you've specified.

We'll see all the gems and their dependencies:


```console
Fetching gem metadata from https://rubygems.org/
Fetching version metadata from https://rubygems.org/
Fetching dependency metadata from https://rubygems.org/
Resolving dependencies...
Using rake 11.3.0
Using concurrent-ruby 1.0.2
Using i18n 0.7.0
Using minitest 5.9.1
.
.
.
(many more gems not shown... you get the idea)
.
.
.
Bundle complete! 20 Gemfile dependencies, 73 gems now installed.
Use `bundle show [gemname]` to see where a bundled gem is installed.
```

You can use your text editor to view the contents of **Gemfile.lock**
and you will see a detailed listing of every gem and each dependency,
with version numbers. There's no reason to edit a **Gemfile.lock** file;
if it is ever in error, delete it and run `bundle install` to recreate
it.

Run `gem list` to see all the gems that are loaded into the development
environment:


```console
$ gem list
```

The list of gems loaded in the environment is the same as the list
specified in the **Gemfile.lock** file. Here's how it works. RVM makes a
place for the gems to be stored (the RVM gemset); the **Gemfile** lists
the gems you want to use; `bundle install` reads the Gemfile and
installs the gems into the RVM gemset; the **Gemfile.lock** file records
dependencies and version numbers; and `gem list` shows you the gems that
are in the gemset and available for use.

### Troubleshooting

If your development environment is set up correctly, there should be no
difficulty installing gems with the `bundle install` command. If your
development environment is not set up correctly, you may see error
messages when Bundler attempts to install the
[Nokogiri](http://nokogiri.org/) gem. Nokogiri is often needed by other
gems (it is a *dependency* of some gems) and Nokogiri can become a
problem to install. Unlike most gems that are written in pure Ruby,
parts of Nokogiri are written in the C language and must be compiled
using system tools that vary with different operating systems. If you
get an error while installing gems, and the message says, "An error
occurred while installing nokogiri," ask for help on [Stack
Overflow](http://stackoverflow.com/questions/tagged/learn-ruby-on-rails).

Git
---

Let's commit our changes to the Git repository and push to GitHub:


```console
$ git add -A
$ git commit -m "add gems"
$ git push origin master
```

After your first use of `git push origin master`, you can use the
shortcut `git push`.

If you get a message:


```console
fatal: Not a git repository (or any of the parent directories): .git
```

It indicates you are in a folder that has not been initialized with Git.
You are probably not in your project directory. Use the Unix command
`pwd` to see where you are.

If you get a message:


```console
fatal: 'origin' does not appear to be a git repository
fatal: The remote end hung up unexpectedly
```

It shows that you can't connect to GitHub to push the changes. To
investigate, enter:


```console
$ git remote show origin
```

It is not absolutely necessary to use GitHub for this tutorial. We're
only using it so you'll be familiar with the workflow of professional
development.

We're ready to configure the application.
