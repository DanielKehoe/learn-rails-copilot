Mailing List
============

Even as other messaging avenues become increasingly popular, such as messaging apps
or Facebook messages, email remains the most practical way to stay
in touch with website visitors. Encouraging a visitor to provide an
email address means offering an invitation to a dialog and a
relationship beyond a single visit.

If you have a legitimate reason to stay in touch, and you've motivated
the visitor to leave an email address, you'll need a mailing list
service. You've seen how Rails can send an email message. From what
you've seen so far, you can imagine it would not take much code to loop
through a list of email addresses from a database, sending a message to
each. In the early days of the web, it was easy for any system
administrator to write a script for mass mailings. Since there is
negligible cost to sending bulk email, unscrupulous and ignorant
operators sent email to any address they could scrape, borrow, or steal.
The resulting flood of spam made checking one's inbox an icky experience
and destroyed much of the early culture of the Internet. Fortunately,
services such as Gmail arose to filter email. There is now a thick (but
leaky) layer of screening protocols that redirect spam to a junk folder.
One reason you won't use a Rails application to send bulk email is that
a web application server is not the most efficient tool for sending
email. More significantly, there's a good chance your email won't go
through or, if it does (and someone complains), you'll quickly see your
IP address blacklisted. That's why we use mailing list services to send
bulk email such as newsletters or promotional offers.

Considerable expertise is required to keep email from being filtered as
spam (see MailChimp's article [Email Delivery For IT Professionals](http://static.mailchimp.com/web/guides/email-delivery-for-it-professionals/package/email-delivery-for-it-professionals.pdf).
Email service providers increase reliability of delivery. These services
track deliveries and show how well your email is being delivered. You'll
also get features such as management of "unsubscribe" requests and
templates to design attractive messages.

There are at least a dozen well-established email service providers that
allow a Rails application to programmatically connect to the service
(via an API) to add or remove email addresses. For a list, see the
article [Send Email with
Rails](http://railsapps.github.io/rails-send-email.html). For this
tutorial application, we'll use
[MailChimp](http://mailchimp.com/pricing/) because there is no cost to
open an account and you can send up to 12,000 emails/month to list of
2000 or fewer subscribers for free.

Spam is unsolicited email. Don't ever send spam, whether for yourself, a
client, or an employer. If recipients complain, your IP address and
domain name will be blacklisted. So be very careful to only send to
subscribers who signed up, send what subscribers expect, and be sure to
offer value. If you get complaints, or the unsubscribe rate is high,
stop.

We'll assume we've discussed the rules with Foobar Kadigan and he is
eager to offer a newsletter to his visitors that will be genuinely
appreciated.

User Story
----------

Let's plan our work with a user story:


```cucumber
*Subscribe to Mailing List*
As a visitor to the website
I want to sign up for a mailing list
In order to receive news and announcements
```

To implement the user story, we'll add a mailing list feature.

Implementation
--------------

We'll use the Rails model-view-controller architecture. We'll need:

-   Visitors model
-   view for visitors#new
-   Visitors controller with `new` and `create` methods
-   routing for visitors#new and visitors#create

We'll add a Visitor model that has a data attribute for an email
address. We already have a Visitors controller that renders the home
page using the file in the **app/views/visitors/** folder. We'll replace
the contents of the view file with a nice photo, a marketing message,
and a form.

Our Visitors controller `new` and `create` methods will be very similar
to what we created for the Contacts controller. Instead of connecting to
SendGrid to send a message, we'll call a method to save the visitor's email
address to a MailChimp mailing list.

Gibbon Gem
----------

The [Gibbon gem](https://github.com/amro/gibbon) is a convenient wrapper
for the [MailChimp API](http://apidocs.mailchimp.com/). We could connect
to the MailChimp API using other gems that provide low-level plumbing
such as HTTP connections
([httparty](http://johnnunemaker.com/httparty/)) and data parsing
([multi_json](https://github.com/intridea/multi_json)), but other
developers have already done the work of wrapping the plumbing in a
higher-level abstraction that easily fits into a Rails application. Amro
Mousa's Gibbon gem is popular and actively maintained.

In your **Gemfile**, you've already added:


```ruby
gem 'gibbon'
```

and previously run `$ bundle install`.

Home Page
---------

Earlier we built a home page that provided a simple demonstration of the
Ruby language. We'll discard it and replace it with a page that you
could adapt for a typical small-business website.

We want a nice photo, space for a marketing message, and the "sign up"
form.

Replace the contents of the file **app/views/visitors/new.html.erb**:


```erb
<% content_for :title do %>Foobar Kadigan<% end %>
<% content_for :description do %>Website of Foobar Kadigan<% end %>
<section>
  <img src="http://lorempixel.com/1170/600/cats/1">
</section>
<section>
  <div class="column">
    <h3>Stay in touch.</h3>
  </div>
  <div class="column">
    <div class="form-centered">
      <%= form_with(model: @visitor) do |f| %>
        <%= f.email_field :email, placeholder: 'Your email address...', autofocus: true %>
        <br/>
        <br/>
        <%= f.submit 'Sign up for the newsletter', class: 'submit' %>
      <% end %>
    </div>
  </div>
</section>
```

We include `content_for` view helpers that pass a title and description
to the application layout.

We add a photo to the page with an `<img>` tag. We're taking
a shortcut and using a placeholder photo from the
[lorempixel.com](http://lorempixel.com/) service.

The `section` and `<div class="column">` tags apply our CSS grid
to create a row with two columns, one for our marketing
message, and one for the form.

Our marketing message is merely a placeholder. For a real website, you'd
likely craft a stronger call to action than merely "Stay in touch."

The form is very similar to the form on the Contact page, except we
initialize it with the `@visitor` instance variable and only need a
field for an email address. We use the `:placeholder` parameter to
create a hint in the empty input field.

A submit element will contain the text, "Sign up for the newsletter,"
and we apply a CSS class to style the element as a button.

### Photo Options

You're free to modify this page as you wish, as long as you keep the
form intact.

You might wish to modify the placeholder photo. If you don't like cats,
try
[http://lorempixel.com/1170/600/nightlife/1](http://lorempixel.com/1170/600/nightlife/1)
or any other categories from the
[lorempixel.com](http://lorempixel.com/) service. You can change the
size by modifying the dimensions from 1170 (pixel width) by 600 (pixel
height).

You can replace the placeholder photo with your own. Look for the
**app/assets/images** folder and add an image. Instead of the HTML
`<img>` tag, use the Rails `image_tag` view helper, like this:


```erb
<%= image_tag "myphoto.jpg" %>
```

We'll need a Visitor model to initialize the form.

Visitor Model
-------------

The Visitor model is almost identical to the Contact model we created
earlier, except there is just one data attribute for the email field.

We'll also add a `subscribe` method to add a visitor to a MailChimp
list. We'll call this method from the controller when we process the
submitted form.

Create a file **app/models/visitor.rb**:


```ruby
class Visitor
  include ActiveModel::Model
  attr_accessor :email
  validates_presence_of :email
  validates_format_of :email, with: /\A[-a-z0-9_+\.]+\@([-a-z0-9]+\.)+[a-z0-9]{2,4}\z/i

  def subscribe
    mailchimp = Gibbon::Request.new(api_key: Rails.application.secrets.mailchimp_api_key)
    list_id = Rails.application.secrets.mailchimp_list_id
    result = mailchimp.lists(list_id).members.create(
      body: {
        email_address: self.email,
        status: 'subscribed'
    })
    Rails.logger.info("Subscribed #{self.email} to MailChimp") if result
  end

end
```

When you copy this, be careful to keep the long regex expression
`with: /.../i` on one line (no line breaks).

Just as we did for the Contact model, we use
`include ActiveModel::Model` to mix in behavior from the ActiveModel
class. This is the best way to create a model that does not use a
database. In other applications, where models use a database, you will
create a model class that inherits from ActiveRecord instead.

We create the email attribute using the `attr_accessor` keyword. We set validation
requirements using `validates_presence_of` and `validates_format_of`
keywords.

To subscribe a visitor to a mailing list, you need to provide:

-   list_id - identify the MailChimp list
-   email_address - address of the visitor
-   status - subscribed, pending, or unsubscribed

We specify "subscribed" to immediately add the address without
asking the user for confirmation. We could specify "Pending"
if we wanted to add the address with double-opt-in so the
visitor receives a request to confirm the email address before they
are subscribed.

Our `subscribe` method does the work of connecting to the MailChimp
server to add the visitor to the mailing list. We instantiate the Gibbon
object which provides all the connectivity, providing the
`mailchimp_api_key` value, which we've set in the **config/secrets.yml**
file. We assign the Gibbon object to the `mailchimp` variable (we could
name it anything).

We set the `list_id` from a configuration variable in the
**config/secrets.yml** file.

The visitor's `email_address` is an attribute of the model we obtain
from `self`.

We must set the `status` property to `'subscribed'` to indicate the
visitor should receive mailings.

Finally, if the application successfully adds the new subscriber, we
write a message to the logger. If we get an error when trying to add the
subscriber, Gibbon will raise an exception.

Visitors Controller
-------------------

We already have a Visitors controller that contains a simple `new`
method. We'll change the `new` method, add a `create` method, and
provide a `secure_params` private method to secure the controller from
mass assignment exploits.

Replace the contents of the file
**app/controllers/visitors_controller.rb**:


```ruby
class VisitorsController < ApplicationController

  def new
    @visitor = Visitor.new
  end

  def create
    @visitor = Visitor.new(secure_params)
    if @visitor.valid?
      @visitor.subscribe
      flash[:notice] = "Signed up #{@visitor.email}."
      redirect_to root_path
    else
      render :new
    end
  end

  private

  def secure_params
    params.require(:visitor).permit(:email)
  end

end
```

Our `new` method now assigns the Visitor model to an instance variable
instead of the Owner model.

The `create` method is almost identical to the Contacts controller
`create` method. We instantiate the Visitor model with scrubbed
parameters from the submitted form.

If the validation check succeeds, we subscribe the visitor to the
MailChimp mailing list with the `@visitor.subscribe` method. All the
work of connecting to MailChimp happens in the Visitor model.

If the validation check fails, we redisplay the home page (the `new`
action).

Clean Up
--------

We no longer use the Owner model, so we can delete the file
**app/models/owner.rb**:


```console
$ rm app/models/owner.rb
```

There's no harm if it remains but it is good practice to remove code
that is no longer used.

Routing
-------

Our routing is now more complex. In addition to rendering the
visitors#
new view as the application root (the home page), we need to
handle the `create` action. We can use a "resourceful route" as we did
with the Contacts controller.

Open the file **config/routes.rb**. Replace the contents with this:


```ruby
Rails.application.routes.draw do
  resources :contacts, only: [:new, :create]
  resources :visitors, only: [:new, :create]
  root to: 'visitors#new'
end
```

The root path remains `visitors#new`. Order is significant in the
**config/routes.rb** file. As the final designated route, the root path
will only be active if nothing above it matches the route.

We've added `resources :visitors, only: [:new, :create]`.

We only want two routes so we've added the restriction
`only: [:new, :create]`.

The `new` route has these properties:

-   `new_visitor_path` - route helper
-   `visitors` - name of the controller (VisitorsController)
-   `new` - controller action
-   [http://localhost:3000/visitors/new](http://localhost:3000/visitors/new) - URL generated by the route helper
-   `GET` - HTTP method to display a page

The `create` route has these properties:

-   `visitors_path` - route helper
-   `visitors` - name of the controller (VisitorsController)
-   `create` - controller action
-   [http://localhost:3000/visitors](http://localhost:3000/visitors) - URL generated by the route helper
-   `POST` - HTTP method to submit form data

You can run the `rails routes` command to see these in the console:


```console
$ rails routes
     Prefix Verb URI Pattern             Controller#Action
   contacts POST /contacts(.:format)     contacts#create
new_contact GET  /contacts/new(.:format) contacts#new
   visitors POST /visitors(.:format)     visitors#create
new_visitor GET  /visitors/new(.:format) visitors#new
       root GET  /                       visitors#new
       page GET  /pages/*id              high_voltage/pages#show
```

The output of the `rails routes` command shows we've created the routes
we need.

Test the Application
--------------------

If you need to start the server:


```console
$ rails server
```

Open a web browser window and navigate to
[http://localhost:3000/](http://localhost:3000).

You'll see our new home page with the placeholder photo and the "sign
up" form.

Enter your email address and click the "sign up" button. You should see
the page redisplay with an acknowledgment message. Try entering an
invalid email address such as "me@foo@", or click the submit button
without entering an email address, and you should see an error message.

You'll have to [log in to MailChimp](https://admin.mailchimp.com/) and
check your list of subscribers to see if the new email address was added
successfully.

With MailChimp, you can send a welcome message automatically when the
visitor signs up for the mailing list. Use the welcome message to inform
the visitor that they've successfully subscribed to the mailing list and
will receive the next newsletter email.

It's a bit difficult to find the MailChimp option to create a welcome
message. Strangely, MailChimp considers a welcome message a "form."
Here's how to find it. On the MailChimp "Lists" page, click the "down
arrow" for a list and click "Signup forms." Then click "General forms."
On the "Create Forms" page, there is a drop-down list of "Forms &
Response Emails." The gray box shows "Signup form." Click the down
arrow. Select the menu item named "Final 'Welcome' Email" and you'll be
able to create a welcome message.

Git
---

Let's commit our changes to the Git repository and push to GitHub:


```console
$ git add -A
$ git commit -m "mailing list"
$ git push
```

Our tutorial application is feature complete.

Let's deploy it so we can see it running as a real website.
