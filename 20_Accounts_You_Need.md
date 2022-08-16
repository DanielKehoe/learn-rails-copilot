Accounts You May Need
=====================

You'll need accounts with four services before you begin building the application in this book.

This tutorial will show you how to save your work using
[GitHub](https://github.com/). You can sign up for a GitHub account for
free. Every experienced Rails developer has a GitHub account; it is where we
collaborate on our code, both commercial and open source projects.

We'll create a form that allows website visitors to "opt-in" to a
mailing list. You'll need a [MailChimp](http://mailchimp.com/) account,
which is free. If you send email to a mailing list, you will find it is
useful to have an account with MailChimp or a similar service.

We'll also send email from the application, which will require a
[SendGrid](https://sendgrid.com/) account. SendGrid is a transactional email service that lets you send email messages efficiently and reliably. SendGrid offers a free account that allows you to send 12,000 messages per month for free.

Finally, we'll deploy the tutorial application to
[Heroku](https://www.heroku.com/) which provides Rails application
hosting. It costs nothing to set up a Heroku account and deploy as many
applications as you want. It is the easiest way to deploy a Rails application and most Rails
developers use Heroku at some time in their careers.

GitHub
------

Rails developers use [GitHub](https://github.com/) for collaboration and
remote backup of projects.

For this tutorial, I suggest you get a [free personal GitHub account](https://github.com/signup/free) if you don't already have one.
As a developer, your GitHub account establishes your reputation in the
open source community. If you're seeking a job as a developer, employers
will look at your GitHub account. When you work with other developers,
they may check to see what you've worked on recently. Don't be reluctant
to set up a GitHub account, even if you're a beginner. It shows you are
serious about learning Rails.

You'll be asked to provide a username. This can be a nickname or short
version of your real name (for example, your Twitter username).

You'll be asked to provide an email address. It's very important that
you use the same email address for your GitHub account that you use to
configure Git locally (there will be more about configuring Git later).
If you create a Heroku account to deploy and host your Rails
applications, you should use the same email address.

After you create your GitHub account, log in and look for the button
"Edit Your Profile." Take a few minutes to add some public information
to your account. It is really important to provide your real name and a
public email address. Displaying your real name on your GitHub account
makes it easy for people to associate you with your work when they meet
you in real life, for example at a meetup, a hackathon, or a conference.
Providing a public email address makes it possible for other developers
to reach you if you ask questions or submit issues. If you can, provide
a website address (even just your Twitter or Facebook page). In general,
you won't be exposed to stalkers or spammers (except some recruiters) if
you are open about yourself on GitHub.

Later I'll show you how to set up and use Git and GitHub.

MailChimp
---------

This tutorial shows how website visitors can sign up to receive a
newsletter provided by a [MailChimp](http://mailchimp.com/) mailing
list. MailChimp allows you to send up to 12,000 emails/month to a list
of 2000 or fewer subscribers for free. There is no cost to set up an
account.

MailChimp will ask you to provide a website address and company details
for your account. These details are included when email messages are
sent to your subscribers. If you don't have your own website, you can
enter the URL for your GitHub account for now. Use your own name for
a company if you don't have one.

After you have set up a MailChimp account, create a new mailing list
where you can collect email addresses of visitors who have asked to
subscribe to a newsletter. The MailChimp "Lists" page has a button for
"Create List." The list name and other details are up to you.

If you get frustrated with the complex and confusing MailChimp
interface, try to remember that the friendly MailChimp monkey is
laughing with you, not at you.

SendGrid
-----

Earlier editions of this book showed how to use a [Gmail](https://accounts.google.com/SignUp?service=mail)
account to send email from the application. Google has taken steps to make Gmail more secure and now
it can be difficult to send email from a Rails application using Gmail.

This tutorial provides instructions for [SendGrid](https://sendgrid.com/). SendGrid offers a free account that allows you to send 12,000 messages per month for free.

Scroll to the bottom of the [SendGrid pricing page](https://sendgrid.com/pricing) to see details about the free plan. Click the "Try for Free" link to set up an account. No credit card is needed.

Heroku
------

We'll use [Heroku](https://www.heroku.com/) to host the tutorial
application so anyone can reach it.

To deploy an app to Heroku, you must have a Heroku account. Visit
[https://signup.heroku.com/devcenter](https://signup.heroku.com/devcenter)
to set up an account.

Be sure to use the same email address you used to register for GitHub.
It's very important that you use the same email address for GitHub and
Heroku accounts.
