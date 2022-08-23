# Create the Application

In this chapter, we'll begin building the tutorial application. But first, let's consider the options you have for starter applications.

## Starter Applications

Rails provides a *framework*; that is, a software library that provides utilities, conventions, and organizing principles to allow us to build complex web applications. Without a framework, we'd have to code everything from scratch. Rails gives us the basics we need for many websites.

Still, the framework doesn't give us all the features we need for many common types of websites. For example, we might want users to register for an account and log in to access the website ("user management and authentication"). We might want to restrict portions of our website to just administrators ("authorization"). We also might want to add gems that enhance Rails to aid development (gems for testing, for example) or improve the look and feel of our application (the Bootstrap or Foundation front-end frameworks). Developers often mix and match components to make a customized Rails stack.

Developers often use a *starter application* instead of assembling an application from scratch. You might call this a "template" but we use that term to refer to the *view files* that combine HTML with Ruby code to generate web pages. Most experienced developers have one or more starter applications that save time when beginning a new project. The [RailsApps project](http://railsapps.github.io/) was launched to provide open source starter applications so developers could collaborate on their starter applications and avoid duplicated effort. After you gain some skill with this tutorial, you might use the RailsApps starter apps to instantly generate a Rails application with features like authentication, authorization, and an attractive design. At the end of this book, you'll learn about [Rails Composer](http://www.railscomposer.com/), a tool for building starter applications.

For now, we'll begin with the Rails default starter application.

## Workspace Folder and RVM Gemset

Are you in the folder named **workspace/** you created earlier?

```console $ pwd /Users/danielkehoe/workspace/ ```

If you're not in your workspace folder, enter a Unix command to move to the folder:

```console $ cd ~/workspace ```

We already created a project-specific gemset using RVM. Make sure it's ready to use:

```console $ rvm use ruby-2.4.1@learn-rails $ rvm gemset list gemsets for ruby-2.4.1... (default) global => learn-rails ```

You should see an arrow pointing to the `learn-rails` gemset. If not, go back to the previous "Get Started" chapter.

## Use "Rails New" to Build the Application

Let's go! We have selected a gemset, we have Rails installed, and we're in our **workspace/** folder. Let's build a Rails application!

To create the Rails default starter application, type: 

```console $ rails new learn-rails ```

This will create a new Rails application named "learn-rails."

It takes a few minutes when the build script runs `bundle install`. Don't worry; just give it enough time to finish (but no more than five minutes even if your Internet connection is very slow).

In the future, you can give your application a different name. For this tutorial, it is VERY IMPORTANT that you use the name "learn-rails." You'll be copying code that assumes the name is "learn-rails;" it will save you trouble to use this name.

The `rails new` command will create ten folders and 93 files.

It will install 62 gems into your gemset.

After you create the application, switch to its folder to continue work directly in the application: 

```console $ cd learn-rails ```

This is your project directory. It is also called the application root directory. You'll spend all your time inside this folder.

\begin{aside} \label{aside:exec_binstub} \heading{Spring}

After creating a new Rails application, you may see a message to run a command:

``` $ bundle exec spring binstub --all ```

The command sets up Spring. Spring is a Rails application preloader. It speeds up development by keeping your application running in the background so you don't need to stop and restart it when you make changes.

After you change into the project directory, you can run the command.

\end{aside}

Type the `ls` command to show the folders and files in a directory. Soon we'll learn more about each of these folders and files.

```console $ ls Gemfile Rakefile config lib test Gemfile.lock app config.ru log tmp README.md bin db public vendor ```

## Make a Sticky Gemset

RVM gives us a convenient technique to make sure we are always using the correct gemset when we enter the project directory. It will create hidden files to designate the correct Ruby version and project-specific gemset. Enter this command to create the hidden files: 

```console $ rvm use ruby-2.4.1@learn-rails --ruby-version ``` The `--ruby-version` argument creates two files, **.ruby-version** and **.ruby-gemset**, that set RVM every time we `cd` to the project directory. Without these two hidden files, you'd need to remember to enter `rvm use ruby-2.4.1@learn-rails` every time you start work on your project after closing the console.

If you see "ERROR: Gemset 'learn-rails' does not exist", perhaps you overlooked an earlier step in the *Project-Specific Gemset* section (in the previous chapter) where we created the learn-rails gemset.

After creating the two hidden files, check if they are there: 

```console $ ls -1pa ./ ../ .gitignore .ruby-gemset .ruby-version Gemfile Gemfile.lock README.md Rakefile app/ bin/ config/ config.ru db/ lib/ log/ public/ test/ tmp/ vendor/ ```

The "a" flag in the Unix `ls -1pa` command displays hidden files. Each hidden file is listed with a dot (period or full stop) at the beginning of the filename. You'll notice `.ruby-gemset` and `.ruby-version`.

You'll also see two "special files" which are not files at all:

- `./` - an alias that represents the current directory - `../` - an alias that represents the parent directory

\begin{aside} \label{aside:cloud9_hidden_files} \heading{Hidden Files in Cloud9}

If you're using Cloud9, you must change preferences to see hidden files. In the window that contains the file list, there is a gear icon (dark in color and difficult to see). Clicking the gear option will give you options:

* Show Root File System * Show Home in Favorites * Show Hidden Files

You must select all three options to see the hidden files.

![Cloud9 Hidden Files](images/figures/23_cloud9_hidden_files.jpg)

\end{aside}

That's a brief diversion into Unix; let's try running our new Rails application.

## Test the Application

You've created a simple default web application. It's ready to run.

### Launching the Web Server

You can launch the application by entering the command: 

```console $ rails server ```

Alternatively, to save typing, you can abbreviate the `rails server` command: 

```console $ rails s ```

If you are using the Cloud9 hosted service, you'll need to enter `bin/rails server -p $PORT -b $IP`.

You'll see: 

```console => Booting Puma => Rails 5.1.2 application starting in development on http://localhost:3000 => Run `rails server -h` for more startup options => Ctrl-C to shutdown server Puma starting in single mode... * Version 3.4.0 (ruby 2.4.1-p0), codename: Owl Bowl Brawl * Min threads: 5, max threads: 5 * Environment: development * Listening on tcp://localhost:3000 Use Ctrl-C to stop ```

The `rails server` command launches the [Puma web server](http://puma.io/) that is provided with Rails.

### Errors for Linux Users

If you enter the command `rails server` and get an error message: 

```console ... Could not find a JavaScript runtime ... ```

You need to install Node.js. For help, see [Install Ruby on Rails - Ubuntu](http://railsapps.github.io/installrubyonrails-ubuntu.html).

### Viewing in the Web Browser

To see your application in action, open a web browser window and navigate to [http://localhost:3000/](http://localhost:3000). You'll see the Rails default information page.

\begin{aside} \label{aside:viewing_hosted_} \heading{Viewing on a Hosted Platform}

It is easy to see your web application in action on your local computer. If you are using a hosted service such as Cloud9, it is a little more complicated.

If you are using **Cloud9**, click the "Preview" link in the IDE menu (at the top of the page). There is a "Run" link, too, but it doesn't work if you have created your Rails application in a folder within the **workspace/** folder. You can also open a browser tab or window and enter the URL for the application, as hosted by Cloud9. When you launch the Rails server, Cloud9 displays a helpful message showing the URL where you can view your application.

\end{aside}

### Watch Log Messages

Notice that messages scroll in the console window when your browser requests the Rails default web page.

Open the file **log/development.log** and you'll see the same messages. When a browser sends requests to the Puma web server, diagnostic messages are written to the console and to the **log/development.log** file. These diagnostic messages are an important tool for troubleshooting when you are developing.

### Multiple Terminal Windows

You can keep more than one terminal window open. For convenience, you may want to keep a terminal window open for running the web server and watching diagnostic messages. In the Terminal or iTerm2 applications, Command-t opens additional console sessions in new "tabs."

Developers typically open more than one terminal window when they work on a Rails application. They'll start the server with the `rails server` command in one window (or tab) and watch the log messages. In another window (or tab), they'll enter commands as they build the application. They might create folders with a Unix command, run generators, or try out code with the `rails console` command (you'll learn about the `rails console` command in the "Troubleshoot" chapter).

To some people, the text editor and the terminal window look very similar. When you work on a file in a text editor, you make changes to one file, in one place. The terminal window is very different. Your computer can run multiple programs at once. You can open multiple terminal windows. In each terminal window, you can use the command line to launch a different program. Each program you start in a terminal window is a separate *process* and multiple processes can run simultaneously. You can end a process by pressing Control-c (in most cases), Control-d (in some cases), or closing the terminal window (almost always). From this perspective, a terminal window is a tool you use to launch processes and your computer is a machine that runs processes.

### Stop the Web Server

You can stop the server with Control-c to return to the command prompt. When we say Control-c, we mean hold down the Control key as you press the letter "c".

Most of the time you'll keep the web server running as you add or edit files in your project. Changes will automatically appear when you refresh the browser or request a new page. There is a tricky exception, however. If you make changes to the Gemfile, or changes to configuration files, the web server must be shut down and relaunched for changes to be activated.

As a rule of thumb, files that produce web pages can be changed without a restart. This includes any file in the **app/** folder which creates web pages, as well as the **config/routes.rb** file. Changes to files that create the environment for the web application, such as gems or configuration files, and are loaded at web server launch, won't be seen until the web server is restarted.

## Get Organized for Efficiency

Before we learn about the Rails directory structure, take a minute to organize your screen real estate. During development, you'll jump between the console in a terminal application, your text editor, and a web browser window. As a Rails developer, you'll do this constantly, so think about how you can do this efficiently. Multiple screens make it easy, but even on a laptop you can get organized for efficiency.

![Getting organized for efficiency.\label{fig:organized_for_efficiency}](images/figures/learn-rails-getting-organized.png)

Here's some ideas. Open a window in the terminal application, place it on the left side of your screen, and stretch it to the maximum vertical height of your screen. Open multiple tabs in your terminal application. Keep one tabbed window open for entering shell commands (like `cd` or `ls`) and another terminal window open for running the `rails server` command and viewing the log output.

Place your text editor window next to the terminal window and stretch it to full vertical height. If you are using Atom or Sublime Text, you can open two editor panels side-by-side. Some developers find it helpful to leave the file browser panel open to navigate the project directory; others hide the file browser panel to save space.

If you have enough screen space, leave your web browser open and place it next to your text editor. If your screen space is limited, you may have to overlap the web browser with the text editor, but position your web browser window so you can bring it to the front with a single click. You'll need multiple tabs open in your web browser. Unless you like constant distraction, close Gmail, Facebook, Twitter, and Hacker News. Open tabs for [http://localhost:3000/](http://localhost:3000/), this tutorial, and additional references or documentation.

On the Mac, there are window management utilities that reposition windows with just a click or keyboard command; I use [Moom](http://manytricks.com/moom/) but you can find others if you search for "mac window management utilities."

This is just a guide; I'm sure you can improve upon these suggestions. 