Analytics
=========

In earlier chapters, we built the tutorial application and deployed it
for hosting on Heroku.

We've left something out. Though not obvious, it's very important:
analytics.

Analytics services provide reports about website traffic and usage.

You'll use the data to increase visits and improve your site. Analytics
close the communication loop with your users; your website puts out a
message and analytics reports show how visitors respond.

Google Analytics is the best known tracking service. It is free, easy to
use, and familiar to most web developers. In this chapter we'll
integrate Google Analytics with the tutorial application.

There are several ways to install Google Analytics for Rails. The
article on [Analytics for Rails](http://railsapps.github.io/rails-google-analytics.html) looks at
various approaches and explains how Google Analytics works.

For this tutorial, we'll use the [Segment.com](https://segment.com/)
service. The service provides an API to send analytics data to dozens of
different services, including Google Analytics.

Segment.com
----------

[Segment.com](https://segment.com/) is a subscription service that gathers
analytics data from your application and sends it to dozens of different
services, including Google Analytics. The service is free for low-volume
websites, accommodating 1000 tracked users per month at no cost.
There is no charge to sign up for the service.

Using Segment.com means you install one JavaScript library and get access
to reports from dozens of analytics services. You can
[see a list of supported services](https://segment.com/docs/integrations). The company
offers helpful advice about [which analytics tools to choose from](https://segment.com/academy/).
For low-volume sites, many of the
analytics services are free, so Segment.com makes it easy to experiment
and learn about the available analytics tools. The service is fast and
reliable, so there's no downside to trying it.

Accounts You Will Need
----------------------

You will need an account with Segment.com. [Sign up for
Segment.com](https://segment.com/signup).

You will need accounts with each of the services that you'll use via
Segment.com.

You'll likely want to start with Google Analytics, so you'll need a
Google Analytics account and tracking ID.

Visit the [Google Analytics website](http://www.google.com/analytics/)
to obtain the Tracking ID for your website. You'll need to know the
domain name of your website to get an account for your website. If
you've deployed to Heroku without a custom domain, use the domain that
looks like "myapp.herokuapp.com". Or use your custom domain if you have
one. Use it for fields for "Website Name," "Web Site URL," and "Account
Name."

Choose the defaults when you create your Google Analytics account and
click "Get Tracking ID." Your tracking ID will look like this:
`UA-XXXXXXX-XX`. You won't need the tracking code snippet as we will use
the Segment.com JavaScript snippet instead.

You'll check your Google Analytics account later to verify that Google
is collecting data.

Installing the JavaScript Library
---------------------------------

Segment.com provides a JavaScript snippet that sets an API token to
identify your account and installs a library named **analytics.js**.
This is similar to how Google Analytics works. The Segment.com library
loads asynchronously, so it won't affect page load speed.

The Segment.com JavaScript snippet should be loaded on every page and it
can be included as an application-wide asset using the Rails asset
pipeline.

We'll add the Segment.com JavaScript snippet to a file named
**app/assets/javascripts/segment.js**. The manifest directive
`//= require_tree .` in the file
**app/assets/javascripts/application.js** will ensure that the new file
is included in the concatenated application JavaScript file. If you've
removed the `//= require_tree .` directive, you'll have to add a
directive to include the **app/assets/javascripts/segment.js** file.

Create a file **app/assets/javascripts/segment.js** and include the
following:


```js
(function(){

  // Create a queue, but don't obliterate an existing one!
  var analytics = window.analytics = window.analytics || [];

  // If the real analytics.js is already on the page return.
  if (analytics.initialize) return;

  // If the snippet was invoked already show an error.
  if (analytics.invoked) {
    if (window.console && console.error) {
      console.error('Segment snippet included twice.');
    }
    return;
  }

  // Invoked flag, to make sure the snippet
  // is never invoked twice.
  analytics.invoked = true;

  // A list of the methods in Analytics.js to stub.
  analytics.methods = [
    'trackSubmit',
    'trackClick',
    'trackLink',
    'trackForm',
    'pageview',
    'identify',
    'reset',
    'group',
    'track',
    'ready',
    'alias',
    'debug',
    'page',
    'once',
    'off',
    'on'
  ];

  // Define a factory to create stubs. These are placeholders
  // for methods in Analytics.js so that you never have to wait
  // for it to load to actually record data. The `method` is
  // stored as the first argument, so we can replay the data.
  analytics.factory = function(method){
    return function(){
      var args = Array.prototype.slice.call(arguments);
      args.unshift(method);
      analytics.push(args);
      return analytics;
    };
  };

  // For each of our methods, generate a queueing stub.
  for (var i = 0; i < analytics.methods.length; i++) {
    var key = analytics.methods[i];
    analytics[key] = analytics.factory(key);
  }

  // Define a method to load Analytics.js from our CDN,
  // and that will be sure to only ever load it once.
  analytics.load = function(key){
    // Create an async script element based on your key.
    var script = document.createElement('script');
    script.type = 'text/javascript';
    script.async = true;
    script.src = ('https:' === document.location.protocol
      ? 'https://' : 'http://')
      + 'cdn.segment.com/analytics.js/v1/'
      + key + '/analytics.min.js';

    // Insert our script next to the first script element.
    var first = document.getElementsByTagName('script')[0];
    first.parentNode.insertBefore(script, first);
  };

  // Add a version to keep track of what's in the wild.
  analytics.SNIPPET_VERSION = '4.0.0';

  // Load Analytics.js with your key, which will automatically
  // load the tools you've enabled for your account. Boosh!
  analytics.load("YOUR_WRITE_KEY");

})();
```

You can get the newest version of the code from the
[Segment.com Quickstart](https://segment.com/docs/sources/website/analytics.js/quickstart/) page.
If you copy a newer version of the code, remove the
`<script type="text/javascript">` and `</script>` tags from the top and bottom. The Rails
asset pipeline will add the code to the **application.js** file which already contains the
necessary `<script>` tags.

If you copy the code from the Segment.com Quickstart instructions, also remove:

```js
  // Make the first page call to load the integrations. If
  // you'd like to manually name or tag the page, edit or
  // move this call however you'd like.
  analytics.page();
```

We'll add `analytics.page();` later, wrapping it in additional code to
accommodate Rails Turbolinks.

Note that the Segment.com website offers a minified version of the snippet for
faster page loads. We've used the non-minified version so you can read
the code and comments. If you want, you can get minified version from
the Segment.com website for improved speed.

Replace the Write Key
----------------------------------

You **must replace** `YOUR_WRITE_KEY` with your Segment.com "Write Key."
After you [log in to Segment.com](https://segment.com/), click on your "workspace,"
then choose a "source," click "settings," and click "API Keys" in the side navigation bar.
Add the "Write Key" in the file where you see this line:

```js
// Load Analytics.js with your key, which will automatically
// load the tools you've enabled for your account. Boosh!
analytics.load("YOUR_WRITE_KEY");
```

Now you must add extra code to the Segment.com JavaScript snippet.
The extra code accommodates Turbolinks, plus page view and event tracking,
which we'll look at next.

Add Integration Code
----------------------------------

To make sure every page is tracked when Rails Turbolinks is used, plus track page views and events,
you must add the following JavaScript to the end of the **app/assets/javascripts/segment.js** file:

```js
// accommodate Turbolinks
// track page views and form submissions
$(document).on('turbolinks:load', function() {
  console.log('page loaded');
  analytics.page();
  analytics.trackForm($('#new_visitor'), 'Signed Up');
  analytics.trackForm($('#new_contact'), 'Contact Request');
})
```

Add it after the last line. Add it after the orthographic car wreck that looks like `})();`.

I'll explain the purpose of this code next.

Page View Tracking with Turbolinks
----------------------------------

To make sure every page is tracked when Rails Turbolinks is used, we've added
the following JavaScript to the **app/assets/javascripts/segment.js** file:

```js
// accommodate Turbolinks
// track page views and form submissions
$(document).on('turbolinks:load', function() {
.
.
.
  analytics.page();
.
.
.
})
```

Rails 4.0 introduced a feature named
[Turbolinks](https://github.com/rails/turbolinks/) to increase the
perceived speed of a website.

Turbolinks makes an application appear faster by only updating the body
and the title of a page when a link is followed. By not reloading the
full page, Turbolinks reduces browser rendering time and trips to the
server.

With Turbolinks, the user follows a link and sees a new page but
Segment.com or Google Analytics thinks the page hasn't changed because a
new page has not been loaded. To resolve the issue, you could disable
Turbolinks by removing the turbolinks gem from the Gemfile. However,
it's nice to have both the speed of Turbolinks and tracking data, so
I'll show you how to get tracking data with Turbolinks.

Turbolinks fires a `load` event when a page has been replaced.
The code listens for the `load` event and calls the Segment.com
`analytics.page()` method. This code will work even on pages that are
not visited through Turbolinks (for example, the first page visited).

Event Tracking
--------------

Segment.com gives us a convenient method to track page views. Page view
tracking gives us data about our website traffic, showing visits to the
site and information about our visitors.

It's also important to learn about a visitor's activity on the site.
Site usage data helps us improve the site and determine whether we are
meeting our business goals. This requires tracking events as well as
page views.

The Segment.com JavaScript library gives us two methods to track events:

-   `trackLink`
-   `trackForm`

Link tracking can be used to send data to Segment.com whenever a visitor
clicks a link. It is not useful for our tutorial application because we
simply record a new page view when a visitor clicks a link on our site.
However, if you add links to external sites and want to track
click-throughs, you could use the `trackLink` method. The method can
also be used to track clicks that don't result in a new page view, such
as changing elements on a page.

The `trackForm` method is more useful for our tutorial application.
We've already appended it to the **app/assets/javascripts/segment.js**
file:


```js
// accommodate Turbolinks
// track page views and form submissions
$(document).on('turbolinks:load', function() {
  console.log('page loaded');
  analytics.page();
  analytics.trackForm($('#new_visitor'), 'Signed Up');
  analytics.trackForm($('#new_contact'), 'Contact Request');
})
```

I've included a `console.log('page loaded')` statement so you can check
the browser JavaScript console to see if the code runs as expected.

The `trackForm` method takes two parameters, the ID attribute of a form
and a name given to the event.

Form tracking will show us how many visitors sign up for the newsletter
or submit the contact request form. Obviously we can count the number of
subscribers in MailChimp or look in the site owner's inbox to see how
many contact requests we've received. But form tracking helps us
directly correlate the data with visitor data. For example, we can
analyze our site usage data and see which traffic sources result in the
most newsletter sign-ups.

You can read more about the Segment.com JavaScript library in the
[Segment.com documentation](https://segment.com/libraries/analytics.js).

Troubleshooting
-----------------------

Click "Debugger" in the navigation bar so you can monitor data sent to
Segment.com from your application.

When you test the application locally, you should see the results of
page visits and form submissions within seconds in the Segment.com
debugger.

If you don't see your page visits in the Segment.com debugger, open the
browser JavaScript console, visit a page, and check for the message "page loaded"
in the JavaScript console. In the Chrome browser, the JavaScript console is
available under the item "Developer" in the "View" menu.

Segment.com Integrations
-----------------------

After installing the Segment.com JavaScript snippet in your application,
go to your "sources" page and click the "integrations" link to
visit the integrations page to select the services that will
receive your data.

Each service requires a different configuration information. At a
minimum, you'll have to provide an account identifier or API key that
you obtained when you signed up for the service.

For Google Analytics, enter your Google Analytics tracking id. It looks
like `UA-XXXXXXX-XX`.

With Google Analytics enabled as a Segment.com integration, you'll see
form submissions appear in the Google Analytics Real-Time report, under
the "Events" heading.

Note that Google doesn't process their data in real-time in most of its
reports. Data appears immediately in the Google Analytics Real-Time
report. Other Google Analytics reports, such as the Audience report,
won't show data immediately. Check the next day for updated reports.

Deploy
------

Commit to the Git repo and deploy to Heroku:


```console
$ git add -A
$ git commit -m "analytics"
$ git push
```

Then you can deploy to Heroku:


```console
$ git push heroku master
```

When you visit the site, you should see real-time tracking of data sent
to Segment.com in the Segment.com debugger.

Log into your Google Analytics account to see real-time tracking of
visits to your website. Under "Standard Reports" see "Real-Time
Overview." You'll see data within seconds after visiting any page.

Improving the User Experience
-----------------------------

Website analytics can be used to improve visitors' experience of the
website. Deploying the website is not the last step in your project.
Unlike many earlier forms of communication (such as releasing a film,
publishing a book, or broadcasting an advertisement), we can see how
every visitor responds to the website. That means your work is not done
when you deploy the site. Look at your usage data to see which elements
of the site are getting attention and which are being used.

Does no one visit the "About" page? Maybe the navigation link is
difficult to find. Do many people visit the Contact page but few submit
a contact request form? Maybe you should change the label on the button
or offer other ways to contact the site owner.

Effective and successful websites often are the result of systematic
[A/B testing](http://en.wikipedia.org/wiki/A/B_testing) (sometimes
called *split testing*). A/B testing is a technique of creating
variations on a web page, such as changing text, layout, or button
colors, and using website analytics to measure the effect of the change.
You can learn more about services such as [Content
Analytics](http://www.google.com/analytics/features/content.html) in
Google Analytics, [Optimizely](https://www.optimizely.com/), or [Visual
Website Optimizer](http://visualwebsiteoptimizer.com/). These services
provide complete "dashboards" to set up usage experiments and measure
results ([Optimizely](https://www.optimizely.com/) is available as a
Segment.com integration).

Conversion Tracking
-------------------

You may only be interested in knowing that people visit your site,
without measuring visitors' engagement or response to the site. But in
most cases, if you build a website, you'll offer a way for visitors to
respond, whether it is by purchasing a product, signing up for a
newsletter, or clicking a "like" button.

The ultimate measure of website effectiveness is the [conversion
rate](http://en.wikipedia.org/wiki/Conversion_rate). The term comes from
the direct marketing industry and originally referred to a measure of
how people responded to "junk mail" offers. For a website, the
conversion rate indicates the proportion of visitors who respond to a
*call to action*, which may be an offer to make a purchase, register for
a membership, sign up for a newsletter, or any other activity which
shows the visitor is engaged and interested.

For our tutorial application, we can measure our website effectiveness
by looking at the conversion rate for newsletter sign-ups.

We're tracking page views which will give us a count of visits to the
website home page. And we've got event tracking in place to count
newsletter sign-ups. If 100 people visit the home page and 10 people
request a newsletter, we've got a conversion rate of 10%.

We can try to improve the conversion rate by improving the user
experience (perhaps through A/B testing) or focusing on increasing
traffic from sources that provide a higher conversion rate.

You can monitor your site's conversion rate by [setting up events as
goals](https://support.google.com/analytics/answer/1032415?hl=en) in
Google Analytics. Segment.com also integrates with many services which
provide conversion tracking.

Enjoy What You've Achieved
------------------------

You've completed building the tutorial application.

If your project was to build an application for someone else, whether
the company you work for, or a client like Foobar Kadigan, you've
completed the [deliverable](http://en.wikipedia.org/wiki/Deliverable).

You started with project planning, in the form of user stories. You
implemented the application using a variety of technologies supported by
the Ruby on Rails development platform. And you've deployed the
application for others to use, with analytics in place to track traffic
and usage.

Not every manager or client will appreciate the effort or the complexity
of the project you've built. Mr. Kadigan's happiness may depend on how
well you've understood his goals and the degree to which you've met his
expectations. If you're working for yourself, or launching your startup,
you may be your own toughest boss, because there is always more to do.

With technology projects, like many other aspects of life, though it
seems you'll never get it right, and never get it done, there are
moments when you can savor a sense of accomplishment. This is one of
those moments.

Before you start thinking about adding one more feature, or updating the
application for the new releases that inevitably came out during the
time you were working, take time to bask in the satisfaction of seeing
the results of your work.

Software development has its own unique rhythm of frustration and
satisfaction. As software developers, we subject ourselves to hours,
days, or weeks of struggle with code that is cryptic and resists
understanding. We gain mastery for a few minutes and then turn to the
next problem. With each feature you implement, or issue you resolve,
you'll experience brief elation before resuming the grind of
development. But at each milestone, and at the completion of the
project, you've built something tangible that you can use. You can try
it out yourself and show it to others.

Give yourself full credit. You've built something extraordinary with
little more than intelligence and attention. You've leveraged the work
of other developers who have contributed to the open source Ruby on
Rails platform and you've created your own unique product. This is what
drives us as developers; to create something from nothing, using only
our collective intelligence and ambition.
