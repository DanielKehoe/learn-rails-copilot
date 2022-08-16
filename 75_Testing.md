Testing
=======

You don't need to read this chapter if you will always be a student, or
a hobbyist, working on personal projects. But if you wish to work as a
professional Rails developer, or launch your own startup, with money and
reputation at stake, you must learn about testing. In this chapter, I'll
introduce the basic concepts of testing and show how to build a test
suite for the tutorial application.

Why Test?
---------

Software applications are fragile. When you write a song, you can
include a wrong note and the song won't break. In a film, technical
flaws like a "jump cut" or a microphone in the frame won't ruin an
entire movie. But an unseen error in a software program can disrupt a
key feature or crash the entire application.

Software applications are never finished. Songs and movies reach a stage
of completion and are delivered to their audience, with no expectation
that the completed work will change. With software applications, there's
always an upcoming version with bug fixes or new features. As web
developers, we continue to make changes to the applications that our
customers are actively using. Sometimes new features are delivered
within minutes, or hours, of committing new code to the repository.

Software applications are complex. A web application, or any software
program, is a machine with intricately connected parts, or
*dependencies*. As an application grows, the connections quickly grow
more complex, to the point where no one is able to see all the
dependencies at once. Plus, web applications are often a collaborative
effort, so no one person is familiar with every line of code.

Combine the evolving nature of an application, with the complexity of
the product, and the likelihood that flaws will be immediately noticed
by users, and you'll realize why testing is so important to the software
development process.

Testing was once considered the sole responsibility of a *quality
assurance* (QA) department. Senior developers created new features or
fixed bugs. When the work was "done," lesser paid (and lower status)
developers "in QA" clicked through screens, with written notes or
scripts, as if they were users testing every feature of a program.
Invariably, manual testing led to oversights, because testing notes were
out of date, "edge cases" were overlooked, and the work was monotonous.
In the best-run companies, QA engineers are now expert consultants on
testing methods and a source of guidance for other developers. We now
rely on *automated testing*. Even more important, the job of writing
test code now belongs to the developer who creates a feature or fixes a
bug. It's our responsibility to write adequate tests for any code we add
to the repository.

What Are Tests?
---------------

Developers talk about testing as if it were an activity different from
writing code. It is not. Testing is something we do while writing code.
We create tests with the same text editor we use use to write code. The
tests themselves are written in Ruby, just like any other part of a
Rails application. You'll put the test code in either a **tests/** or
**spec/** folder, committed to the Git repository with all the other
code. You'll use the specialized API of a testing framework for the
methods of your tests, either
[Minitest](https://github.com/seattlerb/minitest) or
[RSpec](http://rspec.info/). Test code is different from code that
implements features in one significant way: Instead of supporting
interactions with a user, test code interacts with the code you've
written, verifying the code behaves as intended.

Scripted or Exploratory
-----------------------

When testing is used for quality assurance, the goal is to create a
suite of automated tests that will reveal any bugs that creep into code
and break the application. Sometimes this is called *scripted testing*.
These tests are checked into the software repository and maintained with
the application. Often developers will set up a system for *continuous
integration* (CI), which will automatically run the test suite whenever
the repository is updated. Developers can set up a CI server such as
[Jenkins](http://jenkins-ci.org/) or use a hosted CI service such as
[Travis CI](https://travis-ci.com/), [CircleCI](https://circleci.com/),
or [Semaphore](https://semaphoreapp.com/) to run tests automatically.
Automated testing with continuous integration serves as a safety net for
developers.

There is another role for testing, which is often called *exploratory
testing*, or *developer testing*. These tests may end up in an
application test suite, but the primary purpose is to help a developer
construct an application. Many developers, after gaining experience in
writing tests for quality assurance, realize that writing tests can be a
useful first step in figuring out how a feature should be implemented.
It may seem odd to write tests first, but exploratory testing can
clarify what behavior will be required, and help the developer think
through alternatives and edge cases. This approach is called *test-first
development*, and many developers will tell you that when you write
tests first, you'll be more satisfied; you'll be more focused; and
you'll avoid tangents and detours of the
"nice-to-have-but-not-really-needed" variety. We'll look closely at
test-first development in conjunction with Test-Driven Development (TDD)
and Behavior-Driven Development (BDD) at the end of this chapter. First,
let's gain an understanding of testing terminology and practice.

Regression and Acceptance
-------------------------

We describe tests by the purpose they serve. In addition to exploratory
testing used in test-first development, there are several kinds of tests
used for quality assurance.

*Regression tests* are run every time we change code. Sometimes we want
to make sure new features don't break the existing application. More
often, we run tests after changing existing code to make it more
readable, elegant, or effective. We call this tinkering "*refactoring*."
Refactoring is very similar to what we call editing or rewriting when we
work with the written word. Before we refactor, we need to know what
results we expect from our code, and we need automated tests to execute
our code and check for the expected results. If our automated tests are
adequate, we can use the tests as regression tests, making sure our
refactoring hasn't introduced new bugs.

*Acceptance tests* are sometimes identical to regression tests, and may
use the same test code. The purpose is different, so we give this kind
of testing a different name. Acceptance tests provide accountability and
serve a management function. These are tests that determine if a feature
has been implemented as expected. It is common to run acceptance tests
when an outside contractor delivers code, so we can determine if the
team has delivered what we requested. We can also use acceptance tests
to determine if our internal team has implemented the stated
requirements. Proponents of behavior-driven development claim that the
process of creating acceptance tests clarifies the product requirements.
Obviously, if we want adequate acceptance tests, we need to plan
carefully when specifying the product requirements. If we've planned
well, we can turn our user stories into automated tests that serve as
acceptance tests.

Units and Integration
---------------------

We also describe tests by their relationship to the rest of the code.

*Unit tests* probe the internal workings of the machine. If we've
written our code well, a small section of the code, such as a class or a
method, will be a discrete unit that can be tested independently of all
other units. Unit tests inspect the integrity of small parts of the
application in isolation. When a unit test fails, we can quickly
identify and fix broken code.

We use *integration tests* to make sure the entire application works as
expected. Integration tests mimic the behavior of real users. For a web
application, an integration test may simulate a user signing in, filling
out forms, clicking between pages, and verifying that contents of pages
match expected results. Integration tests can also be called *feature
tests* if they are designed to confirm that product features work as
expected. Our feature tests can serve as acceptance tests if we use the
test suite to determine if we've correctly implemented our user stories
or other product specifications. Sometimes these tests are called *black
box tests* because the code is tested as if the application was a black
box, with the internal workings of the application hidden from the
observer. They are also called *system tests* or *end-to-end tests*.

Sample Data
-----------

When we write tests, either feature tests or unit tests, we often want
to check whether a method returns the data we expect. That means we have
to create the data we need in advance of the test. Either we populate a
database with the data we expect, or we disconnect the database and
instantiate an object that provides the data we expect. Test frameworks
give us a tool named a *factory* or a *fixture* to create sample data.
Developers argue about what is better, factories or fixtures, but you'll
encounter factories more often, particularly the popular
[FactoryGirl](https://github.com/thoughtbot/factory_girl) gem. A factory
is an object that creates other objects. When you use FactoryGirl, you
have the option of saving your object to the database (which is slow) or
building your object in memory only (which is faster). Fixtures are used
to populate a database with sample data before your tests run. If you
use fixtures, you'll save sample data in a configuration file. Before
tests run, Rails automatically loads all fixtures from configuration
files in the **test/fixtures** folder. As you gain experience with
testing, you'll become familiar with both factories and fixtures.

Test Doubles
------------

In unit testing, to isolate small parts of the application, sometimes we
artificially decouple the code from the rest of the application. For
example, with a unit test, we don't want to connect to an external
service with an API to obtain data. Or we simply want a method to get a
predictable response from another object.

*Test doubles* stand in for external dependencies. The term is borrowed
from Hollywood, where stunt doubles stand in for actors in action
scenes. A test double is any kind of pretend object used in place of a
real object for testing purposes. There are two types of test doubles,
*stubs* and *mocks*. Stubs provide canned answers to calls made during
the test, only responding when queried by the test. Sometimes stubs
record information about the call, for example, the message sent or the
number of times called. Mocks are pre-programmed objects that reproduce
the behavior of the object they represent, forming a specification of an
object's behavior. It takes time to write stubs and mocks and lots of
experience to use them correctly, so as a beginner, you probably won't
write stubs and mocks without help. As you can gain experience, you'll
better understand the difference between stubs and mocks and learn how
to use them. For now, it is enough to recognize the terminology and
remember that tests run faster and better when we reduce coupling and
complexity with test doubles.

Minitest and RSpec
------------------

You've already learned that Rails developers mix and match gems to
create a favorite technology *stack*. Not everyone likes ERB for view
templates. Some prefer Haml or Slim syntax for mixing HTML and Ruby in a
view. Developers often stray from the default Rails stack when it comes
to testing. Since the release of Ruby 1.9,
[Minitest](https://github.com/seattlerb/minitest) has been supplied as a
standard gem with all Ruby installations. Yet most Rails developers use
[RSpec](http://rspec.info/) for testing.

In this tutorial, I'll use Minitest to introduce you to testing.
Minitest is easier to set up and offers a syntax that is very similar to
RSpec. Some developers say that there is no reason to use RSpec because
Minitest provides almost all the convenience of RSpec with smaller size,
faster speed, and less complexity. Other developers insist that RSpec is
more expressive and flexible. Realistically, if you want a job working
on most Rails teams, you'll need to learn RSpec. Get started with
Minitest to learn the basics of testing. When you're ready for the next
step, the [Capstone Rails Tutorials](https://tutorials.railsapps.org/) will
take you deeper. I also recommend the books [Rails 4 Test Prescriptions](http://pragprog.com/book/nrtest2/rails-4-test-prescriptions)
by Noel Rappin and [Everyday Rails Testing with RSpec](https://leanpub.com/everydayrailsrspec)
by Aaron Sumner.

Capybara, the Ghost in the Machine
----------------------------------

Unit tests are simple, in principle and often in practice. The tests are
just Ruby code, supplemented with methods from the test framework API.
If we want unit tests for all the methods of a User class, we
instantiate the class and write code that calls each method and verifies
if the response matches our expectations. Using methods from the
Minitest or RSpec test framework, we output a message that indicates
whether each unit test passes or fails.

Integration tests, or feature tests, require more of a framework than
unit tests. We want our tests to be as realistic as possible, as if a
robot was using a web browser and interacting with our web application.
Fortunately, the maintainers of the
[Capybara](http://jnicklas.github.io/capybara/) gem have created such a
robot. To create integration tests, we add the Capybara gem, using it
with either Minitest or RSpec. Capybara gives us a `visit` method that
simulates a user visiting a page. After we call the `visit` method,
Capybara gives us a `page` object and allows us to test whether the page
contains the content we expect. Every Rails application relies on a
layer of *middleware* named [Rack](http://rack.github.io/) that ties
into a web server. Capybara interacts with the web application, via
calls to Rack, as if it was a browser making requests and receiving HTML
files as a response.

When we use Capybara, by default it operates in *headless mode*,
interacting directly with the Rails application via Rack. "Headless"
means there is no graphical user interface (as if the absent screen was
a computer's head). In headless mode, JavaScript is unavailable. If some
of our application features require JavaScript, we must set up Capybara
to act as a robot using a real web browser. Capybara has a built-in
*driver* (named
[Selenium](http://docs.seleniumhq.org/projects/webdriver/)) that gives
our robot the option of automatically launching and using a real web
browser for each test. By default, Capybara will use the Firefox web
browser if it is installed on your computer. What you'll see is amazing.
When you run tests using Capybara with the JavaScript option, the
Firefox web browser will pop open on your desktop and you'll watch a
ghost flying through your web application. With Capybara, you now have a
ghostly QA department running your integration tests.

Four Phases of Feature Tests
----------------------------

Test code is easier to understand when you recognize that tests proceed
in stages, or phases. Code that simulates a user visiting a web page
tends to be organized in four phases:

-   set up
-   visit page
-   verify page contents
-   neutralize

The setup phase may include creating a user, signing in, or any other
activity that creates the conditions for a test. With Capybara, the test
visits the page, which requires Capybara to simulate a browser request
to the Rails application. Then, in the third stage, we check if the
server response contains the data we expect. Finally, we may need to
clean up, resetting the original state of the application, or removing
any data the test added to the database.

Four Phases of Unit Tests
-------------------------

Unit tests also are organized in four stages:

-   set up
-   exercise
-   verify
-   teardown

When you test a small part of the application in isolation, you'll focus
on an object or method which we call the "system under test." The setup
phase prepares the system under test. Often this means instantiating an
object. Here is an example:


```ruby
user = User.new(email: 'user@example.com')
```

During the exercise phase, something is executed. Often this is a method
call:


```ruby
user.save
```

During verification, the result of the exercise is verified against the
developer's expectations:


```ruby
user.email.must_equal 'user@example.com'
```

During teardown, the system under test is reset to its initial state.
Rails integrates with Minitest or RSpec to reset a database to its
initial state. You will seldom write code for the teardown phase.

Now that you've learned about the basic concepts of testing, let's set
up Minitest for our first tests.

Set Up Minitest
---------------

We'll set up testing with both Minitest and Capybara, so we can write
both unit tests and feature tests. Minitest is a standard Ruby gem,
installed when you install Ruby in your environment. We'll install the
[minitest-spec-rails](https://github.com/metaskills/minitest-spec-rails)
gem which makes it easy to use an RSpec-like syntax with Minitest. We'll
also add the
[minitest-rails-capybara](https://github.com/blowmage/minitest-rails-capybara)
gem to integrate Capybara with Minitest and Rails.

Open your **Gemfile** and replace the contents with the following:

**Gemfile**


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
  gem 'sqlite3'
end
group :production do
  gem 'pg'
end
group :test do
  gem 'minitest-spec-rails'
  gem 'minitest-rails-capybara'
end
```

We've added the two gems to the `test` group. Now, some gems are loaded
only when we're writing code (during development), some are loaded only
when the application is running on Heroku (deployed to production), and
our newest additions only are loaded when we run tests.

Next, install the additional gems:


```console
$ bundle install
```

The `bundle install` command will download and install the gems from the
[rubygems.org](https://rubygems.org/) server.

### Run Tests

The command `rails test` will execute Minitest. Let's see what happens
when we run tests:

```console
$ rails test
Running via Spring preloader in process 29254
/Users/danielkehoe/workspace/learn-rails/db/schema.rb doesn't exist yet.
Run `rails db:migrate` to create it, then try again. If you do not intend
to use a database, you should instead alter /Users/danielkehoe/workspace/
/learn-rails/config/application.rb to limit the frameworks that will be loaded.
Run options: --seed 35136

# Running:
Finished in 0.005570s, 0.0000 runs/s, 0.0000 assertions/s.
0 runs, 0 assertions, 0 failures, 0 errors, 0 skips
```
Rails Minitest informs us that our application is not set up to use a database.
The easiest way to resolve the issue is to run `rails db:migrate` which sets up the
database schema file. We're not using a database for this application so the database
schema file will be empty.

```console
$ rails db:migrate
```
The `rails db:migrate` command doesn't produce any result in the terminal but it will create
a new **db/schema.rb** file.

Try running `rails test` again:

```console
$ rails test
Running via Spring preloader in process 29468
Run options: --seed 46952

# Running:

Finished in 0.005945s, 0.0000 runs/s, 0.0000 assertions/s.
0 runs, 0 assertions, 0 failures, 0 errors, 0 skips
```

The output shows that Minitest executes but we have no tests for it to
run.

Let's commit our changes to the Git repository and push to GitHub:


```console
$ git add -A
$ git commit -m "set up minitest"
$ git push
```

Unit Test (Standard Syntax)
---------------------------

In its default form, Minitest uses the syntax of the older [test_unit
framework](http://test-unit.github.io/) that was supplied with Ruby
before version 1.9. The test_unit syntax uses explicit Ruby to set up
tests. Here's an example of Minitest using the test_unit syntax:


```ruby
require 'test_helper'

class VisitorTest < ActiveSupport::TestCase

  def valid_params
    { email: 'john@example.com' }
  end

  def test_valid
    visitor = Visitor.new valid_params
    assert visitor.valid?, "Can't create with valid params: #{visitor.errors.messages}"
  end

  def test_invalid_without_email
    params = valid_params.clone
    params.delete :email
    visitor = Visitor.new params
    refute visitor.valid?, "Can't be valid without email"
    assert visitor.errors[:email], "Missing error when without email"
  end

end
```

Notice that we must declare a class `VisitorTest` that inherits from
`ActiveSupport::TestCase`. Then we must define a new method for each
test case using the `def` keyword. This syntax is not popular with Rails
developers. RSpec offers its own DSL (domain specific language) that
hides the overhead of setting up classes and methods behind convenience
methods. Minitest offers its own version of the the RSpec DSL, allowing
us to use the more popular syntax. I'll use the new RSpec-like syntax in
this tutorial, since you are likely to encounter RSpec more frequently.

Unit Test (Spec Syntax)
-----------------------

For our first test, let's create a simple unit test for our Visitor
model. Every time we run our tests, we want to know that we're able to
create a Visitor model. We'll also check that the Visitor model contains
a method that returns an email address.

The default Rails directory structure already contains a
**test/models/** folder. Thanks to Rails conventions, we know exactly
where to create our test file.

Create a file **test/models/visitor_test.rb**:


```ruby
require 'test_helper'

describe Visitor do

  let(:visitor_params) { {email: 'user@example.com'} }
  let(:visitor) { Visitor.new visitor_params }

  it 'is valid when created with valid parameters' do
    visitor.must_be :valid?
  end

  it 'is invalid without an email' do
    # Delete email before visitor let is called
    visitor_params.delete :email
    visitor.wont_be :valid? # Must not be valid without email
    visitor.errors[:email].must_be :present? # Must have error for missing email
  end

end
```

The test above, written in the RSpec-like syntax, is functionally
identical to the previous example, written in the old test_unit syntax.
Take a close look at both, so the structure and keywords will be
familiar when you see it again.

We need `require 'test_helper'` to enable the test framework and apply
any configuration settings.

The keywords `describe`, `let`, and `it` are keywords that are also used
in the RSpec DSL (domain-specific language). When you see these
keywords, you know you are looking at test code, either Minitest or
RSpec.

The purpose of a unit test is to describe the system under test, in
terms of its expected behavior. We create a `do ... end` block using the
`describe` keyword and specifying a class we wish to test:


```ruby
describe Visitor do
  .
  .
  .
end
```

### Create a Test Class With Describe

The `describe` keyword creates a test class. In this case, the
`describe` keyword will create a class named `VisitorTest` that inherits
from `ActiveSupport::TestCase`. Using the old test_unit syntax, we
could do this with `class VisitorTest < ActiveSupport::TestCase` but the
`describe` keyword is more convenient. When Minitest runs, it recognizes
and executes test classes. By including our code inside a test class, we
get to use methods such as `let` and `it` which are useful for writing
tests. Minitest will recognize various classes like models or
controllers and provide appropriate behavior.

### Setup Phase

We must set up everything we need for the test. Minitest provides a
simple way to set up everything before a test using the `before`
keyword:


```ruby
before do
  do_some_setup
end
```

We could initialize the Visitor model using a `before` block and setting
instance variables:


```ruby
before do
  @visitor_params = {email: 'user@example.com'}
  @visitor = Visitor.new(visitor_params)
end
```

Instead of using a `before` block, we'll use the convenient `let`
keyword:


```ruby
let(:visitor_params) { {email: 'user@example.com'} }
let(:visitor) { Visitor.new visitor_params }
```

The `let` keyword is a specialized version of the `before` keyword. It
caches the objects that you create so they are ready for every test you
write in the test class. And it is *lazy-loaded*, which means it does
not require any processing overhead until the first time it is used.

### Do It

Each test is defined by the `it` keyword and a `do ... end` block that
contains the exercise and verify phases of the test. The `it` keyword
must be accompanied by a description. The description will be displayed
if the test fails.

For our first test, we want to check if the Visitor model can be created
when we provide a valid email address. Before the test runs, the `let`
statement makes sure the Visitor object is instantiated with an email
value.

The verification phase of each test consists of a comparison between the
results of an operation and our expectations. We expect that each time
we create a Visitor object with a valid email address, the
`visitor.valid?` method will return true. We can create a test:


```ruby
it 'is valid when created with valid parameters' do
  assert_equal visitor.valid?, true
end
```

The keyword `assert_equal` is the old test_unit syntax. It compares the
result of `visitor.valid?` with `true` and tells Minitest the test has
passed or failed.

We can write the same thing using the new RSpec-style syntax:


```ruby
it 'is valid when created with valid parameters' do
  visitor.must_be :valid?
end
```

The method `must_be` is an <em>expectation</em>. You can see a [Minitest
cheat sheet](http://cheat.errtheblog.com/s/minitest) with a list of all
the expectation methods. As you might guess, `must_be`
functions as a comparison operator, checking if a call to
`visitor.valid?` returns true.

For our second test, we want to make sure the Visitor object is invalid
when no email address is provided:


```ruby
it 'is invalid without an email' do
  # Delete email before visitor let is called
  visitor_params.delete :email
  visitor.wont_be :valid? # Must not be valid without email
  visitor.errors[:email].must_be :present? # Must have error for missing email
end
```

We created the `visitor_params` hash with a `let` statement. Before we
invoke the Visitor object and call the `visitor.valid?` method, we
delete the email address from the `visitor_params` hash. When the
Visitor object is invoked, it will be created by the `let` statement
without an email address. The `wont_be` expectation confirms that the
result of `visitor.valid?` method is `false`. Then we check if a
validation error message is present.

At this point, don't expect to be ready to write unit tests for every
model method. You'll need to spend time with the [documentation for
Minitest
expectations](http://docs.seattlerb.org/minitest/Minitest/Expectations.html)
or the [Minitest cheat sheet](http://cheat.errtheblog.com/s/minitest) to
become familiar with all the possible ways to write tests. This
introduction should help you recognize the syntax of tests, understand
the structure, and give you the background you need to learn more about
unit testing.

Run Tests
---------

Let's run our unit tests:


```console
$ rails test
Running via Spring preloader in process 29585
Run options: --seed 7800

# Running:

..

Finished in 0.020289s, 98.5770 runs/s, 147.8655 assertions/s.

2 runs, 3 assertions, 0 failures, 0 errors, 0 skips
```

The output shows that our tests pass.

### Breaking the Test

Let's see what happens if we purposefully break our Visitor model.
Modify the file **app/models/visitor.rb**:


```ruby
class Visitor
  include ActiveModel::Model
  attr_accessor :email
  # validates_presence_of :email
  # validates_format_of :email, with: /\A[-a-z0-9_+\.]+\@([-a-z0-9]+\.)+[a-z0-9]{2,4}\z/i

  def subscribe
    mailchimp = Gibbon::Request.new(api_key: Rails.application.secrets.mailchimp_api_key)
    list_id = Rails.application.secrets.mailchimp_list_id
    result = mailchimp.lists(list_id).members.create(
      body: {
        email_address: self.email,
        status: 'subscribed'
    })
    Rails.logger.info("Subscribed #{self.email} to MailChimp") if result
  end

end
```

When you copy this, be careful to keep the long regex expression
(/\textbackslash{}A…\textbackslash{}z/i) on one line (no line breaks).

We've commented out the statements that require validation for the email
attribute. Let's run the tests again:


```console
$ rails test
Running via Spring preloader in process 29655
Run options: --seed 45089

# Running:

F

Failure:
Visitor#test_0002_is invalid without an email
[/Users/danielkehoe/workspace//learn-rails/test/models/visitor_test.rb:15]:
Expected #<Visitor:0x007fa5440a2260 @validation_context=nil,
@errors=#<ActiveModel::Errors:0x007fa5440a1f40 @base=#<Visitor:0x007fa5440a2260 ...>,
@messages={}, @details={}>> to not be valid?.

bin/rails test test/models/visitor_test.rb:12

.

Finished in 0.008457s, 236.4993 runs/s, 236.4993 assertions/s.

2 runs, 2 assertions, 1 failures, 0 errors, 0 skips
```

The output shows a failure. The diagnostic message displays the
description of the failing test, "Visitor#test_0002_is invalid
without an email", and indicates the line number where the test failed.
Now you know what a failing test looks like.

Before you continue, restore the file **app/models/visitor.rb** to its
original state, and make sure the tests pass.

If you wish, you can continue writing unit tests. You could create a
similar unit test for the Contact model. With more experience, or some
independent research, you could create a test for the `subscribe` method
in the Visitor model. This method connects to an external API, so it
requires test doubles to fake the response of the external services. Our
goal here is to introduce you to the concepts of testing, so we'll put
aside advanced work on unit tests, and take a look at feature tests.

Feature Test
------------

Let's start with a user story for our home page. It might seem trivial
to call the home page a "feature" and describe it with a user story, but
it illustrates a process that works just as well with more complex
features. Here's our user story:


```cucumber
*Feature: Home page*
  As a visitor
  I want to visit a home page
  And see a welcome message
```

For our test, we know we want to visit the home page and check if the
words "Stay in touch" appear on the page. This is the scenario we'll
test:


```cucumber
*Scenario: Visit the home page*
  Given I am a visitor
  When I visit the home page
  Then I see "Stay in touch"
```

If you think of your application as a collection of features, and you
describe each feature in terms of "As a (role), I want (goal), In order
to (benefit)," and then imagine scenarios for each feature using the
"Given…, When…, Then…" formula, you'll be able to write automated tests
to cover every feature in the application. Let's try it for the home
page.

Examine the folders within the **test/** directory. Remember that
feature tests are also called integration tests. You'll see a folder
**test/integration/**. That's where we'll add our feature tests.

Create a file **test/integration/home_page_test.rb**:


```ruby
require 'test_helper'

# Feature: Home page
#   As a visitor
#   I want to visit a home page
#   So I can learn more about the website
feature 'Home page' do

  # Scenario: Visit the home page
  #   Given I am a visitor
  #   When I visit the home page
  #   Then I see "Welcome"
  scenario 'visit the home page' do
    visit root_path
    page.must_have_content 'Stay in touch'
  end
end
```

I've included the user story and scenario description in comments.
There's no convention to do so, but it will help you to see the
relationship between testing and the product planning process. It should
be easy to transform a "Given… When… Then…" scenario into the code
needed for a feature test.

### Feature

When we created a unit test, we used the `describe` keyword to create a
test class. The `feature` keyword creates a test class that inherits
from the `Capybara::Rails::TestCase` class, giving us methods such as
`visit` and `page`.

Feature tests are created with a `do ... end` block using the `feature`
keyword and providing a description of the feature:


```ruby
feature 'Home page' do
  .
  .
  .
end
```

Notice that the description is placed in quotes. In this case, Minitest
will automatically generate a class named `HomePageTest`.

### Scenario

Typically we test a single feature with multiple scenarios in a single
test file.

The `scenario` keyword is similar to the `it` keyword you've seen in
unit tests. Each feature test is defined by the `scenario` keyword and a
`do ... end` block that contains the visit and verify phases of the
test. The `scenario` keyword must be accompanied by a description. The
description will be displayed if the test fails.


```ruby
scenario 'visit the home page' do
  visit root_path
  page.must_have_content 'Stay in touch'
end
```

The directive `visit` is a Capybara method that takes a URL or Rails
route as an argument. You could specify either `visit '/'` or
`visit root_path` to direct Capybara to retrieve the home page.

Capybara provides other *actions* in addition to `visit`. You can see
the [documentation for Capybara
actions](http://rubydoc.info/github/jnicklas/capybara/master/Capybara/Node/Actions)
that include actions for filling in a form and clicking a button.

Capybara creates a `page` object for us as a response to the visit. The
`page` object is a representation of the HTML file returned by the
application. We can call the `must_have_content` method, testing if the
string "Stay in touch" is present in the page.

Capybara gives us a collection of methods we can use to verify our
expectations. The [documentation for Capybara
expectations](http://blowmage.com/minitest-rails-capybara/Capybara/Expectations.html)
provides an extensive collection of methods we can use to verify what's
on a web page. For example, `must_have_link` checks for a link. With
Capybara expectations, you can check almost anything on a page.
Combining Capybara actions and expectations allows you to build a
powerful page-checking robot.

Run Tests
---------

Let's run all our tests:


```console
$ rails test
Running via Spring preloader in process 30144
Run options: --seed 51858

# Running:

...

Finished in 0.459255s, 6.5323 runs/s, 8.7098 assertions/s.

3 runs, 4 assertions, 0 failures, 0 errors, 0 skips
```

We have three tests (in two test files) making four assertions, all
passing.

### Troubleshooting

You might get an error message:


```console
rails aborted!
NoMethodError: undefined method `feature' for main:Object
```

You'll see this error message if you neglected to modify the
**test/test_helper.rb** file to allow use of the Capybara test
framework methods.

### Breaking the Test

Let's see what happens if we purposefully break our home page. Modify
the file **app/view/visitors/new.html.erb**:


```ruby
<% content_for :title do %>Foobar Kadigan<% end %>
<% content_for :description do %>Website of Foobar Kadigan<% end %>
<section>
  <img src="http://lorempixel.com/1170/600/cats/1">
</section>
<section>
  <div class="column">
    <h3>GO AWAY!</h3>
  </div>
  <div class="column">
    <div class="form-centered">
      <%= form_with(model: @visitor) do |f| %>
        <%= f.email_field :email, placeholder: 'Your email address...', autofocus: true %>
        <br/>
        <br/>
        <%= f.submit 'Sign up for the newsletter', class: 'submit' %>
      <% end %>
    </div>
  </div>
</section>
```

We've changed the welcome message from "Stay in touch" to "GO AWAY!".

Let's run the tests again:


```console
$ rails test
Running via Spring preloader in process 30059
Run options: --seed 39958

# Running:

F

Failure:
Home page Feature Test#test_0001_visit the home page
[/Users/danielkehoe/workspace//learn-rails/test/integration/home_page_test.rb:15]:
Expected to find text "Stay in touch" in "Toggle navigation Home About Contact GO AWAY!".

bin/rails test test/integration/home_page_test.rb:13

..

Finished in 5.124522s, 0.5854 runs/s, 0.7806 assertions/s.

3 runs, 4 assertions, 1 failures, 0 errors, 0 skips
```

The output shows a failure. The diagnostic message displays the
description of the failing test, "Home page Feature
Test#test_0001_visit the home page", showing a failure, "Expected to
include 'Stay in touch'."

Before you continue, restore the file **app/view/visitors/new.html.erb**
to its original state, and make sure the tests pass.

Now that we have written a few basic tests, let's commit our changes
to the Git repository and push to GitHub:

```console
$ git add -A
$ git commit -m "add tests"
$ git push
```
You've written a complete application with tests. Very good!

### Using Capybara

There is an art to developing feature tests. You can test that all the
text on the home page is exactly what you want. That would make your
test files large. And your tests would be "brittle," because any changes
you made in development, even the slightest changes to the words on the
page, would break your tests. For good integration tests, focus on the
features that are essential to your application. For example, use the
Capybara robot to make sure the user can follow a critical path through
your application, visiting important pages, filling in forms, clicking
buttons, and seeing results. Capybara lets you select any HTML element
on a page, so you can check an ID or class attribute of an HTML tag, not
just text on a page. You'll want to be confident that application
navigation and page flow continues to work after any code changes. That
will serve you better than tests that tell you a word changed here or
there.

Other Tests
-----------

The art of testing lies in making good choices about what to test. It's
common to write feature tests because they will test the entire
application from the viewpoint of the user. It is also common to write
unit tests for models because models contain much of the uniqueness of
an application.

Every other aspect of a Rails application can be tested, including
controllers, helpers, and views. Developers seldom write tests for every
aspect of a Rails application. If your controllers contain only the
standard RESTful actions, with no extra logic, you probably don't need
to write unit tests for your controllers. If you only have simple HTML
markup in helpers, helpers don't need to be tested. And views are rarely
tested with unit tests (use feature tests if you want to make sure a
page contains what you expect). As a beginner, you'll make a good start
if you concentrate on unit tests for models and integration tests for
your page flow.

Behavior-Driven Development
---------------------------

In Book One, you learned about the software
development approach called Behavior-Driven Development (BDD), or
sometimes, Behavior-Driven Design. In writing the feature tests for the
home page, you saw it in action. With BDD, you turn user stories into
detailed scenarios that are accompanied by tests. BDD is a powerful
approach for managing software development. It helps you define your
product requirements, refine your project scope, and divide your project
into well-defined tasks. The BDD process is complete when each feature
has automated tests, when you enter `rails test` on the command line and
see that every feature is implemented and functioning as expected.

You may feel lost or overwhelmed when you attempt to build a Rails
application for the first time, especially if your only experience is
following the step-by-step instructions of a tutorial. When you
experience that panic, BDD is your lifeline. Start by writing user
stories for a few simple features. Write feature tests and implement the
code required to make the tests pass. As you focus on the process of
writing scenarios and tests, and implementing the code for each feature,
you'll begin to gain momentum, and before you know it, you'll be over
the first hurdle.

Test-Driven Development
-----------------------

You can see how the BDD approach refines the product requirements and
user experience. At a microscopic level, a similar discipline, named
*test-driven development*, helps refine the implementation. Where BDD is
driven by feature tests, TDD is focused on unit tests.

TDD is an approach to software development that emphasizes that all code
should be written to be tested. Excellent test coverage, allowing easy
refactoring, is not the only goal of TDD. Just as important, the
developer focuses on what needs to be accomplished and thinks through
alternatives and edge cases. Some TDD aficionados say testing is a tool
to write better code, and regression tests are a side effect. Unit tests
are at the heart of TDD, and easiest to write when code is carefully
decoupled into systems that can be tested in isolation. An application
that is composed of decoupled units with clearly defined interfaces is a
well-designed application that is easy to extend and maintain. If you
make it a practice to write unit tests in conjunction with all the code
you write, you'll write better code, and you'll be practicing TDD.

Test-First Development
----------------------

Often when you are practicing TDD, you'll write tests before you write
implementation code. Earlier in this chapter, I referred to *test-first
development* and explained that it serves a different purpose than
testing for quality assurance. In some situations, test-first
development is simply exploratory testing, a means of describing the
behavior of the code that must be built. Test-first development is
particularly useful when you've solved a similar problem and know
exactly what results to expect, making it easy to write tests before
writing the implementation.

Test-first development leads to a "red-green-refactor" workflow. A
developer imagines the results of an operation, writes a test that
checks for the results, and runs tests which fail (with the right
configuration, failing tests display as red in the console). Then the
developer writes code that produces the correct results and runs the
tests again, improving the code until the tests pass (displaying in
green). At this point, the developer has an adequate regression test and
can begin to refactor to improve the implementation, checking that the
tests continue to pass. Developers like the rhythm and coherency of the
"red-green-refactor" workflow. Writing tests creates discrete,
manageable tasks. When tests pass, turning green, there is a feeling of
satisfaction, of a job well-done. By postponing concerns about improving
the code to a refactoring phase, it's easier to get the job done without
trying to get it perfect. And perfection can be pursued in the
refactoring phase without worrying about regressing to a broken state.

David Heinemeier Hansson, the creator of Rails, famously declared that
[TDD is dead. Long live testing.](http://david.heinemeierhansson.com/2014/tdd-is-dead-long-live-testing.html).
He pointed out that sometimes ardent advocates of TDD will try out an
implementation before writing tests, to determine what needs to be done,
or to clarify a problem. In the real world, even though developers
recommend writing tests first, there are often times when a developer
will write tests only after writing code and settling on an approach.
TDD, which emphasizes the benefit of writing tests as a first step,
doesn't really require that you write tests before you write code, or
even that you write tests for all code. The test-first emphasis of TDD
is a recommendation, not a rule. You'll be a better developer if you
find opportunities to get "in the zone" with the red-green-refactor
workflow of test-first development, but testing is worthwhile whether it
comes first or last.

Words of Encouragement
----------------------

Testing often intimidates the newcomer. It is difficult to find good
examples. The syntax of Minitest and RSpec has evolved over time, so
there is little consistency among examples you'll find. Older examples
are not a good guide to current practices. But once you gain familiarity
with the concepts in this chapter, you can start writing tests.

Testing is one of the few things in Rails that you can jump into without
getting just right. You can't screw up your code base by writing
incorrect tests. Experienced developers seem to worry that inexperienced
developers will write slow tests, but in truth, a slow test is better
than no test. Tests won't affect the performance of your application in
production.

If your code is clumsy, don't worry, you'll get better with practice.
What's most important is that you've begun writing tests. That's an
indication you are committed to Rails best practices.

Your tests are only "bad" if they don't cover your code adequately or if
they give you a false sense of assurance. You will only discover this
over time, as you find bugs you didn't anticipate (which is inevitable).
It's better to just begin testing, even if you're not sure you're doing
it right, than to not test at all.
