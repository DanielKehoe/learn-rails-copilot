# Get Started

Before you can start building, you'll need to install Ruby (the language) and Rails (the gem). I'll provide links to installation instructions that are up to date. Even if you've already installed Rails, please review the instructions to make sure your development environment is set up correctly. Other books and tutorials often skip important details.

## Text Editor and Terminal Applications

I've explained how to use a text editor and terminal application in the book *Learn Ruby on Rails: First Steps*. If you haven't used the Unix command line before, refer to the book for an introduction.

I recommend the [Atom](https://atom.io/) text editor but you may use [Sublime Text](http://www.sublimetext.com/) or any others that provide syntax highlighting. Refer to the book *Learn Ruby on Rails: First Steps* for important instructions about setting up the text editor so you can open a file from the command line.

## Copying and Pasting Code

In the next chapter you'll begin building a Rails application.

You need to get the code from this tutorial into your computer. You could just read and imagine, but really, building a working application is the only way to learn.

The most obvious way is to copy and paste from this tutorial into your text editor, assuming you are reading this on your computer (not a tablet or printed pages). It's a bit tedious and error-prone but you'll have a good opportunity to examine the code closely.

Some students like to type in the code, character by character. If you have patience, it's a worthwhile approach because you'll become more familiar with the code than by copying and pasting.

Don't feel shy about copying code; it's how you will learn. Working programmers spend a lot of time copying code from others. At first, you will copy a lot of code. As you gain proficiency, you will copy code and adapt it, more extensively as you gain confidence and skill. Only when you've been working full-time as a coder for months or years will you find yourself writing code from scratch; even then, when you encounter new problems, you will still look for code examples to copy and adapt.

\begin{aside} \label{aside:pdf_and_kindle_warning} \heading{Warning About the PDF and Kindle Versions}

This book is available in several formats, including online (HTML), PDF, ePub (Apple iBooks), and mobi (Kindle) versions.

Use the online edition of the book if you can. With the online edition, you'll be able to copy and paste the code without any problem. The ePub version (using Apple iBooks) also preserves line breaks and indentation when copying code.

Copying without line breaks will cause code errors. You'll lose line breaks when copying code with the following versions:

- PDF version on macOS using the Preview application - mobi (Kindle)

If you use [Adobe Acrobat](http://get.adobe.com/reader/) you'll be able to copy the line breaks (though indenting is lost). You can also open a PDF file in Chrome or Safari web browsers and copy code with line breaks. With the mobi (Kindle) version, you'll have to carefully reformat the code after pasting into your text editor.

Indentation makes code more readable, so try to preserve the indentation you see in the code samples. In YAML files (with the file extension **.yml**), indentation is required (your application will break without it).

\end{aside}

## Your Computer

You can develop web applications with Rails on computers running Mac OS X, Linux, or Microsoft Windows operating systems. Most Rails developers use macOS or Linux because the underlying Unix operating system has long been the basis for open source programming.

Later in this chapter, I'll give links to installation instructions for macOS and Linux.

For Windows users, I have to say, installing Rails on Windows is frustrating and painful. Readers and workshop students often tell me that they've given up on learning Rails because installation of Ruby on Windows is difficult and introduces bugs or creates configuration issues. Even when you succeed in getting Rails to run on Windows, you will encounter gems you cannot install. For these reasons, I urge you to use Cloud9, a browser-based development environment, on your Windows laptop.

### Hosted Computing

If you are using Windows, or have difficulty installing Ruby on your computer, try using Cloud9.

[Cloud9](https://c9.io/) provides a hosted development environment. That means you set up an account and then access a remote computer from your web browser. The Cloud9 service is free for ordinary use. There is no credit card required to set up an account. You'll only be charged if you add extra computer memory or disk space (which you don't need for ordinary Rails development).

The Cloud9 service gives you everything you need for Rails development, including a Unix shell with Ruby pre-installed, plus a browser-based file manager and text editor. Any device that runs a web browser will give you access to Cloud9, including a tablet or smartphone, though you need a broadband connection, a sizable screen, and a keyboard to be productive.

## Try the Terminal

Look for the Terminal application in the following places:

- MacOS: *Applications - Utilities - Terminal* - Linux: *Applications - Accessories - Terminal* - Windows: *Taskbar Start Button - Command Prompt*

On the Mac, search for the macOS Terminal application by pressing the Command-Spacebar combination (which Apple calls "Spotlight Search") and searching for "Terminal." The magnifying glass in the upper right corner of your screen will also launch "Spotlight Search." Or look in the **Applications/Utilities/** folder for the Terminal application. You'll need to click the name of the application to launch the Terminal.

For Linux or Windows, [The Command Line Crash Course](http://cli.learncodethehardway.org/book/) explains [how to launch a terminal application](http://cli.learncodethehardway.org/book/ex1.html).

Launch your terminal application now.

Try out the terminal application by entering a shell command.

```console $ whoami ```

Don't type the `$` character. The `$` character is a cue that you should enter a shell command. This is a longtime convention that indicates you should enter a command in the terminal application or console.

The Unix shell command `whoami` returns your username.

Don't type the `$` prompt.

You might see: 

```console command not found: $ ```

which indicates you typed the `$` character by mistake.

If you are new to programming, using a text editor and the shell will seem primitive compared to the complexity and sophistication of Microsoft Word or Photoshop. Software developers edit files with simple text editors and run programs in the shell. That's all we do. We have to remember the commands we need (or consult a cheatsheet) because there are no graphical menus or toolbars. Yet with nothing more than a text editor and the command line interface, programmers have created everything that you use on your computer.

## Installing Ruby

Your first challenge in learning Rails is installing Ruby on your computer.

Frankly, this can be the most difficult step in learning Rails because no tutorial can sort out the specific configuration of your computer. Get over this hump and everything else becomes easy.

The focus of this book is learning Rails, not installing Ruby, so to keep the book short and readable, I'm going to give you links to articles that will help you install Ruby.

You'll spend at least an hour installing Ruby and Rails, so be sure to allow enough time for the task.

### MacOS

See this article for macOS installation instructions:

[**Install Ruby on Rails - MacOS**](http://railsapps.github.io/installrubyonrails-mac.html)

### Ubuntu Linux

See this article for Ubuntu installation instructions:

[**Install Ruby on Rails - Ubuntu**](http://railsapps.github.io/installrubyonrails-ubuntu.html)

### Hosted Computing

[Cloud9](https://c9.io/) is a browser-based development environment. Cloud9 is free for small projects. If you have a fast broadband connection to the Internet, this is your best choice for developing Rails on Windows. And it is a good option if you have any trouble installing Ruby on Mac or Linux because the Cloud9 hosted environment provides everything you need, including a Unix shell with Ruby and RVM pre-installed, plus a browser-based file manager and text editor. Using a hosted development environment is unconventional but leading developers do so and it may be the wave of the future.

See this article for Cloud9 installation instructions:

[**Install Ruby on Rails - Cloud9**](http://railsapps.github.io/rubyonrails-cloud9.html)

The article shows how to get started with Cloud9.

If you use Cloud9, be sure to pick the "Blank" template for your workspace, not the "Ruby" or "Ruby on Rails" templates that provide a prebuilt Rails application. We're building from scratch in this tutorial.

### Windows

Here are your choices for Windows:

- Use the [Cloud9](http://railsapps.github.io/rubyonrails-cloud9.html) hosted development environment - Install the [Railsbridge Virtual Machine](https://github.com/railsbridge/railsbridge-virtual-machine) - Use [RubyInstaller for Windows](http://rubyinstaller.org/)

Cloud9 is ideal if you have a fast Internet connection. If not, download the Railsbridge Virtual Machine to create a virtual Linux computer using [Vagrant](http://www.vagrantup.com/). Other tutorials may suggest using [RailsInstaller](http://railsinstaller.org/), but it will not provide an up-to-date version of Ruby or Rails. Also, RVM does not run on Windows.

## Your Workspace

Take a moment to think about where on your computer you'll do your work and store your files. You may have a **documents/** folder. You could make a similar folder named **projects/** or **code/** or **workspace/** for your programming projects. Use the Unix `mkdir` command to create a folder or create it with your file browser.

If you haven't done so already, make a folder to contain your programming projects. You don't need to do this if you already created a **workspace/** folder in the Unix chapter in the book *Learn Ruby on Rails: First Steps*.

```console $ cd ~ $ pwd /Users/danielkehoe $ mkdir workspace $ cd workspace ``` In this tutorial, the terms "folders" and "directories" mean the same thing.

Use the Unix `cd` command to change directories.

When you enter the Unix command `cd \textasciitilde`, you'll move to your home (or "user") directory. The squiggly `\textasciitilde` "tilde" character is a Unix shortcut that indicates your home folder.

The Unix `pwd` command shows the "present working directory," where you are.

The Unix `mkdir` command creates an empty folder and we move into it with the Unix `cd` command.

### Video Option

Watch the four minute video if you have subscribed:

- [UNIX Commands Basics](https://tutorials.railsapps.org/videos/2)

## Understanding Version Numbers

Rails follows a convention named *semantic versioning*:

- The first number denotes a *major version* (Rails 4) - The second number denotes a *minor release* (Rails 4.2) - The third number denotes a *patch level* (Rails 4.2.1)

A major release includes new features, including changes which break backward compatibility. For example, switching from Rails 3.2 to Rails 4.0 required a significant rewrite of every Rails application.

A minor release introduces new features but doesn't break anything. For example, Rails 3.2 added the asset pipeline, and Rails 4.2 added the Active Job feature for background processing.

A patch release fixes bugs but doesn't introduce significant features. Usually this means you can change the version number in the Gemfile and run `bundle update` without making any other changes to your application.

## Ruby and Rails Version Check

Check that appropriate versions of Ruby and Rails are installed in your development environment. You'll need:

- The Ruby language (version 2.3 or newer) - The Rails gem (version 5.1 or newer)

Open your terminal application and enter: 

```console $ ruby -v ```

You might see: 

```console ruby 2.4.1p0 (...) ```

You've got Ruby version 2.4.1, patch level "p0" (Ruby versions add an extra patch level to semantic versioning). If you've got a newer version of Ruby, no problem; minor updates to Ruby don't affect Rails.

Try:

```console $ rails -v ```

You might see:

```console Rails 5.1.2 ```

If you see:

```console Rails is not currently installed on this system. ``` You are not using an RVM gemset where the Rails gem is installed. Go to the [Installing Rails](http://railsapps.github.io/installing-rails.html) instructions for your computer if you have not set up Rails. The next section explains more about RVM gemsets which may be all you need to find Rails.

If you have Rails 4.2 or older versions, you must update to Rails 5.1. See the [Installing Rails](http://railsapps.github.io/installing-rails.html) instructions for your computer.

Versions such as `5.0.0.beta3` or `5.0.0.rc1` are beta versions or "release candidates." You can use a release candidate in the weeks before a final release becomes available.

If you've got Rails 5.1.3 or newer, that's fine. It means minor bugs have been fixed since this was written, but the book is still current. You can check for the [current version of Rails](http://rubygems.org/gems/rails) here.

\begin{aside} \label{aside:rails_5_warning} \heading{Rails 5.1}

This edition of the book was prepared using Rails 5.1.2. The newest version of the book is listed on the README page of the [learn-rails](https://github.com/RailsApps/learn-rails) GitHub repository.

\end{aside}

## RVM

I promised that this book would introduce you to the practices of professional Rails developers. One of the most important utilities you'll need in setting up a real-world Rails development environment is RVM, the [Ruby Version Manager](https://rvm.io/).

RVM lets you switch between different versions of Ruby. Right now, that might not seem important, but as soon as a new version of Ruby is released, you'll need to upgrade, and it is best to be ready by installing the current version of Ruby with RVM, so you can easily add a new version of Ruby later, and still switch back to older versions as needed.

RVM also helps you manage your collections of gems, by letting you create multiple *gemsets*. Each gemset is the collection of gems you need for a specific project. Rails changes frequently; with RVM, you can install a specific version of Rails in a project gemset, along with all the gems you need for the project. When a new version of Rails is released, you can create a new gemset with the new Rails version when you start a new project. Your old project will still have the version of Rails it needs in its own gemset.

If you've followed the instructions in the article [Installing Rails](http://railsapps.github.io/installing-rails.html) and installed RVM, you'll be ready to handle multiple versions of Ruby, and multiple versions of Rails. That's as it should be. Most professional Rails developers have more than one version of Ruby or Rails, and RVM makes it easy to switch.

RVM will show you a list of available Ruby versions: 

```console $ rvm list ```

You can see a list of available gemsets associated with the current Ruby version: 

```console $ rvm gemset list ```

You will see an arrow that shows which gemset is active.

You will see a `global` gemset as well as any others you have created, such as a gemset for `Rails5.0`.

Here's how to switch between gemsets: 

```console $ rvm gemset use global ```

And switch back to another: 

```console $ rvm gemset use default ```

After you've worked on a few Rails applications, you'll see several project-specific gemsets if you are using RVM in the way most developers do.

RVM is not the only utility you can use to manage multiple Ruby versions. Some developers like [Chruby](https://github.com/postmodern/chruby) or [rbenv](https://github.com/sstephenson/rbenv). Don't be worried if you hear debates about RVM versus Chruby or rbenv; developers love to compare the merits of their tools. RVM is popular, well-supported, and an excellent utility to help a developer install Ruby and manage gemsets; that's why we use it.

## Project-Specific Gemset

For our learn-rails application, we'll create a project-specific gemset using RVM. We'll give the gemset the same name as our application.

By creating a gemset for our tutorial application, we'll isolate the current version of Rails and the gems we need for this project. Whether you use RVM or another Ruby version manager, this will introduce you to the idea of "sandboxing" (isolating) your development environment so you can avoid conflicts among projects.

After we create the project-specific gemset, we'll install the Rails gem into the gemset. Enter these commands: 

```console $ rvm use ruby-2.4.1@learn-rails --create $ gem install rails ```

This will install the newest version of Rails 5.0. It takes a few minutes to automatically install all the gems that are needed for Rails.

It's absolutely necessary to create a gemset and install Rails so we can move on to creating the application in the next chapter. If you have trouble at this point, refer to the article [Installing Rails](http://railsapps.github.io/installing-rails.html) or the [RVM website](https://rvm.io/). Linux users may need to check instructions for [Integrating RVM](https://rvm.io/integration/gnome-terminal).

Let's make sure Rails is ready to run. Open a terminal and type: 

```console $ rails -v ```

You should see the message "Rails 5.1.2" (or something similar).

Now let's explore the `rails new` command and get started building the tutorial application. 