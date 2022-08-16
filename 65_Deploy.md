Deploy
======

You've been running the default web server on your local
machine. If you wanted, you could leave your computer running, set up a
[managed DNS
service](http://en.wikipedia.org/wiki/List_of_managed_DNS_providers),
and your web application would be accessible to anyone. But even if you
wanted to leave your computer running 24 hours a day, you're probably
not a security expert, your web server isn't tuned to handle much traffic, and
your computer is distant from the interconnection hubs where most
websites are hosted. For these reasons, when we move a web application
from development to production, we deploy it to a [web hosting
service](http://en.wikipedia.org/wiki/Web_hosting_service) that provides
a hosting platform on a server located in a strategically-located [data
center](http://en.wikipedia.org/wiki/Data_center).

Data centers offer [colocation
services](http://en.wikipedia.org/wiki/Colocation_centre), renting
rack-mounted computers with fast Internet connections that can be
configured as web servers. In the early days of the web, deploying a web
application required [system
administration](http://en.wikipedia.org/wiki/System_administration)
skills to configure and maintain a web server. Today, some developers
like to set up their web servers "from bare metal" using [virtual
private servers](http://en.wikipedia.org/wiki/Virtual_private_server)
from Linode, Slicehost, Rackspace, Amazon EC2, or others. With sufficent
skills and study, they say there is a feeling of satisfaction from doing
it yourself. But not everyone wants to be a system administrator. Most
Rails developers simply use a hosted [platform as a
service](http://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS)
provider such as [Heroku](https://www.heroku.com/),
[DigitalOcean](https://www.digitalocean.com/),
[EngineYard](https://www.engineyard.com/),
[OpenShift](https://www.openshift.com/), or [Pivotal Cloud
Foundry](http://pivotal.io/platform).

If you've previously built web sites, you may already be using a [shared web
hosting](http://en.wikipedia.org/wiki/Shared_web_hosting_service)
service such as GoDaddy or DreamHost.
Be skeptical if a shared web hosting service, designed for WordPress
or static websites, claims to support
Rails applications; most do so badly. Shared hosting services offer file
space for static websites on servers that are shared by thousands of
websites. A Rails application requires considerably greater computing
resources and specialized expertise. In contrast, a platform as a
service provider offers a hardware
and software stack optimized for application performance and developer
convenience.

[Heroku](https://www.heroku.com/) is the best known and most popular
PaaS provider and we'll use it to deploy the tutorial application. Using
Heroku or another PaaS provider means you don't need skills as a system
administrator to manage your web server. Instead, you'll have experts
maintaining the production environment, tuning system performance, and
keeping the servers running.

Heroku Costs
------------

It costs nothing to set up a Heroku account and deploy as many
applications as you want. You'll pay only if you upgrade your hosting to
accommodate a busy website.

Heroku pricing is based on a measure of computing resources the company
calls a "dyno." Think of a dyno as a virtual server (though it is not).
For personal projects, you can run your Rails application on a single dyno
and never incur a charge, as long as it is not active more than 12 hours a day.

A single dyno idles after one hour of inactivity, "going to sleep" until
it receives a new web request. For a personal project, this means your
web application will respond with a few seconds delay if it hasn't
received a web request in over an hour. After it wakes up, it will
respond quickly to every browser request.

If you want your web application running 24 hours per day and
responding to every request without
delay, Heroku will charge \$7 per month for a "hobby" account.
You'll be able to set up a
custom domain, using your own domain name. Heroku offers the option
of adding dynos to handle more traffic for \$25 per month;
here's an article that
[compares Heroku costs](http://www.octolabs.com/blogs/octoblog/2015/03/31/analysis-of-the-rumored-heroku-pricing-changes/).

A single dyno can serve thousands of requests per second, but
performance depends greatly on your application. As a default,
Heroku supports [Puma](http://puma.io/), the recommended web server
for Rails 5. Serving a typical Rails application that
takes 100ms on average to process each request, Puma can accommodate
about 50 requests per second per dyno, which is adequate for a personal
project. If traffic surges on your website and exceeds 50 requests per second,
you can scale up with more dynos.

Heroku is ideal for hosting our application:

-   no system administration expertise is required
-   hosting is free
-   performance is excellent

For this tutorial application, we won't concern ourselves with the
possibility that the website may get a lot of traffic. I'm sure you'll
join me in offering hearty thanks to Heroku for providing a convenient
service that beginners can use for free.

Let's deploy!

Test the Application
--------------------

Before deploying an application to production, a professional Rails
developer runs *integration* or *acceptance* tests. If the developer
follows the discipline of *test-driven development*, he or she will have
a complete test suite that confirms the application runs as expected.
Often the developer uses a *continuous integration* server which
automatically runs the test suite each time the code is checked into the
GitHub repository.

We haven't used test-driven development to build this application so no
test suite is available. You've tested the application manually at each
stage.

Preparing for Heroku
--------------------

You'll need to prepare your Rails application for deployment to Heroku.

### Gemfile

We need to modify the Gemfile for Heroku.

We add a `group :production` block for a gem that Heroku needs:

-   [pg](https://rubygems.org/gems/pg) - PostgreSQL gem

Heroku doesn't support the SQLite database; the company provides a
PostgreSQL database. Though we won't need it for our tutorial
application, we must include the PostgreSQL gem for Heroku. We'll mark
the [sqlite3](https://rubygems.org/gems/sqlite3) gem to be used in
development only.

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
```

We have to run `bundle install` because we've changed the Gemfile. The
gem we've added is only needed in production so we don't install it
on our local machine. When we deploy, Heroku will read the Gemfile and
install the gem in the production environment. We'll run
`bundle install` with the `--without production` argument so we don't
install the new gem locally:


```console
$ bundle install --without production
```

You'll see:

```console
.
.
.
Gems in the group production were not installed.
Use `bundle show [gemname]` to see where a bundled gem is installed.
```

Let's commit our changes to the Git repository and push to GitHub:


```console
$ git add -A
$ git commit -m "gems for Heroku"
$ git push
```

### Asset Pipeline in Production

It is important to understand that assets are compiled by Heroku
at the time of deployment. Rails compiles assets to make our application faster for the user.

The Rails asset pipeline produces single CSS and JavaScript files that combine all the files in the
folders **app/assets/javascripts/** and **app/assets/stylesheets/**. In development
mode, the Rails asset pipeline "live compiles" all CSS
and JavaScript files so any changes are reflected immediately.
But compiling assets adds processing overhead. In
production, a web application would be slowed unnecessarily if assets
were compiled for every web request. Consequently, assets are
precompiled by Heroku at the time we deploy our application to production.

When assets are compiled, the Rails asset pipeline will automatically
produce concatenated and minified **application.js** and
**application.css** files from files listed in the manifest files
**app/assets/javascripts/application.js** and
**app/assets/stylesheets/application.css.scss**. The result will be several files added
to the **public/assets/** folder. The filenames will contain a long unique identifier that prevents
caching when you change the application CSS or JavaScript.

You can precompile assets manually with the command `rails assets:precompile`
but ordinarily it is not necessary. It is a likely indicator that
the asset pipeline is not working or assets are not compiled if CSS styling is missing from your web pages.

If you want to learn more about the asset pipeline, refer to the Rails Guide on the [Asset Pipeline](http://guides.rubyonrails.org/asset_pipeline.html) or an [article from LaunchSchool](https://launchschool.com/blog/rails-asset-pipeline-best-practices).

### Option to Ban Spiders

Do you want your website to show up in Google search results? If there's
a link anywhere on the web to your site, within a few days (sometimes
hours) the Googlebot spider will visit your site and add it to the
database for the Google search engine. Most webmasters want their sites
to be found in Google search results. If that's not what you want, you
may want to modify the file **public/robots.txt** to prevent indexing by
search engines.

Only change this file if you want to prevent your website from appearing
in search engine listings:


```html
# See http://www.robotstxt.org/robotstxt.html for documentation
#
# To ban all spiders from the entire site uncomment the next two lines:
# User-agent: *
# Disallow: /
```

To block all search engine spiders, remove the commenting from the
`User-Agent` and `Disallow` lines.

You can learn more about the format of the [robots exclusion
standard](http://en.wikipedia.org/wiki/Robots_exclusion_standard).

### Humans.txt

Many websites include a **robots.txt** file for nosy bots so it's only
fair that you offer a **humans.txt** file for nosy people. Few people
will look for it but you can add a file **public/humans.txt** to credit
and identify the creators and software behind the website. The HTML5
Boilerplate project offers an [example
file](http://html5boilerplate.com/humans.txt) or you can [borrow from
RailsApps](https://tutorials.railsapps.org/humans.txt).

Sign Up for a Heroku Account
----------------------------

In the chapter, "Accounts You May Need," I suggested you sign up for a
Heroku account.

To deploy an app to Heroku, you must have a Heroku account. Visit
[https://id.heroku.com/signup/devcenter](https://id.heroku.com/signup/devcenter)
to set up an account.

Be sure to use the same email address you used to configure Git locally.
You can check the email address you used for Git with:


```console
$ git config --get user.email
```

Heroku Toolbelt
---------------

Heroku provides a command line utility for creating and managing Heroku
apps.

Visit [https://toolbelt.heroku.com/](https://toolbelt.heroku.com/) to
install the Heroku Toolbelt. A one-click installer is available for Mac
OS X, Windows, and Linux.

The installation process will install the Heroku command line utility.
It also installs the
[Foreman](http://blog.daviddollar.org/2011/05/06/introducing-foreman.html)
gem which is useful for duplicating the Heroku production environment on
a local machine. The installation process will also make sure Git is
installed.

To make sure the Heroku command line utility is installed, try:


```console
$ heroku version
heroku-toolbelt/...
```

You'll see the heroku-toolbelt version number.

You should be able to login using the email address and password you
used when creating your Heroku account:


```console
$ heroku login
Enter your Heroku credentials.
Email: adam@example.com
Password:
Could not find an existing public key.
Would you like to generate one? [Yn]
Generating new SSH public key.
Uploading ssh public key /Users/adam/.ssh/id_rsa.pub
```

The Heroku command line utility will create SSH keys if necessary to
guarantee a secure connection to Heroku.

Heroku Create
-------------

Be sure you are in your application root directory and you've committed
the tutorial application to your Git repository.

Use the Heroku create command to create and name your application.


```console
$ heroku create myapp
```

Replace `myapp` with something unique. Heroku demands a unique name for
every hosted application. If it is not unique, you'll see an error,
"name is already taken." Chances are, "learn-rails" is already taken.

The name must start with a letter and can only contain lowercase letters, numbers, and dashes.

If you don't specify your app name (`myapp` in the example above),
Heroku will supply a placeholder name. You can easily change Heroku's
placeholder name to a name of your choice with the `heroku apps:rename`
command (see [Renaming Apps from the CLI](https://devcenter.heroku.com/articles/renaming-apps)).

Don't worry too much about getting the "perfect name" for your Heroku
app. The name of your Heroku app won't matter if you plan to set up your
Heroku app to use your own domain name. You'll just use the name for
access to the instance of your app running on the Heroku servers; if you
have a custom domain name, you'll set up DNS (*domain name service*) to
point your domain name to the app running on Heroku.

The `heroku create` command sets your Heroku application as a Git remote
repository. That means you'll use the `git push` command to deploy your
application to Heroku.

Enable Email
------------

You'll need to enable email for production or else you'll get errors
when your application tries to send email from Heroku.

To use SendGrid, add the following to your **config/environments/production.rb** file:


```ruby
# email enabled in production
config.action_mailer.smtp_settings = {
  address: "smtp.sendgrid.net",
  port: 587,
  domain: Rails.application.secrets.domain_name,
  authentication: "plain",
  enable_starttls_auto: true,
  user_name: Rails.application.secrets.email_provider_username,
  password: Rails.application.secrets.email_provider_password
}
# ActionMailer Config
config.action_mailer.default_url_options = { :host => Rails.application.secrets.domain_name }
config.action_mailer.delivery_method = :smtp
config.action_mailer.perform_deliveries = true
config.action_mailer.raise_delivery_errors = false
```

You can use port 25, 587, or 2525 (some ISPs restrict connections on port 25).

Be sure to add the new settings before the `end` keyword in the file.
The settings can be added anywhere, as long as they precede the `end`
keyword!

You'll need to specify the unique name you've selected for your hosted
application. We're using the `Rails.application.secrets.domain_name`
configuration variable in two places in the file. The
**config/secrets.yml** file provides configuration variables for use in
production.

Be sure to commit your code to the Git local repository:


```console
$ git add -A
$ git commit -m "email set for Heroku"
$ git push
```

Next we'll set Heroku environment variables.

Set Heroku Environment Variables
--------------------------------

When you run your application, configuration
values are obtained from the **config/secrets.yml** file, which contains
Unix environment variables which are set in the **.bash_profile** or **.bashrc** files.

Heroku doesn't have a **.bash_profile** or **.bashrc** file, so you'll need a way to set environment
variables on Heroku. You can use the `heroku config:add` command.

```console
$ heroku config:add SENDGRID_USERNAME='example'
$ heroku config:add SENDGRID_PASSWORD='secret'
$ heroku config:add MAILCHIMP_API_KEY='my-key'
$ heroku config:add MAILCHIMP_LIST_ID='mylistid'
$ heroku config:add OWNER_EMAIL='me@example.com'
$ heroku config:add DOMAIN_NAME='myapp.herokuapp.com'
```
Don't use the values shown above. Instead, look in your
**.bash_profile** or **.bashrc** files and copy the values you find there.

When you set `myapp.herokuapp.com`, replace `myapp` with the name that
Heroku is using for your application. If you want to use a custom domain
name, you'll need to set up DNS (*domain name service*), which we won't
cover in this tutorial.

You don't need to set `SECRET_KEY_BASE`, even though it is in your
**config/secrets.yml** file. Heroku sets it automatically.

Check that the environment variables are set with:


```console
$ heroku config
```

See the Heroku documentation on [Configuration and Config
Vars](https://devcenter.heroku.com/articles/config-vars) and the article
[Rails Environment
Variables](http://railsapps.github.io/rails-environment-variables.html)
for more information.

Push to Heroku
--------------

After all this preparation, you can finally push your application to
Heroku.

Be sure to commit any recent changes to the Git local repository before
you push to Heroku.

You commit your code to Heroku just like you push your code to GitHub.

Here's how to push to Heroku:


```console
$ git push heroku master
```

You may see a message, "The authenticity of host 'heroku.com' can't be
established. Are you sure you want to continue connecting (yes/no)?".
You can answer "yes" and safely continue.

The push to Heroku takes several minutes. You'll see a sequence of
diagnostic messages in the console, beginning with:


```console
Counting objects...
```

and finishing with:


```console
remote: Verifying deploy.... done.
```

Updating the Application
------------------------

It is likely you'll make changes to your application after deploying to
Heroku.

Each time you update your site and push the changes to GitHub, you'll
also have to push the new version to Heroku. A typical
update scenario looks like this:

```console
$ git add -A
$ git commit -m "revised application"
$ git push
$ git push heroku master
```

Visit Your Site
---------------

Your application will be running at
[http://my-app-name.herokuapp.com/](http://my-app-name.herokuapp.com/).
You can open any web browser and visit the site. For a shortcut, you can
open your default web browser and visit your site from the command line:


```console
$ heroku open
```

If you're using hosted development such as Cloud9, you'll need to open a
browser manually to visit the site.

If you've configured everything correctly, you should be able to sign up
for the newsletter and send a contact request.

Customizing
-----------

For a real application, you'll likely want to use your own domain name
for your app.

See [Heroku's article about custom
domains](https://devcenter.heroku.com/articles/custom-domains) for
instructions.

You may also want to improve website responsiveness by adding page
caching with a content delivery network such as
[CloudFlare](http://cloudflare.com/). CloudFlare can also provide an SSL
connection for secure connections between the browser and server.

Heroku offers many [add-on services](https://addons.heroku.com/). These
are particularly noteworthy:

-   [Adept Scale](http://www.adeptscale.com/) - automated scaling of Heroku dynos
-   [New Relic](http://newrelic.com/) - performance monitoring

For an in-depth look at your options, see the [Rails Heroku
Tutorial](http://railsapps.github.io/rails-heroku-tutorial.html).

Troubleshooting
---------------

When you get errors, troubleshoot by reviewing the log files:


```console
$ heroku logs
```

If necessary, use the Unix `tail` flag to monitor your log files. Open a
new terminal window and enter:


```console
$ heroku logs -t
```

to watch the server logs in real time.

Where to Get Help
-----------------

Your best source for help with Heroku is [Stack
Overflow](http://stackoverflow.com/questions/tagged/heroku). Use the tag
"heroku," "learn-ruby-on-rails," or "railsapps" when you post your
question. Your issue may have been encountered and addressed by others.

You can also check the [Heroku Dev Center](http://devcenter.heroku.com/)
or the [Heroku Google Group](http://groups.google.com/group/heroku/).
