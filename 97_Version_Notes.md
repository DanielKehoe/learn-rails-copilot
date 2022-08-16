Version Notes
=============

If you are reading the online edition of the book,
you have the most recent version of the book. If
you've gotten your copy of the book elsewhere, you may have an older
version that doesn't have the newest updates.

You'll find the version number and release date on the first page of this book (under the book title).
Check the [learn-rails GitHub repository](https://github.com/RailsApps/learn-rails) to find out
if you have the newest version of the book. The README page on the GitHub repo always
shows the most recent version number for the book and the tutorial application.

If you have trouble building the application in this book, and suspect something may be out of date,
you can [check the Gemfile in the repo](https://github.com/RailsApps/learn-rails/blob/master/Gemfile) to
see if we've changed gems or specified version numbers to avoid
compatibility issues. You can also check the
[CHANGELOG](https://github.com/RailsApps/learn-rails/blob/master/CHANGELOG.textile),
look at [recent commits](https://github.com/RailsApps/learn-rails/commits/master), and
[check the issues](https://github.com/RailsApps/learn-rails/issues) to
see the current state of the application.

Here are the changes I've made.

Version 4.2.0
-------------

*Version 4.2.0 was released August 2, 2017*

Additional revisions to accommodate Rails 5.1 `form_with`.

Add the jquery-rails gem for the jQuery JavaScript library because it was dropped as a default gem from Rails 5.1.

Minor revisions and corrections for clarity.

Version 4.1.0
-------------

*Version 4.1.0 was released July 3, 2017*

Updated for Rails 5.1 and Ruby 2.4.1.

Removed SimpleForm and replaced with Rails 5.1 `form_with`.

No need to configure MiniTest for Capybara (included in Rails 5.1).

Version 4.0.2
-------------

*Version 4.0.2 was released November 25, 2016*

Minor revisions for clarity.

Apple now calls the operating system macOS not Mac OS X.

Updated for Ruby 2.3.2.

Version 4.0.1
-------------

*Version 4.0.1 was released November 4, 2016*

Fixed broken links.

Removed references to [Nitrous.io](https://www.nitrous.io/) because Nitrous.io is out of business.

Version 4.0.0
-------------

*Version 4.0.0 was released October 31, 2016*

Updated for Rails 5.0 and Ruby 2.3.1.

Switch to using Bootstrap instead of Zurb Foundation front-end framework.

Extensive revisions.

Version 3.1.0
-------------

*Version 3.1.0 was released March 1, 2016*

Switch to using the SendGrid service to send email. Mandrill is no longer offering a free trial.

Version 3.0.2
-------------

*Version 3.0.2 was released January 30, 2016*

Minor change: 'email_provider_username' was 'mandrill_username' and email_provider_api_key' was 'mandrill_apikey'.

Version 3.0.1
-------------

*Version 3.0.1 was released January 29, 2016*

Specify version 5.5 of the foundation-rails gem. Foundation 6 is out but Zurb has not yet released documentation for migration from Foundation 5 to 6.

Version 3.0.0
-------------

*Version 3.0.0 was released January 14, 2016*

Extensive revision throughout the book, and the length of the book increased, so the book is now two books.
Book One contains the introductory and self-help chapters and can be read without access to a computer.
Book Two contains the step-by-step tutorial and requires use of a computer.

Switch to using the Mandrill service to send email. Previously used Gmail but Google has taken steps to make Gmail more secure and now it can be difficult to send email from a Rails application using Gmail.

Sending mail now requires the method `deliver_now` instead of `deliver`. The UserMailer class now inherits from `ApplicationMailer`.

Updated references to Rails from version 4.2.4 to 4.2.5.

Updated references to Ruby from version 2.2.3 to 2.3.0.

Version 2.2.2
-------------

*Version 2.2.2 was released October 30, 2015*

In the "Front-End Framework" chapter, updated filename to
`1st_load_framework.css.scss` from `framework_and_overrides.css.scss` to
reflect a change in the rails_layout gem.

Version 2.2.1
-------------

*Version 2.2.1 was released September 19, 2015*

Updated references to Ruby from version 2.2.0 to 2.2.3.

Updated references to Rails from 4.2.0 to Rails 4.2.4.

Updated Visitor model `subscribe` method for the new Gibbon 2.0 API.

Recommending [Cloud9](https://c9.io/) instead of
[Nitrous.io](https://www.nitrous.io/) because Nitrous.io is no longer
free.

Version 2.2.0
-------------

*Version 2.2.0 was released June 6, 2015*

For Amazon customers, added an offer to access the online version or
download a PDF at [learn-rails.com](http://learn-rails.com/).

Google now requires use of OAuth 2.0 for application access to Google
Drive. The implementation is considerably more complex than the previous
implementation using a Gmail address and password. I've dropped the
"Spreadsheet Connection" chapter.

Minor clarification in the "Layout and Views" chapter.

Version 2.1.6
-------------

*Version 2.1.6 was released March 17, 2015*

Remove references to the Thin web server in the "Deploy" chapter.

Correct version number for `gem 'sass-rails'` in various Gemfile
listings. Fixes [issue 49](https://github.com/RailsApps/learn-rails/issues/49) and an error
"Sass::SyntaxError - Invalid CSS" when the Foundation front-end
framework is used.

In the "Testing" chapter, the file
*test/integration/home_page_test.rb* was missing
`require 'test_helper'`.

Updated "Rails Composer" chapter to describe new options.

Minor improvements and corrections of typos.

Version 2.1.5
-------------

*Version 2.1.5 was released March 4, 2015*

Use the Ruby 1.9 hash syntax in the `validates_format_of :email`
statement.

Minor improvements and corrections of typos.

Version 2.1.4
-------------

*Version 2.1.4 was released January 3, 2015*

Updated references to Ruby from version 2.1.5 to 2.2.0.

Specify the "v0" version of the google_drive gem in the "Spreadsheet
Connection" chapter.

Version 2.1.3
-------------

*Version 2.1.3 was released December 25, 2014*

Updated references to Rails 4.1.8 to Rails 4.2.0.

Version 2.1.2
-------------

*Version 2.1.2 was released December 4, 2014*

Released for sale as a Kindle book on Amazon, with new cover art (same
cat, though).

RailsApps Tutorials now named the [Capstone Rails
Tutorials](https://tutorials.railsapps.org/).

Updated references to Ruby from version 2.1.3 to 2.1.5.

Updated references to Rails 4.1.6 to Rails 4.1.8 (minor releases with
bug and security fixes).

Removed link to the (now defunct?) [Lowdown](http://lowdownapp.com/) web
application in the "Plan Your Product" chapter.

Changes to the "Asynchronous Mailing" section of "Send Mail" chapter to
describe Active Job in Rails 4.2.

Minor improvements to the "Dynamic Home Page," "Deploy," "Configure,"
"Troubleshoot," and "Create the Application" chapters.

Version 2.1.1
-------------

*Version 2.1.1 was released October 22, 2014*

Minor rewriting for clarity.

Updated "Precompile Assets" section of the "Deploy" chapter.

Mentioned [explainshell.com](http://explainshell.com/) in the "Get
Started" chapter.

Mentioned [Zeal](http://zealdocs.org/) as a Linux alternative to
[Dash](http://kapeli.com/dash).

Recommended book [Practicing Rails](https://www.justinweiss.com/book/)
by Justin Weiss.

Version 2.1.0
-------------

*Version 2.1.0 was released October 12, 2014*

Updated references to Ruby from version 2.1.1 to 2.1.3.

Updated references to Rails 4.1.1 to Rails 4.1.6 (minor releases with
bug and security fixes).

Four new chapters:

-   "Testing"
-   "Rails Composer"
-   "Crossing the Chasm"
-   "Level Up"

Use ActiveModel instead of the
[activerecord-tableless](https://github.com/softace/activerecord-tableless)
gem.

In the "Configuration" chapter, add a note to use spaces (not tabs) in
the **config/secrets.yml** file.

Updated "Gems" chapter to add a troubleshooting note to the "Install the
Gems" section (about errors with the Nokogiri gem).

Added a section on "Multiple Terminal Windows" to the "Create the
Application" chapter.

In the "Get Help When You Need It" chapter, updated the list of
recommended newsletters, replaced [rubypair.com](http://rubypair.com/)
with [codermatch.me](http://www.codermatch.me/), and added a section on
code review. Removed reference to defunct [Rails Development
Directory](http://www.railsdevelopment.com/).

Version 2.0.2
-------------

*Version 2.0.2 was released May 6, 2014*

Updated references to Rails 4.1.0 to Rails 4.1.1 (a minor release with a
security fix).

For Nitrous.io users, clarify that "http://localhost:3000/" means the
Preview browser window.

Update "Gems" chapter, section "Where Do Gems Live?" to add more
explanation.

Minor change to code in the "Mailing List" chapter, setting
'mailchimp_api_key' explicitly when instantiating Gibbon, for easier
troubleshooting.

Version 2.0.1
-------------

*Version 2.0.1 was released April 16, 2014*

Minor updates for Rails 4.1.0. Mostly small changes to the "Configure"
and "Front-End Framework" chapters.

Added an explanation that, in the **config/secrets.yml** file,
`domain_name` doesn't have to be kept secret and set as a Unix
environment variable.

Added a hint about passwords that use punctuation marks (plus a
completely irrelevant note about profanitype).

Replaced `Rails.application.secrets.gmail_username` with
`Rails.application.secrets.email_provider_username`. Also replaced
`gmail_password` with `email_provider_password`. Just trying to make
things a little more generic in case Gmail is not used as a provider.

Added a section explaining the horrid details of the
`config.assets.precompile` configuration setting in the
**config/application.rb** file. Please convey my displeasure to those
responsible for subjecting beginners to this travesty.

In the "Deploy" chapter, restored
`RAILS_ENV=production rake assets:precompile` because Rails 4.1.0 no
longer barfs on this.

Added resources to the "Get Help When You Need It" chapter.

Minor rewriting of the introduction.

Version 2.0.0
-------------

*Version 2.0.0 was released April 8, 2014*

Updated references to Ruby from version 2.1.0 to 2.1.1.

Updated the book to Rails 4.1. The application name is no longer used in
the **config/routes.rb** file.

Rails 4.1 changes the **app/assets/stylesheets/application.css.scss**
file. Updated the "Front-End Framework" chapter. Also expanded the
explanation of the Foundation grid.

In Rails 4.1, configuration variables are set in the
**config/secrets.yml** file. The Figaro gem is dropped, along with the
**config/application.yml** file. Updated the "Configure" chapter and
references to configuration variables throughout the book.

In the "Deploy" chapter, changed
`RAILS_ENV=production rake assets:precompile` to
`rake assets:precompile` to avoid the error "database configuration does
not specify adapter."

Updated "The Parking Structure" chapter with comments about "Folders of
Future Importance" that experienced developers often use: **test/**,
**spec/**, **features/**, **policies/**, and **services/**. Updated the
"Spreadsheet Connection" chapter to mention service-oriented
architectures (SOA).

Extended the section on "Limitations of Metaphors" in the "Just Enough
Ruby" chapter to include the example of gender when modeling a person.

Minor rewriting for clarity throughout.

Version 1.19
------------

*Version 1.19 was released February 1, 2014*

Updated the book to use Foundation 5.0. Foundation 5.0.3 was released
January 15, 2014 (earlier versions 5.0.1 and 5.0.2 were incompatible
with Rails Turbolinks and the Rails asset pipeline). Changed the Gemfile
to remove `gem 'compass-rails'` and replace `gem 'zurb-foundation'` with
`gem 'foundation-rails'`. Updated a line in the "Front-End Framework"
chapter for Foundation 5.0:


```console
$ rails generate layout foundation5 --force
```

The files **navigation.html.erb** and **application.html.erb** are
changed for Foundation 5.0.
The Bootstrap front-end framework is now independent of Twitter, so I
call it "Bootstrap" not "Twitter Bootstrap."
Revised the chapter "Just Enough Ruby" to incorporate suggestions from
technical editor Pat Shaughnessy.
Revised the chapter "Request and Response" to incorporate suggestions
from technical editor Kirsten Jones.
Minor rewriting for clarity throughout.

Version 1.18
------------

*Version 1.18 was released January 10, 2014*

Updated references to Ruby from version 2.0.0 to 2.1.0.
Changed one line in the "Front-End Framework" chapter to accommodate a
change in the rails_layout gem version 1.0.1.
The command was:

```console
$ rails generate layout foundation4 —force
```

Changed to:

```console
$ rails generate layout:install foundation4 —force
```

Updated the "Configure" chapter to add ActionMailer configuration values
to the file **config/environments/development.rb**.

Version 1.17
------------

*Version 1.17 was released December 21, 2013*

Updated Rails version from 4.0.1 to 4.0.2 .

Changed Gemfile to remove `gem 'compass-rails', '> 2.0.alpha.0'` and
replace it with `gem 'compass-rails', '> 1.1.2'`. The 2.0.alpha.0
version was yanked from the RubyGems server. The compass-rails gem is
needed for Foundation 4.3. It will not be needed for Foundation 5.0.

Changed Gemfile to replace `gem 'zurb-foundation'` with
`gem 'zurb-foundation', '> 4.3.2'`. Foundation 5.0 will require
`gem 'foundation-rails'` but we can't use it until an [incompatibility with Turbolinks](https://github.com/zurb/foundation/issues/3642) is
resolved. So we will stick with Foundation 4.3.2 for now.

Revised code in the "Analytics" chapter. Using `ready page:change`
instead of `page:load` to accommodate Turbolinks. Updated
the **segmentio.js** file to use a new tracking script from Segment.io.
Updated instructions for setting up Google Analytics tracking on
Segment.io. Added concluding paragraphs "Making Mr. Kadigan Happy" to
the "Analytics" chapter.

Minor clarification in the "Front-End Framework" chapter to explain that
the navigation bar won't show a dropdown menu until the next chapter,
when we add navigation links.

Minor clarification in the "Spreadsheet Connection" chapter to explain
that Google may block access if you attempt access from a new and
different computer (including Nitrous.io).

Added cat names in the "Credits and Comments" chapter.

Revised "Getting Help" chapter and added "Version Notes" chapter.

Minor clarifications, plus fixes for various typos and insignificant
errors.
