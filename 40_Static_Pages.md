Static Pages and Routing
========================

A Rails application can deliver static web pages just like an ordinary
web server. The pages are delivered fast and no Ruby code is required.
We'll look at simple static pages and learn about Rails routing before
we explore the complexities of dynamic web pages in Rails.

Add a Home Page
---------------

Make sure you are in your project directory.

Start the application server:


```console
$ rails server
```

Open a web browser window and navigate to
[http://localhost:3000/](http://localhost:3000). You'll see the Rails
default information page.

For the next step, you'll need to know how to use a text editor such as
[Atom](https://atom.io/) or [Sublime Text](http://www.sublimetext.com/).
You can find free tutorials on YouTube. Or, if you prefer a book, try Michael Hartl's
[Learn Enough Text Editor to Be Dangerous](https://www.learnenough.com/text-editor-tutorial).

Use your text editor to create and save a file **public/index.html**:


```html
<h1>Hello World</h1>
```

Refresh the browser window and you'll see the "Hello World" message.

The Rails application server looks for any pages in the **public**
folder by default.

If no filename is specified in the URL, the server will attempt to
respond with a file named **index.html**. This is a convention that
dates to 1993; if no filename was specified, one of the first web
servers ever built (the NCSA httpd server) would return a list of all
files in the directory, unless a file named **index.html** was present.
Since then, **index.html** has been the default filename for a home
page.

Routing Error
-------------

What happens when no file matches the requested web address?

Enter the URL
[http://localhost:3000/about.html](http://localhost:3000/about.html) in
your browser.

You'll see an error page that shows a routing error.

If you are using Cloud9, add "/about.html" to the URL in the preview
browser window.

Add an About Page
-----------------

Use your text editor to create and save a file **public/about.html**:


```html
<h1>About</h1>
```

Visit the URL
[http://localhost:3000/about.html](http://localhost:3000/about.html) in
your browser. You'll see the new "About" page.

By the way, you've just done test-driven development (TDD).

### Introducing TDD

With test-driven development, a developer tests behavior before
implementing a feature, expecting to see an error condition. Then the
developer implements the feature and sees a successful result to the
test. That's exactly what you've done, in the simplest way.

Beginners tend to think TDD is scary and complicated. Now that you've
experienced a simple form of TDD, maybe it won't be intimidating. Real
TDD means writing tests in Ruby before implementing features, but the
principle is the same.

Introducing Routes
------------------

The guiding principle of "convention over configuration" governs Rails
routing. If the web browser requests a page named "index.html", Rails
will deliver the page from the **public** folder by default. No
configuration is required. But what if you want to override the default
behavior? Rails provides a configuration file to control web request
routing.

If you've got only one terminal window open, you'll have to stop the Rails server with Control-c to get your terminal prompt. Here is where it is helpful to have two terminal sessions going in different tabs.

Let's set the "About" page as the home page.

Open the file **config/routes.rb**. Remove all the comments and replace
the file with this:


```ruby
Rails.application.routes.draw do
  root to: redirect('/about.html')
end
```

This snippet of Rails routing code takes any request to the application
root ([http://localhost:3000/](http://localhost:3000/)) and redirects it
to the **about.html** file (which is expected to be found in the
**public** folder).

There is no need to restart your application server to see the new
behavior. If you need to start the server:


```console
$ rails server
```

Visit the page [http://localhost:3000/](http://localhost:3000). You'll
see the "About" page.

If you still see the "Hello World" page, you didn't remove the the **public/index.html** file.
Rails will use the index file in the public folder before it checks the routing file for a redirect.

You've just seen an example of Rails magic. Some developers complain
that the "convention over configuration" principle is black magic. It's
not obvious why pages are delivered from the **public** folder; it just
happens. If you don't know the convention, you could be left scratching
your head and looking for the code that maps
[http://localhost:3000/](http://localhost:3000/) to the
**public/index.html** file. The code is buried deep in the Rails
framework. However, if you know the convention and the technique for
overriding it, you have both convenience and power at your disposal.

Using the "About" Page
----------------------

We've created an "About" page so we can learn about routing.

For the next chapter, we'll use the static "About" page to investigate
how a web application works.

Later in the tutorial we'll create a new "About" page using a different
approach.
