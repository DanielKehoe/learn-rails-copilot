Send Mail
=========

Email sent from a web application is called [transactional
email](http://blog.mailchimp.com/what-is-transactional-email/). As a
website visitor, you've probably seen transactional email such as these
messages:

-   sign up confirmation email
-   response to a password reset request
-   acknowledgment of a purchase
-   notice of a change to a user profile setting

A web application can send email to a visitor. It can also send messages
to its owner or webmaster. On large active sites, email notices can be
impractical (an admin interface is better) but for our small-volume
tutorial application, it makes sense to email the contact request
directly to the site owner (Foobar Kadigan is retired and enjoys
receiving email).

User Story
----------

Let's plan our work with a user story:


```cucumber
*Send Contact Message*
As the owner of the website
I want to receive email messages with a visitor's name, email address, and some text
In order to communicate with visitors
```

To implement the user story, let's create a feature that sends the
contact data as an email message.

Implementation
--------------

Rails makes it easy to send email. The
[ActionMailer](https://github.com/rails/rails/tree/master/actionmailer)
gem is part of any Rails installation.

Implementation of email closely follows the model-view-controller
architecture. To implement email, you'll need:

-   model
-   view
-   mailer

The "mailer" is similar to a controller, combining data attributes from
a model with a view file. Any methods we add to the mailer class can be
called from a controller, triggering delivery of an email message.

The model can be any we've already created. In this case, we'll use the
Contact model, since it gives us access to the visitor's name, email
address, and message.

We'll create a mail-specific view file in the
**app/views/user_mailer/** folder. Our folder for mail-specific views
will go in the **app/views/** directory as a sibling of the
**app/views/layouts** folder.

The Rails directory structure already gives us a folder **app/mailers/**
for the mailer class and, not surprisingly, it is a sibling of the
**app/controllers/** folder.

We don't have to create the necessary folders and files manually, as the
`rails generate` command runs a utility to create what we need.

Create View Folder and Mailer
-----------------------------

Use the `rails generate` command to create a mailer with a folder for
views:


```console
$ rails generate mailer UserMailer
```

The name of the mailer isn't important; we'll use `UserMailer` because
it is obvious.

The `rails generate` command will create a file:

-   **app/mailers/user_mailer.rb**

It also creates test files which we won't use in this tutorial.

It uses three additional files which are provided by default in a Rails 5 application:

-   **app/mailers/application_mailer.rb**
-   **app/views/layouts/mailer.html.erb**
-   **app/views/layouts/mailer.text.erb**

This implements our model-view-mailer architecture.

Edit the Mailer
---------------

Add a `contact_email` method to the mailer by editing the file
**app/mailers/user_mailer.rb**:


```ruby
class UserMailer < ApplicationMailer
  default from: "do-not-reply@example.com"

  def contact_email(contact)
    @contact = contact
    mail(to: Rails.application.secrets.owner_email, from: @contact.email, :subject => "Website Contact")
  end
end
```

The `UserMailer` class inherits behavior from the `ApplicationMailer` class.
We'll create a method definition that assigns the `contact` argument to
the instance variable `@contact`. Like a controller that combines a
model with a view, our mailer class makes the instance variable
available in the view.

The name of the method isn't important; it can be anything obvious.
We'll use it in the ContactsController to trigger mail delivery.

Like the `render` method in a web page controller, the ActionMailer
parent class has a `mail` method that renders the view.

You'll need to use your email address in the mailer. You should have
already set a configuration variable for your email address in the file
**config/secrets.yml**. If you haven't done so, do it now. By inserting
the configuration variable with your email address after `to:`, your
inbox will receive the message. If Foobar Kadigan was a real person,
we'd supply his email address here.

We need to insert a "from" address in two places. First there is a
default, for all messages that do not set a "from" address. We will use
"do-not-reply@example.com" for the default "from" address. The email is
originating from a web application that does not receive email, so this
indicates the email address should not be used for replies. For emails
going to website visitors, it would be best to provide a default email
address for a customer service representative on the "from" line, so the
recipient can easily reply. We're not sending email messages to visitors
so we can ignore this nicety.

For our `contact_email` method, we'll insert the email address of the
visitor as the "from" address since we are sending a message to the site
owner. This makes it easy for Foobar Kadigan to click "reply" when he is
reading the contact messages in his inbox. You can see our use of the
email attribute from the Contact model in the expression
`from: @contact.email`.

That's all we need for mailer class. Next we'll create a view containing the message.

## Create Mailer View

There are two types of mailer views. One contains plain text, for recipients who don't like formatted email (some people still read email from the Unix command line). The other type contains HTML markup to provide formatting. It's good to create a message of both types, though most recipients will benefit from HTML formatting.

The mailer view for formatted email looks very similar to a web page view file. It contains HTML markup plus Ruby expressions embedded in `<%= ... %>`
delimiters. In the `UserMailer` class, we've assigned the Contact model
to the instance variable `@contact` so any attributes are available for
use in the message.

Create a file **app/views/user_mailer/contact_email.html.erb**:


```erb
<!DOCTYPE html>
<html>
  <head>
    <meta content="text/html; charset=UTF-8" http-equiv="Content-Type" />
  </head>
  <body>
    <h1>Website Contact</h1>
    <p>
      This visitor requested contact:
    </p>
    <p>
      <%= @contact.name %><br/>
      <%= @contact.email %><br/>
    </p>
    <p>
      The visitor said:
    </p>
    <p>
      "<%= @contact.content %>"
    </p>
  </body>
</html>
```

You can easily imagine how this view would look as a web page. You'll
soon see it as an email message in your inbox.

For those recipients who like plain text, create a view without HTML
markup.

Create a file **app/views/user_mailer/contact_email.text.erb**:


```erb
You received a message from <%= @contact.name %> with email address <%= @contact.email %>.

The visitor said:

"<%= @contact.content %>"
```

You've created views for the email message.

Now we can integrate our email feature with the ContactsController.

Modify Controller
-----------------

We'll add code to the ContactsController:


```ruby
UserMailer.contact_email(@contact).deliver_now
```

Replace the contents of the file
**app/controllers/contacts_controller.rb**:


```ruby
class ContactsController < ApplicationController

  def new
    @contact = Contact.new
  end

  def create
    @contact = Contact.new(secure_params)
    if @contact.valid?
      UserMailer.contact_email(@contact).deliver_now
      flash[:notice] = "Message sent from #{@contact.name}."
      redirect_to root_path
    else
      render :new
    end
  end

  private

  def secure_params
    params.require(:contact).permit(:name, :email, :content)
  end

end
```

The `UserMailer` class is available to any controller in the
application. We call the `contact_email` method we've created, passing
the `@contact` instance variable as an argument, which renders the email
message. Finally, the `deliver_now` method initiates delivery.

For more on sending email from a Rails application, see [RailsGuides:
Action Mailer
Basics](http://guides.rubyonrails.org/action_mailer_basics.html).

Test the Application
--------------------

If your web server is not running, start it:


```console
$ rails server
```

Open a web browser window and navigate to
[http://localhost:3000/](http://localhost:3000).

Click the "Contact" link and try submitting the form.

The email message should be visible in the console.

If you didn't get an email message in your inbox, make sure you set your
**config/environments/development.rb** file to perform deliveries as
described in the "Configuration" chapter. Be sure to restart your server
if you change the configuration file.

Troubleshooting
--------------------

If you get an error, you can practice troubleshooting. You've set up a complex system with many dependencies. It's great if it works, but there are several opportunities for errors.

The most likely errors are a missing user name or password. We are trying to connect to the SendGrid email service. SendGrid expects your SendGrid user name. Mine is `DanielKehoe` (it is not my email address). SendGrid also expects a password.

### User Name Issues

If you get the error message, "SMTP-AUTH requested but missing user name," SendGrid is not receiving a user name it recognizes.

Check that the user name is set in your Unix environment variables:

```console
$ echo "$SENDGRID_USERNAME"
```
You should see your SendGrid user name.

Make sure you've used underscores consistently. If your Unix environment variable is `SENDGRID_USER_NAME` and the **config/secrets.yml** file contains `SENDGRID_USERNAME`, you'll have a problem.

### Password Issues

If you get the error message, "SMTP-AUTH requested but missing secret phrase," SendGrid is not receiving the SendGrid password.

Check that the SendGrid password is set in your Unix environment variables:

```console
$ echo "$SENDGRID_PASSWORD"
```
You should see the long cryptic string in the console response. Again, make sure you've used underscores consistently, and `SENDGRID_PASSWORD` is used for the Unix environment variable as well as the **config/secrets.yml** file.

### Problems with Environment Variables

First, close and reopen your terminal to make sure your environment reflects any recent changes you've made to your shell configuration. Then try `echo "$SENDGRID_USERNAME"` to see if you get the credentials you set in your **.bash_profile** or **.bashrc** files.

If you've set up Unix environment variables but `echo "$SENDGRID_USERNAME"` doesn't return the correct variable in the console, you may have a problem with the way you've set Unix environment variables. Most computers use the bash shell and you can set environment variables in your **.bash_profile** or **.bashrc** files. But not every system is alike. If it seems Unix environment variables are not working, you may have to find a colleague who can help you troubleshoot.

If your Unix environment variables are not working, you can hardcode the variables in your **config/secrets.yml** file:

Replace the following:

```yaml
development:
  email_provider_username: <%= ENV["SENDGRID_USERNAME"] %>
  email_provider_password: <%= ENV["SENDGRID_PASSWORD"] %>
```

with:

```yaml
development:
  email_provider_username: example
  email_provider_password: 's#cr*t'
```
In a YAML file, you do not need quotes unless your string contains special characters. If your password contains any of these characters you should surround the string with single quotes:

```console
: { } [ ] & * # ? | - < > = ! % @ \
```

Remember the security rule: Don't commit the **config/secrets.yml** file to Git if it contains any secrets. Test the application and finish your troubleshooting. Then remove the hardcoded values from the **config/secrets.yml** file before committing to Git.

Asynchronous Mailing
--------------------

You may notice a delay in the responsiveness of the Contact form after
adding the email feature. Unfortunately, there's a performance penalty
with our new feature. Our controller code connects to the SendGrid server
and waits for a response before it renders the home page and displays
the acknowledgment message.

The performance penalty can be avoided by changing the implementation so
that the controller doesn't wait for a response from the SendGrid server.
We call this *asynchronous* behavior because sending email does not need
to be "in sync" with displaying the acknowledgment. Eliminating a delay
improves the user experience and makes the site feel more responsive.
Asynchronous mailing requires a <em>queueing system</em> for
<em>background jobs</em>.

For our tutorial application, and for a typical small business website,
the delay caused by lack of queueing is no big deal. Keep in mind,
though, as you tackle bigger projects in Rails, you will need to
implement a queueing system. Rails includes the [Active Job](https://github.com/rails/rails/tree/master/activejob) feature for background processing. The [Mailing List with Active Job](https://tutorials.railsapps.org/tutorials/rails-mailinglist-activejob) tutorial in the [Capstone Rails Tutorials](https://tutorials.railsapps.org/) series explains how to use it.

Git
---

Let's commit our changes to the Git repository and push to GitHub:


```console
$ git add -A
$ git commit -m "sending mail"
$ git push
```

You've created a Rails application that handles a form and sends email
to the site owner.

Mail is a practical way to connect with site visitors. Let's implement a
feature that collects email addresses for mass mailing of a newsletter.
