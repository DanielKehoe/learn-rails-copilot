Request and Response
====================

You've configured the tutorial application, created static pages, and
seen the magic of Rails routing.

In this chapter, we'll investigate the web request-response cycle and
look at the model-view-controller design pattern so you'll be prepared
to build a dynamic home page.

Investigating the Request Response Cycle
----------------------------------------

Remember, at its core, the World Wide Web is nothing more than web
browsers that request files from web servers.

Web browsers make *requests*. A web server *responds* to a request by
sending an HTML file. Depending on the headers in the HTML file, the web
browser may make additional requests and get additional CSS, JavaScript,
and image files.

The beauty and simplicity of the World Wide Web architecture, as
conceived by Tim Berners-Lee in 1990, is that the web is nothing more
than a request from a web browser and a response from a web server. Some
web pages now include streaming video, or music, requiring an open
"pipe" between the web server and the web browser, but even so, an
initial request-response cycle delivers the page that sets up the
stream.

We can reduce the mystery of how the web works to its simplest
components when we investigate the request-response cycle. We'll see
that everything that happens in a web application takes place within the
flow of the request-response cycle.

Let's look at the request-response cycle.

![The request-response cycle.\label{fig:request-response}](images/figures/learn-rails-41-request-response.png)

### Inside the Browser

We can see the actual request, and the actual response, by using the
diagnostic tools built into the web browser.

Start the application server if it is not already running:


```console
$ rails server
```

Developers use various web browsers during development. I'll provide
instructions for Chrome, since it is the most popular. Even if you
prefer Mozilla Firefox or Apple Safari, try this in Chrome, so you can
follow along with the text.

Start our investigation by putting Chrome into "Incognito Mode" with
Command-Shift-N (on a Mac). On Linux, use Ctrl-Shift-N to get in
incognito mode with Chrome. Alternatively, you can clear the browser
cache. This clears any files that were previously cached by the browser.

The Developer Tools view is your primary diagnostic tool for front-end
(browser-based) development, including CSS and JavaScript.

In Chrome on macOS, press Command-Option-I to open the *Developer
Tools View* in a section of the browser window. Alternatively, you can
find the menu item under View/Developer/Developer Tools.

In Chrome on Windows or Linux platforms, press Shift-Ctrl-I or select
Menu/Tools/Developer Tools.

Initiate the request-response cycle by visiting the "About" page at
[http://localhost:3000/about.html](http://localhost:3000/about.html).

In the Developer Tools view, under the Network tab, you'll see files received by the browser
from the web server. There is only one: "about.html". This is the file
that the browser evaluates to display a web page.

![Viewing a request in the Developer Tools View.\label{fig:request}](images/figures/learn-rails-41-request.png)

Be sure to select the Network tab in the Developer Tools view.

Click the "about.html" file icon. Then click the tab "Headers." The
diagnostic window shows the entire request sent to the server and the
entire response received by the browser.

![Viewing request headers in the Developer Tools View.\label{fig:request-headers}](images/figures/learn-rails-41-request-headers.png)

Under the heading "General," you can see the request is composed of:

-   request URL (http://localhost:3000/about.html)
-   request method (GET)
-   status code (200 OK or 304 Not Modified)

You can also see request and response headers:

-   request headers (including the User Agent identifier)
-   response headers (including last-modified date/time)

You can see the HTML sent to the browser by clicking the Preview or
Response tabs in the view under the Network tab.

Here's the point of the exercise: The browser's Developer Tools view shows
all the data exchanged between the browser and server. You're looking at
everything that passes through the plumbing.

### Inside the Server

The browser's Developer Tools view doesn't show you what happens on the
server. For that, go to the server logs or the console window.


```console
Started GET "/" for ::1 at ...
```

Notice how the diagnostic messages in the console window match the
headers in the browser Developer Tools view. The browser's "Request
Method:GET" matches the server's "Started GET."

Notice there are no console log messages for pages delivered from the
**public** folder.

Soon we'll see much more in the console window, after we've built a
dynamic web page that is assembled by the application server.

How the Browser Works
---------------------

What happens after the browser receives a response from the server?

The response is not complete until all files are received (or the
browser reaches a time-out limit). Modern browsers retrieve files
asynchronously; the order and location of the files in the initial HTML
file doesn't matter because the browser will try to load all the files
before displaying the page.

### Document Object Model

When the web browser receives an HTML file, it creates an internal
representation of the page in computer memory, called the
Document Object Model (DOM). It provides a structural representation of the document.
The DOM works like an API for HTML documents, allowing you to
modify the content and visual presentation of the page by using JavaScript.

Later in the tutorial, we'll see how a JavaScript library such as
[jQuery](http://en.wikipedia.org/wiki/Jquery) can be used to do things
like hiding or revealing HTML elements on a page by manipulating the
DOM.

### Rendering

Each time the DOM changes, the browser engine converts the DOM to a visual
representation of the page and renders it in the browser window.

Knowing about the DOM will help you understand what happens in the browser when
it receives a web response. And understanding the DOM will help you work
with JavaScript for front-end programming. But in this book, our focus is on
building a server-side web application in Rails. Let's see how a Rails
application responds to a web request.

How the Application Works
---------------------

Now that we've investigated the request-response cycle, let's dig deeper
to understand what happens inside the Rails application in
response to a browser request. To do so, we'll need to understand the
model–view–controller concept.

### Video Option

This eight minute video introduces the model–view–controller concept:

- [Model View Controller in Rails](https://www.youtube.com/watch?v=fWOSN8FLHTY)

### The Model View Controller Concept

The model–view–controller concept is key to understanding how a Rails
application responds to a browser request.

Here is a diagram that shows what happens in the server during the
request-response cycle.

![Model–View–Controller in Rails.\label{fig:mvc-flow}](images/figures/learn-rails-41-mvc-flow.png)

You learned earlier that, from the perspective of a software architect,
Rails is organized to conform to the
[model–view–controller](http://en.wikipedia.org/wiki/Model%E2%80%93View%E2%80%93Controller)
software design pattern. This enforces "separation of concerns" to keep
code manageable and organized. The MVC design pattern is optimal for web
applications and is a central organizing principle for Rails.

The MVC design pattern originated in the design of desktop applications.
"Model" classes manipulated data; "view" classes created the user
interface; and a "controller" class responded to user interaction.

Some computer scientists feel the architecture of web applications
doesn't quite match the original MVC design pattern of desktop
applications. We can see the reason for the quibble in the next diagram.
The diagram shows the MVC architecture as part of the Rails software
stack.

At the base of the stack is the web browser. A request flows upward
through the layers and encounters the router which dispatches the
request to an appropriate controller.

In a Rails application, there is a single routing file,
**config/routes.rb**, and multiple controllers, models, and views.

![Model–View–Controller stack in Rails.\label{fig:mvc-stack}](images/figures/learn-rails-41-mvc-stack.png)

Considering the importance of the router, perhaps we should call our
Rails architecture the *RCMV*, or Routing-Controller-Model-View,
pattern. Despite the quibble about nomenclature, the architecture is
well understood and used by all Rails developers.

Here's the step-by-step walk-through of what happens.

When the web browser makes a request, a *router* component will check
the **config/routes.rb** file and determine which *controller* should
handle the request, based on the web address and HTTP protocol. The
controller will obtain any needed data from a *model*. After obtaining
data, the controller will render a response combining data from the
model with a *view* component that provides markup and layout. The
response is an HTML file that the controller assembles for the browser
to display.

The model, view, and controller are files you create containing Ruby
code. Each file has a certain structure and syntax based on foundation
model, view, and controller classes defined in the Rails framework. The
model, view, and controller classes you create will *inherit* behavior
from parent classes that are part of the framework, so you will have
less code to write yourself.

In most Rails applications, a **model** obtains data from a database,
though some models obtain data from a remote connection to another
server. For example, a User model might retrieve a user name and email
address from a local database. A User model could also obtain a user's
recent tweets from Twitter or a user's hometown from Facebook. The
controller can obtain data from more than one model if necessary.

A **controller** can have more than one *action*. For example, a User
controller might have actions to display a list of users, or add or
delete a user from a list. The **config/routes.rb** file matches a web
request to a controller action. In the software architects' terminology,
each action is a *method* of the controller *class*. We use the terms
*action* and *method* interchangeably when we talk about a Rails
controller; to be precise, controller actions are implemented as
methods.

In practice, Rails developers try to limit controllers to seven standard
actions: `index`, `show`, `new`, `create`, `edit`, `update` and
`destroy` actions. A controller that offers these actions is said to be
"RESTful" (a term that refers to [representational state
transfer](http://en.wikipedia.org/wiki/Representational_state_transfer),
another software design abstraction). It's not important to understand
the abstract principles of RESTful design; recognizing the term and
knowing that Rails controllers have seven standard actions is sufficient
for beginners.

A **view** file combines Ruby code with HTML markup. Typically there
will be a view file associated with each controller action that displays
a page. An index view might show a list of users. A "show" view might
provide details of a user's profile. View files look much like ordinary
HTML files but typically contain data in the form of Ruby variables.
Often you'll see Ruby statements such as blocks that iterate through
lists to create tables. Following the "separation of concerns"
principle, it is considered good practice to limit Ruby code in view
files to only displaying data; anything else belongs in a model.

Not every controller action has its own view file. In many controllers,
on completion, the `destroy` action will redirect to the index view, and
`create` will redirect to either `show` or `new`.

This conceptual overview will be easier to grasp when you actually see
the code for a model, view, and controller. We'll create model, view,
and controller files in the next chapter.

Remove the About Page
---------------------

We've been using the static "About" page to investigate the
request-response cycle.

We're done, so delete the file **public/about.html**:

```console
$ rm public/about.html
```

Earlier, we set up the **config/routes.rb** file. You can leave it in
place. We'll change it in the next chapter.

Now we'll look at ways to implement the home page using the full power
of Rails.
