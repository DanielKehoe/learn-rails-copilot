Configure
=========

Rails is known for its "convention over configuration" guiding
principle. As applied, the principle reduces the need for many
configuration files. It's not possible to eliminate all configuration
files, however. Many applications require configuration of settings such
as email account credentials or API keys for external services.

In our tutorial application, we'll need to store an API key to access MailChimp, which we'll use
to add visitors' email addresses to a mailing list. We'll also need to store credentials so we can send email using
the SendGrid transactional email service.

Rails provides the **config/secrets.yml** file for our configuration
settings. Any variable that is set in the **config/secrets.yml** file
can be used elsewhere in our Rails application, providing a single
location for all our configuration variables.

Configuration Security
----------------------

GitHub is a good place to store and share code. But when your repos are
public, they are not a good place for secret account credentials. In
fact, any shared Git repository, even a private repo, is a bad place to
store email account credentials or private API keys.

Operating systems (Linux, macOS, Windows) provide mechanisms to set
local [environment variables](http://en.wikipedia.org/wiki/Environment_variable), as does
Heroku and other deployment platforms. With a bit of Unix savvy, you can
set environment variables using the Unix shell. Environment variables
can be accessed from Rails applications and provide an ideal place to
set configuration settings that must remain private.

For the best security, set credentials as Unix environment variables and
only use Unix environment variables in the **config/secrets.yml** file.

The article [Rails Environment
Variables](http://railsapps.github.io/rails-environment-variables.html)
shows alternatives to using Unix environment variables, if for any
reason you cannot set environment variables on your machine.

## Videos

If you have subscribed, now's a good time to watch:

- [UNIX Environment Variables](https://tutorials.railsapps.org/videos/7)
- [Rails Environment Variables](https://tutorials.railsapps.org/videos/8)

About Environment Variables
---------------------------

Unix environment variables are typically set in a file that is read when
starting an interactive shell. The *shell* is the program that gives us
the command line interface we see in the Terminal or console
application. Unix gives you a choice of shell programs (with names like
*sh*, *bash*, *ksh*, and *zsh*); each has a slightly different way to
set environment variables. The most common shell program is bash.

Let's find out what shell you are using:


```console
$ echo $SHELL
/bin/bash
```

If you see `/bin/bash`, that's great! If not, you may have to do some
research to find out how to set environment variables in your shell.

You might be surprised to see a dollar sign in the command. You don't type the
first dollar sign (it is just the convention that indicates you are entering a
Unix command). You'll type `echo $SHELL` to ask the operating system to show the
variable `SHELL`. The dollar sign in the command tells Unix to return a variable
named `SHELL`. Try typing `echo SHELL` without the dollar sign and you'll see
`echo` just displays what you type.

When you open a console window, the bash shell reads a configuration
file in your user home directory. You can use a Unix command to list all
the files in your user home directory (the `\textasciitilde` "tilde" character
represents your home directory):


```console
$ ls -1pa ~
.
.
.
.bash_profile
.
.
.
```

On the Mac, you'll see **.bash_profile**. On Linux systems, you'll see **.bashrc**.

Viewing Hidden Files
-------------------------

The files **.bash_profile** or **.bashrc** are hidden in the file
browser. You can force the Mac to display hidden files by entering the following
command in the Terminal application:

```console
defaults write com.apple.finder AppleShowAllFiles TRUE; killall Finder
```
Hidden files will appear in gray in the Finder window.

Use your text editor (Atom or Sublime) to open the **.bash_profile** or
**.bash_rc** file.

To open the **.bash_profile** file with Atom:

```
$ atom ~/.bash_profile
```

In Unix, the squiggle (tilde) character is a shortcut to your user home folder.

Open either file and you'll likely find a command such as:

```console
export PATH=~/.bin:$PATH
```

That is a command that sets the `PATH` environment variable. The command
might not be exactly the same but it is likely you will see some
`export` commands.

You can add the environment variables anywhere in the file. For convenience,
add the environment variables near the end of the file, above any existing
`EXPORT` statement.

You should use quotes to surround configuration values (credentials) in
the **.bash_profile** or **.bashrc** files.

If you don't have a **.bash_profile** or **.bashrc** file in your user
home directory, you can create one.

Set Environment Variables
-------------------------

You'll set the following environment variables in your **.bashrc** or
**.bash_profile** file:

* SENDGRID_USERNAME
* SENDGRID_PASSWORD
* MAILCHIMP_API_KEY
* MAILCHIMP_LIST_ID
* OWNER_EMAIL

Here are details.

### SendGrid

You'll need your SendGrid username and password. The credentials are the same you use to sign in to the SendGrid website.

Add your SendGrid username and password to your **.bash_profile** or **.bashrc** file:

```console
export SENDGRID_USERNAME="example"
export SENDGRID_PASSWORD="secret"
```
Obviously, change "example" and "secret" to your own credentials.

### MailChimp

When visitors sign up to receive a newsletter, we'll add them to a MailChimp list. Add an environment variable for the MailChimp API key: `MAILCHIMP_API_KEY`. [Sign in to MailChimp](https://admin.mailchimp.com/) to get your API key. Click your name at the top of the navigation menu, then click "Account." Click "Extras," then "API keys." You have to generate an API key; MailChimp doesn't create one automatically. The MailChimp API key is a long string of characters like a secret code that works like a password. Enter it in your **.bash_profile** or **.bashrc** file:

```console
export MAILCHIMP_API_KEY="Your_MailChimp_API_Key"
```

You'll need to create a MailChimp mailing list in preparation for our "Mailing List" chapter. Have you already created a MailChimp mailing list? If not, the MailChimp "Lists" page has a button for "Create List." The list name and other details are up to you.

We'll need the `MAILCHIMP_LIST_ID` for the mailing list you've
created. To find the list ID, on the MailChimp "Lists" page, click the
"down arrow" for a menu and click "Settings." At the bottom of the "List
Settings" page, you'll find the unique ID for the mailing list.

```console
export MAILCHIMP_LIST_ID="Your_List_ID"
```
Your environment variables are set up to use MailChimp.

### Owner Email

You'll send email messages to this address when a visitor submits a
contact request form. Set `OWNER_EMAIL` with an email address where you
receive mail.

```console
export OWNER_EMAIL="example@example.com"
```
Enter an email address and your environment variables will be set up with the site owner email address.

### Restart the Terminal Session

Close and reopen your terminal to make sure the environment is updated with any recent changes.

### Troubleshooting

Check that the SendGrid user name is set in your Unix environment variables:

```console
$ echo "$SENDGRID_USERNAME"
```
You should see your SendGrid user name in the console response. Make sure you've used underscores consistently and you've used `SENDGRID_USERNAME` not `SENDGRID_USER_NAME`.

If you have trouble, remember to close and reopen your terminal to make sure the environment includes any recent changes.

On Linux, if you've entered the environment variables in your **.bashrc** file but they don't seem to work, try setting them in your  **.bash_profile** file instead.

If you've set up Unix environment variables but `echo "$SENDGRID_USERNAME"` doesn't return the correct variable in the console, you may have a problem with the way you've set Unix environment variables. Most computers use the bash shell and you can set environment variables in your **.bash_profile** or **.bashrc** files. But not every system is alike. If it seems Unix environment variables are not working, you may have to find a colleague who can help you troubleshoot. If you are having problems, you can continue with the tutorial and add the credentials directly to the **config/secrets.yml** file.

The Secrets File
----------------

Use your text editor to add the Unix environment variables to the file
**config/secrets.yml**:


```yaml
# Be sure to restart your server when you modify this file.

# Your secret key is used for verifying the integrity of signed cookies.
# If you change this key, all old signed cookies will become invalid!

# Make sure the secret is at least 30 characters and all random,
# no regular words or you'll be exposed to dictionary attacks.
# You can use `rails secret` to generate a secure secret key.

# Make sure the secrets in this file are kept private
# if you're sharing your code publicly.

# Shared secrets are available across all environments.

# shared:
#   api_key: a1B2c3D4e5F6

# Environmental secrets are only available for that specific environment.

development:
  email_provider_username: <%= ENV["SENDGRID_USERNAME"] %>
  email_provider_password: <%= ENV["SENDGRID_PASSWORD"] %>
  domain_name: example.com
  mailchimp_api_key: <%= ENV["MAILCHIMP_API_KEY"] %>
  mailchimp_list_id: <%= ENV["MAILCHIMP_LIST_ID"] %>
  owner_email: <%= ENV["OWNER_EMAIL"] %>
  secret_key_base: very_long_random_string

test:
  secret_key_base: very_long_random_string

# Do not keep production secrets in the unencrypted secrets file.
# Instead, either read values from the environment.
# Or, use `bin/rails secrets:setup` to configure encrypted secrets
# and move the `production:` environment over there.

production:
  email_provider_username: <%= ENV["SENDGRID_USERNAME"] %>
  email_provider_password: <%= ENV["SENDGRID_PASSWORD"] %>
  domain_name: example.com
  mailchimp_api_key: <%= ENV["MAILCHIMP_API_KEY"] %>
  mailchimp_list_id: <%= ENV["MAILCHIMP_LIST_ID"] %>
  owner_email: <%= ENV["OWNER_EMAIL"] %>
  secret_key_base: <%= ENV["SECRET_KEY_BASE"] %>

```

Be sure to use spaces, not tabs. Make sure there is a space after each
colon and before the value for each entry or you will get a message
"Internal Server Error: mapping values are not allowed" when you start
the web server.

You used quotes to surround configuration values in the **.bashrc** or
**.bash_profile** files. Here, in the **config/secrets.yml** file, you
don't need quotes when you are importing Unix environment variables.

### Domain Name

We'll need a domain name when we configure email for delivery in
production. For development, use `example.com`. If you have your own
domain name, you can use that instead. There's no need to keep the
`domain_name` configuration variable secret, so we don't need to set it
in a Unix environment variable.

You can decide for yourself if the `owner_email` variable really needs
to be secret. Just for caution, I'm suggesting you set it as a Unix
environment variable.

### Securing the Secrets File

Some developers take steps to prevent the **config/secrets.yml** file
from being checked into Git. To prevent the file from being saved to
your repo you could add the filename to the **.gitignore** file in your
application root directory.

However, you don't need to keep the **config/secrets.yml** file
from being checked into Git if you've used Unix environment variables
in the **config/secrets.yml** file. If you only
reveal the `SECRET_KEY_BASE` used for development or testing, and no one
can access your development machine, no useful secrets will be revealed
in your GitHub repo.

When you deploy to Heroku, the **config/secrets.yml** file must be in
your Git repository. For that reason, I suggest you save the file in
your Git repo and keep your secrets safe by using environment variables.

### Troubleshooting

Remember, in YAML files (with the file extension **.yml**), indentation
is required (your application will break without it).

Be sure to use spaces, not tabs. Make sure there is a space after each
colon and before the value for each entry.

If you have trouble setting Unix environment variables, you can add
credentials directly to the **config/secrets.yml** file. If you do so,
you should not check the file into Git until you've deleted the secrets
from the file.

Replace the following if you are troubleshooting:

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

Again, DON'T CHECK THE FILE INTO GIT if you've hardcoded your
credentials directly in the **config/secrets.yml** file.

The article [Rails Environment Variables](http://railsapps.github.io/rails-environment-variables.html)
shows alternatives to using Unix environment variables, if for any
reason you cannot set environment variables on your machine.

Secret Key Base
---------------

It's not necessary to set `SECRET_KEY_BASE` as an environment variable
on the computer you use for development. Rails generates a unique
`SECRET_KEY_BASE` in the **config/secrets.yml** file each time you
create a new Rails application and you don't need to replace it. If
someone sees the `SECRET_KEY_BASE` in the **config/secrets.yml** file in
your GitHub repo, there isn't anything they can do with it, since they
don't have access to your local machine.

For your future reference, in case you want to change the
`SECRET_KEY_BASE`, here's how. Go to your Rails application directory
and create a new secret token:


```console
$ rails secret
very_long_random_string
```

And, if you wish, add it to your **.bash_profile** or **.bashrc** file:


```console
export SECRET_KEY_BASE="very_long_random_string"
```

You should always use the environment variable
`<%= ENV["SECRET_KEY_BASE"] %>` in the production section of your
**config/secrets.yml** file, otherwise, someone who sees the secret
token in your GitHub repo can gain access to your application in
production. You'll set the environment variables for production when you
deploy to Heroku.

Configure Email
---------------

Email messages are visible in the console and the log file when you test
the application. If you don't want to actually send email, you can skip
this step. But it's more fun when your application can actually send
email.

You can learn more in the article [Send Email with Rails](http://railsapps.github.io/rails-send-email.html).

### Connect to an Email Server

Web servers don't send email. Our Rails application has to connect to an
email server (also known as a [mail transfer agent](http://en.wikipedia.org/wiki/Email_server) or "mail relay"). In
the early days of the Internet, an experienced system administrator
could set up an [SMTP server](http://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol) to
distribute email. Now, because of efforts to reduce spam, it is
necessary to use an established email service to ensure deliverability.
In production, for high volume transactional email and improved
deliverability, it is best to use a service such as [SendGrid](https://sendgrid.com/). Alternatives are:

* [Amazon SES (Simple Email Service)](http://aws.amazon.com/ses/)
* [Mailgun](http://mailgun.net/pricing)
* [Mailjet](http://mailjet.com/)
* [Mandrill](http://mandrill.com/)
* [PostageApp](http://postageapp.com/)
* [Postmark](https://postmarkapp.com/)
* [SparkPost](https://www.sparkpost.com/)

For our tutorial application, we'll connect to SendGrid to send email.

For convenience during development, some developers use their own Gmail account to send email. Google has increased security measures for Gmail, so it is difficult to use Gmail to send email from a Rails application. SendGrid is easier to set up and you're more likely to use it for a real application. That's why we'll use it.

In the file **config/environments/development.rb**, near the end of the
file, find the statement:

```ruby
config.assets.debug = true
```

Immediately following, add this:

```ruby
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
config.action_mailer.default_url_options = { :host => 'localhost:3000' }
config.action_mailer.delivery_method = :smtp
config.action_mailer.raise_delivery_errors = true
# Send email in development mode?
config.action_mailer.perform_deliveries = true
```

You can use port 25, 587, or 2525 (some ISPs restrict connections on port 25).

It's important to add these changes in the body of the configuration
file, before the `end` keyword. The order isn't important but don't add
the configuration statements after the `end` keyword.

Notice that we are using configuration variables that are set in
the **config/secrets.yml** file:

-   Rails.application.secrets.email_provider_username
-   Rails.application.secrets.email_provider_password

We could "hard code" a username and password here but that would expose
confidential data if your GitHub repository is public. Using
configuration variables that are set in the **config/secrets.yml** file
keeps your secrets safe.

Again, if you need to troubleshoot, you can enter the SendGrid username and password
directly in this file instead of the configuration variables. But for security, don't commit to
Git with the password hardcoded in this file.

### Perform Deliveries in Development

If you want to send real messages when you test the application in
development mode, modify the file
**config/environments/development.rb**.

After the code you just added, add the statement:


```ruby
# Send email in development mode?
config.action_mailer.perform_deliveries = true
```

This changes the configuration to send email when you're working on the
application.

Make sure any code you've added to the
**config/environments/development.rb** file is placed before the final
`end` keyword. If you add code after the final `end` keyword, your
application will fail with errors when you start the web server.

Later, after we add a contact form to the tutorial application, the
application will be ready to send email messages.

Git
---

Make sure you're in your application root directory.

Let's commit our changes to the Git repository and push to GitHub:


```console
$ git add -A
$ git commit -m "add configuration"
$ git push
```

We're ready to create a home page for the application.
