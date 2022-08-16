Front-End Framework
===================

This chapter discusses front-end development and design using CSS. I'll
show you how to add style to a Rails application, using Bootstrap
for a simple theme.

What do we mean by "front-end development"? A website *back end* is the
Rails application that assembles files that are sent to the browser,
plus a database and any other server-side services. A website *front
end* is all the code that runs in the browser. Everything that controls
the appearance of the website in the browser is the responsibility of a
front-end developer, including page layout, CSS stylesheets, and
JavaScript code.

Front-end development has grown increasingly important as websites have
become more sophisticated. And front-end technology has grown
increasingly complex, to the degree that front-end development has
become a job for specialists.

Front-end developers are primarily concerned with:

-   markup - the layout and structure of the page
-   style - graphic design for visual communication
-   interactivity - browser-based visual effects and user interaction

Broader concerns include:

-   cross-browser and cross-device functionality
-   interaction design to improve website usability
-   accessibility for users with physical or perceptual limitations

For years, front-end development was haphazard; webmasters each had
their own quirky techniques. Around the time that Rails became popular,
front-end developers at large companies began to share best practices
and establish open source projects to bring structure and consistency to
front-end development, leading to development of CSS frameworks.

CSS Frameworks
--------------

Web developers began putting together "boilerplate" CSS stylesheets as
early as 2000, when browsers first began to fully support CSS.
Boilerplate CSS made it easy to reuse CSS stylesheet rules from project
to project. More importantly, designers often implemented "CSS reset"
stylesheets to enforce typographic uniformity across different browsers.

Engineers at Yahoo! released the [Yahoo! User Interface
Library](http://yuilibrary.com/) (YUI) as an open source project [in
February 2006](http://www.yuiblog.com/blog/2006/02/). Inspired by an
[article by Jeff
Croft](http://web.archive.org/web/20080516101830/http://www.alistapart.com/articles/frameworksfordesigners/),
and reacting to the huge size of the YUI library, independent developers
began releasing other CSS frameworks such as the [960 grid
system](http://960.gs/) and the
[Blueprint](http://www.blueprintcss.org/) CSS framework.

There are [dozens of CSS
frameworks](http://en.wikipedia.org/wiki/CSS_frameworks). In general,
they all seek to implement a common set of requirements:

-   An easily customizable grid
-   Some default typography
-   A typographic baseline
-   CSS reset for default browser styles
-   A stylesheet for printing

More recently, with the ubiquity of smartphones and tablets, CSS
frameworks support [responsive web
design](http://en.wikipedia.org/wiki/Responsive_web_design),
accommodating differences in screen sizes across a range of devices.

In tandem with the development of CSS frameworks, we've seen the
emergence of JavaScript libraries and frameworks.

JavaScript Libraries and Frameworks
-----------------------------------

JavaScript has nothing like RubyGems, a built-in package manager for
code libraries, so initially there were few open source JavaScript
libraries. Now there are several competing [JavaScript package
managers](http://wibblycode.wordpress.com/2013/01/01/the-state-of-javascript-package-management/)
and many software libraries.

[Prototype](http://en.wikipedia.org/wiki/Prototype_JavaScript_Framework)
was one of the first open source JavaScript libraries, created by Sam
Stephenson in February 2005 to improve JavaScript support in Ruby on
Rails. [MooTools](http://en.wikipedia.org/wiki/MooTools),
[Dojo](http://en.wikipedia.org/wiki/Dojo_Toolkit), and
[jQuery](http://en.wikipedia.org/wiki/Jquery) soon followed. Of these
libraries, jQuery has become the most popular, largely because of
thousands of modular jQuery *plug-ins* that implement a wide range of
effects and *widgets* (web page features). These plug-ins are used to
add visual effects and interactivity to web pages. Examples are
drop-down menus, modal windows, tabbed panels, autocompletion search
forms, and sliders or carousels for images. Even without plugins, jQuery
is useful as a high-level interface for manipulating the browser DOM
([document object
model](http://en.wikipedia.org/wiki/Document_Object_Model)), to make it
easy to do things like hiding or revealing HTML elements on a page. Any
Rails application can use jQuery because it is included by default in
any new Rails application.

Libraries such as jQuery add functionality to server-side applications,
such as those built with Rails. Other JavaScript libraries serve as
fully featured web application development frameworks, allowing
developers to build client-side applications that run in the browser and
only interact with a server to read or write data. Examples of these
full-fledged JavaScript frameworks are [Ember.js](http://emberjs.com/),
[AngularJS](http://www.angularjs.org/), and
[Backbone.js](http://backbonejs.org/). All use a variant of the
model-view-controller (MVC) software design pattern to implement
[single-page applications](http://en.wikipedia.org/wiki/Single-page_application)
which function more like desktop or mobile applications than websites.
Developers who build a single-page application with one of these
frameworks often use Ruby on Rails as a back end; an MVC JavaScript
framework can replace all the Rails view files. None of these JavaScript
frameworks dominate web application development like Ruby on Rails, but
they are gaining popularity for single-page applications. We won't look at Ember.js, AngularJS, or Backbone.js
in this book; they are an advanced topic and require entire books
themselves.

The biggest problem with adding JavaScript to Rails is the difficult-to-maintain
"JavaScript soup" that results from adding JavaScript to Rails views.
Ember.js, AngularJS, or Backbone.js are more than is needed for simply
structuring JavaScript in Rails views. But there's a newer framework that can be
used to dry up JavaScript soup. It's
[React](http://reactjs.com/), a JavaScript framework developed by engineers at Facebook.
Unlike AngularJS or Ember.js, React only manages views, not connections to databases or routing of requests, so it is not a full-stack framework, just a framework for the view layer. React's approach to building web pages is abstract and complex. But React is a good choice for complex interactive features, if you're determined to avoid JavaScript soup in your Rails application.

We won't look at JavaScript frameworks in this book, but we will use the Bootstrap framework to manage
our CSS stylesheets.

Front-End Frameworks
--------------------

Front-end frameworks combine CSS and JavaScript libraries. Many elements
that are found on sophisticated web pages, such as modal windows or
tabs, require a combination of JavaScript and CSS. Combining CSS and
JavaScript libraries in a common framework makes it possible to
standardize and reuse common web page features.

There are many responsive front-end frameworks to choose from,
including:

-   [Bootstrap](http://getbootstrap.com/)
-   [Zurb Foundation](http://foundation.zurb.com/)
-   [Material Design Lite](https://getmdl.io/)
-   [Bourbon Neat](http://neat.bourbon.io/)
-   [Semantic UI](http://semantic-ui.com/)
-   [and many others](http://speckyboy.com/2013/10/13/15-new-responsive-frameworks/)

Each has its fans, though Bootstrap and Zurb Foundation are the most
popular among Rails developers. Each adds a library of markup, styles,
and standardized web page features such as modal windows, pagination,
breadcrumbs, and navigation.

[Bootstrap](http://getbootstrap.com/) is the best-known front-end
framework. It is the result of an effort to document and share common
design patterns and assets across projects at Twitter, released as an
open source project in August 2011.

Just ahead, we'll look at why we use Bootstrap in this book. But
first, you'll need to learn about Sass.

CSS Preprocessing with Sass
-----------------------------------

Ordinary CSS is not a programming language. As a result, CSS rules are
verbose and often repetitive. To add efficiency to CSS, Bootstrap
relies on a CSS preprocessor named [Sass](http://sass-lang.com/).
Sass extends CSS to give it more powerful
programming language features. As a result, your stylesheets can use
variables, mixins, and nesting of CSS rules, just like a real
programming language.

For example, in Sass you can create a variable such as `$blue: #3bbfce`
and specify colors anywhere using the variable, such as
`border-color: $blue`. *Mixins* are like variables that let you use
snippets of reusable CSS. *Nesting* eliminates repetition by layering
CSS selectors.

Sass is included in any new Rails application with the default [sass-rails](https://github.com/rails/sass-rails) gem.

Bootstrap or Others?
-----------------------------

Which front-end framework should you use? Bootstrap or another such as Zurb Foundation?

The Bootstrap team maintains a Ruby gem that provides a drop-in version of Bootstrap for Rails.
Other front-end frameworks, such as Zurb Foundation, are also available as Ruby gems. But
Bootstrap has a large developer community and many more third-party
projects, as evidenced by a [Big Badass List of Useful Twitter Bootstrap
Resources](http://www.bootstraphero.com/the-big-badass-list-of-twitter-bootstrap-resources/).
In its sheer magnitude, this list, from Michael Buckbee and Bootstrap
Hero, demonstrates the popularity of Bootstrap and the vitality of its
open source community. We'll use Bootstrap here because of its sheer popularity
and solid support.

Before I show you how to integrate Bootstrap with your Rails
application, let's briefly consider matters of design.

Graphic Design Options
----------------------

There are three approaches to graphic design for your Rails application.

If you're well-funded and well-connected, you can put together a team or
hire a freelance graphic designer to implement a unique design, built
from scratch using CSS or customized from a framework such as Bootstrap
or Zurb Foundation. If you've got strong design skills, or can partner
with an experienced web designer, you'll get a custom design that
expresses the purpose and motif of your website.

A second approach is to use Bootstrap or another CSS framework to quickly add
attractive CSS styling to your application. Many developers don't have
the skill or resources to customize the design. Consequently, sites that
use Bootstrap look very similar. If that's your
situation, it's okay, really! It's better to have a decent site with the
clean look of Bootstrap than to leak ugliness onto the web.

A third option is to obtain a pre-designed theme for your website. You
may have visited [ThemeForest](http://themeforest.net/) or other theme
galleries that offer pre-built themes for a few dollars each. These huge
commercial galleries offer themes for WordPress, Tumblr, or CMS
applications such as Drupal or Joomla. They don't offer themes for Rails.
Your best option is to convert open source themes designed with Bootstrap.
You can visit sites such as [Start Bootstrap](https://startbootstrap.com/),
[Bootswatch](http://bootswatch.com/), or the
[Themestrap](http://code.divshot.com/themestrap/) gallery to find Bootstrap themes.

Whether you use a prepackaged theme or design your own layout, you'll need to know how to set up a
front-end framework in Rails. We'll look at setting up Bootstrap next.

Bootstrap 3 or 4?
-------------------

At the time this was written, the new Bootstrap 4 version was in alpha release. The Bootstrap 4 version
is significantly different from earlier versions. It has been in alpha for testing and feedback for over a year. Many Rails developers are already using the Bootstrap 4 version but almost all themes and third-party add-ons are
only available for Bootstrap 3. Eventually, the Bootstrap 4 beta and final versions will be released but
until then, I recommend sticking with Bootstrap 3. As a beginner, you'll find more resources and help for
Bootstrap 3. We'll use it here for this tutorial.

Bootstrap Gem
-------------------

Bootstrap provides a standard grid for layout plus dozens of
reusable components for common page elements such as navigation, forms,
and buttons. More importantly, it gives CSS the kind of structure and
convention that makes Rails popular for back-end development. Bootstrap is packaged as a gem.

In your **Gemfile**, you've already added:

```ruby
gem 'bootstrap-sass'
```

and previously run `$ bundle install`.

The [bootstrap-sass gem](https://github.com/twbs/bootstrap-sass) provides the files required to integrate Bootstrap 3 with Rails. Developers who want to use the new Bootstrap 4 release will use the [Bootstrap 4 gem](https://github.com/twbs/bootstrap-rubygem).

Rather than following the installation instructions provided in the
[Bootstrap documentation](http://getbootstrap.com/getting-started/), we'll
use the [rails_layout](https://github.com/RailsApps/rails_layout) gem
to set up Bootstrap and create the files we need.

Rails Layout Gem with Bootstrap
-------------------------------------

In the previous chapter, we used the
[rails_layout](https://github.com/RailsApps/rails_layout) gem to
configure the default application layout with HTML5 elements, navigation
links, and flash messages. Now we'll use the rails_layout gem to set up
Bootstrap and generate new files for the application layout as
well as the navigation and messages partials. The new files will replace
the layout files we created in the previous chapter.

We'll use the generator provided by the rails_layout gem to set up
Bootstrap and add the necessary files. Run:


```console
$ rails generate layout:install bootstrap3 --force
```

With the `--force` argument, the rails_layout gem will replace existing
files.

The gem will create the file:

-   **app/assets/stylesheets/1st_load_framework.css.scss**

and modify the files:

-   **app/assets/javascripts/application.js**
-   **app/views/layouts/_messages.html.erb**
-   **app/views/layouts/_navigation.html.erb**
-   **app/views/layouts/application.html.erb**

It will also remove the file:

-   **app/assets/stylesheets/simple.css**

Let's examine the files to see how our application is configured to use
Bootstrap.

Renaming the application.css File
---------------------------------

The rails_layout gem renamed the
**app/assets/stylesheets/application.css** file as
**app/assets/stylesheets/application.css.scss**. Note the **.scss** file
extension. This will allow you to use the advantages of an improved
syntax for your application stylesheet.

You learned earlier that stylesheets can use variables, mixins, and
nesting of CSS rules when you use Sass.

Sass has two syntaxes. The most commonly used syntax is known as "SCSS"
(for "Sassy CSS"), and is a superset of the CSS syntax. This means that
every valid CSS stylesheet is valid SCSS as well. SCSS files use the
extension **.scss**. The Sass project also offers a second, older syntax
with indented formatting that uses the extension **.sass**. We'll use
the SCSS syntax.

You can use Sass in any file by adding the file extension **.scss**. The
asset pipeline will preprocess any **.scss** file and expand it as
standard CSS.

For more on the advantages of Sass and how to use it, see the
[Sass](http://sass-lang.com/) website or the [Sass Basics
RailsCast](http://railscasts.com/episodes/268-sass-basics) from Ryan
Bates.

Before you continue, make sure that the rails_layout gem renamed the
**app/assets/stylesheets/application.css** file as
**app/assets/stylesheets/application.css.scss**. Otherwise you won't see
the CSS styling we will apply.

The application.css.scss File
-----------------------------

In the previous chapter, I introduced the Rails *asset pipeline*.

Your CSS stylesheets get concatenated and compacted for delivery to the
browser when you add them to this directory:

-   **app/assets/stylesheets/**

The asset pipeline helps web pages display faster in the browser by
combining all CSS files into a single file (it does the same for
JavaScript).

Let's examine the file **app/assets/stylesheets/application.css.scss**:


```sass
/*
 * This is a manifest file that'll be compiled into application.css, which will include all the files
 * listed below.
 *
 * Any CSS and SCSS file within this directory, lib/assets/stylesheets, or any plugin's
 * vendor/assets/stylesheets directory can be referenced here using a relative path.
 *
 * You're free to add application-wide styles to this file and they'll appear at the bottom of the
 * compiled file so the styles you add here take precedence over styles defined in any other CSS/SCSS
 * files in this directory. Styles in this file should be added after the last require_* statement.
 * It is generally better to create a new file per style scope.
 *
 *= require_tree .
 *= require_self
 */
```

The **app/assets/stylesheets/application.css.scss** file serves two
purposes.

First, you can add any CSS rules to the file that you want to use
anywhere on your website. Second, the file serves as a *manifest*,
providing a list of files that should be concatenated and included in
the single CSS file that is delivered to the browser.

If you are familiar with CSS syntax, it may seem odd that the relevant
lines are commented out (using asterisks). These lines are not CSS, so
they must be commented out so they won't be interpreted as CSS. Though
they are commented out, the Rails asset pipeline reads and understands
them. It's a bit of a hack, but it works.

### A Global CSS File

Any CSS style rules that you add to the
**app/assets/stylesheets/application.css.scss** file will be available
to any view in the application. You could use this file for any style
rules that are used on every page, particularly simple utility rules
such as highlighting or resetting the appearance of links. However, in
practice, you are more likely to modify the style rules provided by Bootstrap.
 These modifications don't belong in the
**app/assets/stylesheets/application.css.scss** file; they will go in
the **app/assets/stylesheets/1st_load_framework.css.scss** file.

In general, it's bad practice to place a lot of CSS in the
**app/assets/stylesheets/application.css.scss** file (unless your CSS is
very limited). Instead, structure your CSS in multiple files. CSS that
is used on only a single page can go in a file with a name that matches
the page. Or, if sections of the website share common elements, such as
themes for landing pages or administrative pages, make a file for each
theme. How you organize your CSS is up to you; the asset pipeline lets
you organize your CSS so it is easier to develop and maintain. Just add
the files to the **app/assets/stylesheets/** folder.

### A Manifest File

It's not obvious from the name of the
**app/assets/stylesheets/application.css.scss** file that it serves as a
*manifest file* as well as a location for miscellaneous CSS rules. For
most websites, you can ignore its role as a manifest file. In the
comments at the top of the file, the `*= require_self` directive
indicates that any CSS in the file should be delivered to the browser.
The `*= require_tree .` directive (note the Unix "dot operator")
indicates any files in the same folder, including files in subfolders,
should be combined into a single file for delivery to the browser.

If your website is large and complex, you can remove the
`*= require_tree .` directive and specify individual files to be
included in the file that is generated by the asset pipeline. This gives
you the option of reducing the size of the application-wide CSS file
that is delivered to the browser. For example, you might segregate a
file that includes CSS that is used only in the site's administrative
section. In general, only large and complex sites need this
optimization. The speed of rendering a single large CSS file is faster
than fetching multiple files.

Bootstrap JavaScript
--------------------------

Bootstrap provides both CSS and JavaScript libraries.

Like the **application.css.scss** file, the **application.js** file is a
manifest that allows a developer to designate the JavaScript files that
will be combined for delivery to the browser.

The rails_layout gem modified the file
**app/assets/javascripts/application.js** to include jQuery and the Bootstrap
JavaScript libraries:


```js
//= require jquery
//= require jquery_ujs
//= require turbolinks
//= require bootstrap-sprockets
//= require_tree .
```

It added the directives `//= require jquery` and `//= require jquery_ujs` to
make jQuery available to the application.

Keep in mind that Rails 5.1 dropped jQuery and no longer includes the [jquery-rails](https://github.com/rails/jquery-rails)
gem by default. We added the jquery-rails gem to the Gemfile (and ran `bundle install`).
Without the jquery-rails gem, you'll get an error when you run the application.

The rails_layout command also added the directive `//= require bootstrap-sprockets` before
`//= require_tree .` to enable the Bootstrap front-end framework.
Some of the features offered by Bootstrap require the jQuery library which is
why the rails_layout command modifies the **app/assets/javascripts/application.js** file.

Bootstrap CSS
-------------------

The rails_layout gem added a file
**app/assets/stylesheets/1st_load_framework.css.scss** containing:


```scss
// import the CSS framework
@import "bootstrap-sprockets";
@import "bootstrap";
.
.
.
```

The file **app/assets/stylesheets/1st_load_framework.css.scss** is
automatically included and compiled into your Rails application.css file
by the `*= require_tree .` statement in the
**app/assets/stylesheets/application.css.scss** file. The file could be
named anything. However, by giving it a name beginning with "1" it will
load before any other stylesheet files we may add later. The asset
pipeline loads files in alphabetical order. We want the Bootstrap
framework to load before any custom CSS files.

The `@import "bootstrap";` and `@import "bootstrap-sprockets";` directives will import the Bootstrap CSS
rules from the Bootstrap gem.

You could add the Bootstrap `@import` code to the
**app/assets/stylesheets/application.css.scss** file. However, it is
better to have a separate
**app/assets/stylesheets/1st_load_framework.css.scss** file. You may
wish to modify the Bootstrap CSS rules; placing changes to Bootstrap
CSS rules in the **1st_load_framework.css.scss** file will keep your
CSS better organized.

In addition to the simple `@import` directives, the
**app/assets/stylesheets/1st_load_framework.css.scss** contains a
collection of Sass mixins. We'll look at these later in the chapter.

Using Bootstrap CSS Classes
----------------------------

Now that you've installed Bootstrap, you have a rich library of
interactive effects you can add to your pages.

Take a look at the [Bootstrap documentation](http://getbootstrap.com/) to see your options.
Here are just a few examples:

-   [buttons](http://getbootstrap.com/css/#buttons)
-   [navigation bar](http://getbootstrap.com/components/#navbar)
-   [alerts](http://getbootstrap.com/components/#alerts)

At a simpler level, Bootstrap provides a collection of
carefully-crafted styling rules in the form of CSS classes. These are
building blocks you use for page layout and typographic styling. For
example, Bootstrap gives you CSS classes to set up rows and columns in
a grid system.

Let's take a closer look at the Bootstrap grid system.

### Bootstrap Grid

The [Bootstrap grid](http://getbootstrap.com/css/#grid) is responsive because it has "breakpoints." There
are actually four grids:

-   Extra small: browser windows 0 to 768 pixels wide (phones)
-   Small: browser windows 768 to 992 pixels wide (tablets)
-   Medium: browser windows 992 to 1200 pixels wide (desktops)
-   Large: browser windows 1200 pixels and wider (large desktops)

Start by designing for the extra small screen; then add classes prefixed "small,"
"medium," or "large" if you want a different layout for larger screens. The layout will change at each breakpoint.

The grid gives you 12 columns by default. You can organize your layout
in horizontal and vertical sections using `row` and `columns` classes.

For example, you could use Bootstrap grid classes to set up an
application layout with a footer as a row with two sections:


```html
<div class="container">
  <footer class="row">
    <section class="col-xs-4">
      Copyright 2016
    </section>
    <section class="col-xs-8">
      All rights reserved.
    </section>
  </footer>
</div>
```

The Bootstrap `row` class will create a horizontal break. The footer
will contain two side-by-side sections. The first will be four columns
wide; the second will be eight columns wide.

Here's the same footer with a responsive design:


```html
<div class="container">
  <footer class="row">
    <section class="col-xs-12 col-sm-4">
      Copyright 2016
    </section>
    <section class="col-xs-12 col-sm-8">
      All rights reserved.
    </section>
  </footer>
</div>
```

On desktops and tablets, the footer will contain two side-by-side
sections. On phones, each section will expand to take the full browser
width, appearing as stacked rows.

To better understand the grid system with all its options, see the
[documentation for the Bootstrap grid](http://getbootstrap.com/css/#grid).

### Presentational Versus Semantic Styles

There are two schools of thought among front-end developers. Some
developers are content to use Bootstrap's classes directly in Rails
view files. For these developers, the Bootstrap classes are both
practical and descriptive, making it easy for any developer who knows
the Bootstrap framework to visualize the layout of a page.

Other developers take issue with this approach. They argue that
Bootstrap's markup is often *presentational*, with class names
describing the appearance of the page. In an ideal world, all markup
would be *semantic*, with class names describing the function or purpose
of a style. For example, a submit button often needs styling. Compare
these two approaches to markup:

-   presentational: `<button class="big red button">Order Now</button>`
-   semantic: `<button class="submit">Order Now</button>`

Suppose your user testing indicates a green button generates more sales.
With the presentational approach you'd have to change both the Rails
view file and the CSS file. With a semantic approach, you'd just change
the CSS file to reassign the color of the `submit` class.

### Use Bootstrap Classes Directly

For quick and simple websites, where you don't need to be concerned
about long-term maintenance, use Bootstrap's CSS classes directly.

For example, you can style a button like this:

-   `<button type="button" class="btn btn-success">Order Now</button>`

The `btn-success` class is semantic and applies an "alert color"
which is green, by default, in Bootstrap.

### Or Use Sass Mixins with Bootstrap

You can use Sass mixins to create your own semantic class names.

Sass mixins add a layer of complexity that can map Bootstrap class
names to your own semantic class names.

For example, the Bootstrap grid system is presentational. Specifying
rows and columns, and quantifying the size of columns, describes the
visual appearance of sections of the layout rather than the purpose of
each section. The presentational approach makes it easy to visualize the
layout of a page. But you'll be tied to Bootstrap 3 class names for
the life of your website. If class names change in a future version of Bootstrao, or
you decide to switch to another front-end framework, it will be
difficult to update your application, as you will have to carefully
rebuild each view file.

Is it worth the effort to add the complexity of Sass mixins just to
future-proof your website? Probably not for a simple website such as the
one you are building for Foobar Kadigan.

The rails_layout gem uses Sass mixins to apply CSS style rules to the
default application layout. In doing so, the default application layout
is free of framework-specific code and can be used with either Bootstrap
or Zurb Foundation.

Before we examine the default application layout, let's take a look at
the Sass mixins supplied by the rails_layout gem.

Look again at the file
**app/assets/stylesheets/1st_load_framework.css.scss** created by the
rails_layout gem:


```scss
// import the CSS framework
@import "bootstrap-sprockets";
@import "bootstrap";

// make all images responsive by default
img {
  @extend .img-responsive;
  margin: 0 auto;
  }
// override for the 'Home' navigation link
.navbar-brand {
  font-size: inherit;
  }

// THESE ARE EXAMPLES YOU CAN MODIFY
// create your own classes
// to make views framework-neutral
.column {
  @extend .col-md-6;
  @extend .text-center;
  }
.form {
  @extend .col-md-6;
  }
.form-centered {
  @extend .col-md-6;
  @extend .text-center;
  }
.submit {
  @extend .btn;
  @extend .btn-primary;
  @extend .btn-lg;
  }
// apply styles to HTML elements
// to make views framework-neutral
main {
  @extend .container;
  background-color: #eee;
  padding-bottom: 80px;
  width: 100%;
  margin-top: 51px; // accommodate the navbar
  }
section {
  @extend .row;
  margin-top: 20px;
  }
```

The rails_layout gem is in active development so the file you've
created may be different from the example in this tutorial. It will
probably be very similar.

At the top of the file we import the Bootstrap framework CSS files from
the gem.

We override a Bootstrap style rule so the "Home" navigation link
matches the other links in the navigation bar.

Then we use mixins to create semantic classes.

Mixins can take a block of CSS styles, other mixins, or a CSS selector (a CSS class or ID).

If you'd like to combine CSS classes, or rename a CSS class, use the
`@extend` directive.

The first declaration `column` combines the Bootstrap
classes `col-md-6` and `text-center` to make a new class, `column`.

Next we create a few classes that combine Bootstrap
CSS classes. For example, the new `submit` class can be used for a
button. When we use it in a view, this class will be purely
semantic since it describes the purpose of the element, allowing us to
set its appearance outside of any view file.

Finally, to avoid applying Bootstrap classes in the application layout
file, we apply styles to HTML elements `main` and `section` to make the
views framework-neutral. We use the `@extend` directive to add a Bootstrap
CSS class. And we directly set standard CSS properties such as `background-color`
and `margin-top`.

Using this technique, the file
**app/assets/stylesheets/1st_load_framework.css.scss** becomes the
single point of intersection between the Bootstrap framework and the
application layout. For a simple website, this could be over-engineering
and counter-productive. The rails_layout gem uses the technique so that
either Bootstrap or Zurb Foundation can be used without any change to
the default application layout.

We'll use the CSS classes provided by the rails_layout gem in the
tutorial application, but if you choose to customize the application,
feel free to use Bootstrap classes directly to keep your project
simple.

Application Layout with Bootstrap
---------------------------------------

Let's look at the application layout file created by the rails_layout
gem:

Examine the contents of the file
**app/views/layouts/application.html.erb**:


```erb
<!DOCTYPE html>
<html>
  <head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><%= content_for?(:title) ? yield(:title) : "Learn Rails" %></title>
    <meta name="description"
      content="<%= content_for?(:description) ? yield(:description) : "Learn Rails" %>">
    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track' => 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track' => 'reload' %>
    <%= csrf_meta_tags %>
  </head>
  <body>
    <header>
      <%= render 'layouts/navigation' %>
    </header>
    <main role="main">
       <%= render 'layouts/messages' %>
       <%= yield %>
    </main>
  </body>
</html>
```

This file is almost identical to the simple application layout file we
looked at in the previous chapter.

Because we've applied Bootstrap classes to the HTML element `main` in
the **app/assets/stylesheets/1st_load_framework.css.scss** file,
there's no need to use Bootstrap classes directly in the application
layout.

Flash Messages with Bootstrap
-----------------------------------

The messages partial we use with Bootstrap is complex.

Examine the file **app/views/layouts/_messages.html.erb**:


```erb
<%# Rails flash messages styled for Bootstrap 3.0 %>
<% flash.each do |name, msg| %>
  <% if msg.is_a?(String) %>
    <div class="alert alert-dismissible
        alert-<%= name.to_s == 'notice' ? 'success' : 'danger' %>">
      <button type="button" class="close" data-dismiss="alert"
        aria-hidden="true">&times;</button>
      <%= content_tag :div, msg, :id => "flash_#{name}" %>
    </div>
  <% end %>
<% end %>
```

We use `each` to iterate through the flash hash, retrieving a `name` and
`msg` that are passed to a block to be output as a string. The
expression `if msg.is_a?(String)` serves as a test to make sure we only
display messages that are strings.

We construct a div that applies
Bootstrap CSS styling around the message. Bootstrap provides classes
`alert` and `alert-dismissible` to style the message.

We use the Ruby ternary operator to check the type of the alert.
A class of either `success` or `danger` styles the message.
Rails `notice` messages will get styled with the Bootstrap `success` class. Any other Rails
messages, including `alert` messages, will get styled with the
Bootstrap `danger` class.

We use the Rails `content_tag` view helper to create a div containing
the message.

Bootstrap creates a "close" icon by applying the class `alert-dismissible`.
Bootstrap's integrated JavaScript library will hide the alert box when
the "close" link is clicked.

Bootstrap provides [detailed documentation](http://getbootstrap.com/components/#alerts)
if you want to change the styling of the alert boxes.

Navigation Partial with Bootstrap
---------------------------------------

The layout and styling required for the Bootstrap navigation bar are in
the navigation partial file.

Examine the file **app/views/layouts/_navigation.html.erb**:


```erb
<%# navigation styled for Bootstrap 3.0 %>
<nav class="navbar navbar-inverse navbar-fixed-top">
  <div class="container">
    <div class="navbar-header">
      <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <%= link_to 'Home', root_path, class: 'navbar-brand' %>
    </div>
    <div class="collapse navbar-collapse">
      <ul class="nav navbar-nav">
        <%= render 'layouts/navigation_links' %>
      </ul>
    </div>
  </div>
</nav>
```

The navigation partial is now more complex, with layout and Bootstrap
classes needed to produce a responsive navigation bar.

At the conclusion of this chapter, you'll test the responsive navigation
by resizing the window. At small sizes, the navigation links will
disappear and be replaced by an icon labeled "Menu." Clicking the icon
will reveal a vertical menu of navigation links. The navigation menu is
a great demonstration of the ability of Bootstrap to adjust to the
small screen size of a tablet or smartphone.

If you'd like to add a site name or logo to the tutorial application,
you can replace the link helper `<%= link_to 'Home', root_path %>`. It
is important to preserve the enclosing layout and classes, even if you
don't want to display a site name or logo. The enclosing layout is used
to generate the navigation menu when the browser window shrinks to
accommodate a tablet or smartphone.

You'll see we wrap the nested partial
`render 'layouts/navigation_links'` with Bootstrap classes to complete
the navigation bar.

Navigation Links Partial
------------------------

The file **app/views/layouts/_navigation_links.html.erb** is
unchanged:


```erb
<%# add navigation links to this file %>
```

Later we'll add links to "About" and "Contact" pages.

The navigation links partial will be simply a list of navigation links.

We're following the *separation of concerns* principle here. By
separating the links from the styling that creates the navigation bar,
we segregate the code that is unique to Bootstrap. In the future,
if the Bootstrap layout or CSS classes change, we can make changes
without touching the navigation links. If we wish, we can replace the
navigation partial and substitute one that uses a different framework instead
of Bootstrap, leaving the navigation links intact.

Test the Application
--------------------

Let's see how the application looks with Bootstrap. The web server
may already be running. If not, enter the command:


```console
$ rails server
```

Open a web browser window and navigate to
[http://localhost:3000/](http://localhost:3000).

You should see a new page design that displays Bootstrap styling.
Thanks to the open source efforts of the Bootstrap core team and contributors, we've added powerful
front-end features to our website with little effort.

You can click the "X" close icons to hide the flash messages, thanks to
the integrated CSS and JavaScript of the Bootstrap framework.

Next we'll add "About" and "Contact" pages to the application. After we
update the navigation links, you'll see how the Bootstrap responsive
web design adjusts the navigation bar at different browser widths.

Remove the Flash Messages
-------------------------

Before we continue, we'll remove the flash messages we created for our
demonstration.

Update the file **app/controllers/visitors_controller.rb**:


```ruby
class VisitorsController < ApplicationController

  def new
    @owner = Owner.new
  end

end
```

Git
---

Let's commit our changes to the Git repository and push to GitHub:


```console
$ git add -A
$ git commit -m "front-end framework"
$ git push
```

