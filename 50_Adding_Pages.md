Add Pages
=========

Let's begin adding pages to our web application.

There are three types of web pages in a Rails application. We've looked
at two types so far:

-   static pages in the **public/** folder that contain no Ruby code
-   dynamic pages such as our home page that use the application layout

There's another type of web page that is required on many websites. It
has static content; that is, no dynamic data is needed on the page. But
it uses the default application layout to maintain consistency in the
website look and feel. We classify this type of page as a:

-   static view that uses the application layout

Examples include:

-   "About" page
-   Legal page
-   FAQ page

It's possible to place these pages in the **public/** folder and copy
the HTML and CSS from the default application layout but this leads to
duplicated code and maintenance headaches. And dynamic elements such as
navigation links can't be included. For these reasons, developers seldom
create static pages in the **public/** folder.

Alternatively, a dynamic page can be created that has no model, a
nearly-empty controller, and a view that contains no instance variables.
This solution is quite common for static views that use the application
layout.

This solution is implemented so frequently that many developers create a
gem to encapsulate the functionality. We're going to use the best-known
of these gems, the [high_voltage
gem](https://github.com/thoughtbot/high_voltage) created by the
[Thoughtbot](http://www.thoughtbot.com/) consulting firm.

We'll use the High Voltage gem to create an "About" Page.

We also will create a Contact page. We'll again use the High Voltage
gem, but only for the first version of the Contact page. Later we'll
discard the page we created with the High Voltage gem and replace it
with a full model-view-controller implementation. The process will show
the difference between an older form of web application architecture and
a newer "Rails way."

High Voltage Gem
----------------

We can add a page using the High Voltage gem almost effortlessly. The
gem implements Rails "convention over configuration" so well that there
is nothing to configure. There are alternatives to its defaults which
can be useful but we won't need them; visit the GitHub home page for the
[high_voltage gem](https://github.com/thoughtbot/high_voltage) if you
want to explore all the options.

In your **Gemfile**, you've already added:


```ruby
gem 'high_voltage'
```

and previously run `$ bundle install`.

Views Folder
------------

Create a folder **app/views/pages**:


```console
$ mkdir app/views/pages
```

Any view files we add to this directory will automatically use the
default application layout and appear when we use a URL that contains
the filename.

The High Voltage gem contains all the controller and routing magic
required for this to happen.

Let's try it out.

"About" Page
------------

Create a file **app/views/pages/about.html.erb**:


```erb
<% content_for :title do %>About<% end %>
<h3>About Foobar Kadigan</h3>
<p>He was born in Waikikamukau, New Zealand. He left New Zealand for England,
  excelled at the University of Mopery, and served in the Royal Loamshire Regiment.
  While in service, he invented the kanuten valve used in the processing of
  unobtainium for industrial use. With a partner, Granda Fairbook, he founded
  Acme Manufacturing, later acquired by the Advent Corporation, to develop his
  discovery for use in the Turboencabulator. Mr. Kadigan is now retired and
  lives in Middlehampton with a favorite cat, where he raises Griadium frieda
  and collects metasyntactic variables.</p>
<p>His favorite quotation is:</p>
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
  tempor incididunt ut labore et dolore magna aliqua.</p>
```

Our simple "About" view will be combined with the default application
layout by the High Voltage gem.

We include a `content_for` Rails view helper that passes a page title to
the application layout.

Contact Page
------------

For the initial version of the Contact page, create a file
**app/views/pages/contact.html.erb**:


```erb
<% content_for :title do %>Contact<% end %>
<h3>Contact</h3>
```

This is a placeholder page we'll use to test a navigation link.

We include a `content_for` Rails view helper that passes a page title to
the application layout.

Routing for the High Voltage Gem
--------------------------------

The High Voltage gem provides a PagesController. You'll never see it; it
is packaged inside the gem.

In addition to providing a controller, the High Voltage gem provides
default routing so any URL with the form
[http://localhost:3000/pages/about](http://localhost:3000/pages/about)
will obtain a view from the **app/views/pages** directory.

Like the PagesController, the code that sets up the route is packaged
inside the gem. For details about the syntax of routing directives,
refer to [RailsGuides: Routing from the Outside
In](http://guides.rubyonrails.org/routing.html).

Update the Navigation Partial
-----------------------------

You can use a Rails route helper to create a link to any view in the
**app/views/pages** directory like this:


```erb
link_to 'About', page_path('about')
```

Let's add links to the "About" and "Contact" pages.

Replace the contents of the file
**app/views/layouts/_navigation_links.html.erb** with this:


```erb
<%# add navigation links to this file %>
<li><%= link_to 'About', page_path('about') %></li>
<li><%= link_to 'Contact', page_path('contact') %></li>
```

With an updated navigation bar, we can test the application.

Test the Application
--------------------

The web server may already be running. If not, enter the command:


```console
$ rails server
```

Open a web browser window and navigate to
[http://localhost:3000/](http://localhost:3000).

Links to the pages "About" and "Contact" should work.

If you get an error "uninitialized constant PagesController," make sure
the **config/routes.rb** file looks like this:


```ruby
Rails.application.routes.draw do
  root to: 'visitors#new'
end
```

Watch what happens when you resize the page. At smaller sizes, the
navigation bar changes to display a menu icon. Clicking the menu icon
reveals a drop-down menu of navigation links. You're seeing the power of
the Bootstrap framework.

Here's a troubleshooting tip. If clicking the menu icon doesn't reveal a
drop-down menu, the application may not be loading the Bootstrap
JavaScript library. Make sure that the file
**app/assets/javascripts/application.js** contains:


```js
//= require jquery
//= require jquery_ujs
//= require turbolinks
//= require bootstrap-sprockets
//= require_tree .
```

Git
---

Let's commit our changes to the Git repository and push to GitHub:


```console
$ git add -A
$ git commit -m "add 'about' and 'contact' pages"
$ git push
```

There is nothing more we need for our "About" page.

In the next chapter, we'll explore two different implementations for the
Contact page.
