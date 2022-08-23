# The Parking Structure

We've created the default Rails starter application.

The `rails new` command has created a project directory for us.

It is a parking structure for our code. Unlike an ordinary parking structure, where you park anywhere you like, this garage has assigned parking. You have to park your code in the right place. This is Rails, where convention brings order to the development process.

As you develop a web application, you'll do all your work in the project directory. It is important to know your way around and understand the purpose of each folder and file.

If you've built simple websites with HTML and CSS, or built websites with unstructured platforms such as Perl or PHP, you'll be surprised at the complexity of the Rails project directory. Rails is a software machine with many moving parts; the project directory provides a structure to manage the complexity. The logic and order of the project directory structure is familiar to every Rails developer, and consistent for every Rails application, which makes it easy to collaborate, maintain an application, and create open source projects.

## Video Option

Watch the eleven minute video on YouTube:

- [Rails Project Directory](https://www.youtube.com/watch?v=klHTo3NgSUs)

## Project Directory

Use the Unix `ls` command to list the contents of the project directory. For a one-column list that shows each subdirectory (marked with a slash), we'll add the `-1p` option to the command. 

```console $ ls -1p ```

You'll see: 

```console Gemfile Gemfile.lock README.md Rakefile app/ bin/ config/ config.ru db/ lib/ log/ public/ tmp/ vendor/ ```

Now is a good time to open a file browser window and look at the contents of the project directory. On the Mac, there's a command you can use to open the graphical file browser from the console. If you're in the project directory, type `open .`. The period (or "dot") is a Unix symbol that means "the directory I'm in." 

```console $ open . ```

![Rails directory structure.\label{fig:rails_directory_structure}](images/figures/24_rails_directory_structure.png)

You'll learn more about each file and folder as you proceed through the tutorial.

## Get to Know the Folders and Files

To get you started, here are three tables. The first describes the files and folders that are important for every beginner. The second table describes the files and folders that you can ignore. The third table is a preview of things to come.

### Important Folders and Files

These folders and files are **important** to beginners. This is where you will spend your time in Rails.

| Gemfile | Lists all the gems used by the application. | | Gemfile.lock | Lists gem versions and dependencies. | | README.md | A page for documentation. | | app/ | Application folders and files. | | config/ | Configuration folders and files. | | db/ | Database folders and files. | | public/ | Files for web pages that do not contain Ruby code, such as error pages. |

### Not-So-Important Folders and Files

These folders and files are **not important** to beginners.

| Rakefile | Scripts for the Rake utility program. | | bin/ | Folder for binary (executable) programs. | | config.ru | Configuration file for Rack (a software library for web servers). | | lib/ | Folder for miscellaneous Ruby code. | | log/ | Folder for application server logfiles. | | tmp/ | Temporary files created when your application is running. | | vendor/ | Folder for Ruby software libraries that are not gems. |

### Folders for Testing

| spec/ | Folder for the popular RSpec testing framework. | | test/ | Folder for the default Rails testing framework. |

The **test/** folder is present in the default Rails starter app. You'll use the **test/** folder when you learn about test-driven development. Many Rails developers use a different gem for testing, named RSpec, and your RSpec tests will go in a **spec/** folder.

## The App Directory

Take time to drill down into the **app/** folder in the project directory. This is easiest using the file browser.

![Rails app folder.\label{fig:app_folder}](images/figures/24_app_folder.png)

You can also use your text editor to view the folder.

Or do it with Unix commands: 

```console $ cd app $ ls -1p assets/ channels/ controllers/ helpers/ jobs/ mailers/ models/ views/ ```

Whether you use the file browser, Unix commands, or your text editor, you are looking at the same file system.

Most of the work of developing a Rails application happens in the **app/** folder.

Earlier we described Rails as "a set of files organized with a specific structure." We said the structure is the same for every Rails application. The **app/** directory is a good example. The folders in the **app/** directory are the same in every Rails application. This makes it easy to collaborate with other Rails developers, providing consistency and predictability.

- **assets** - **channels** - **controllers** - **helpers** - **jobs** - **mailers** - **models** - **views**

You may recall our earlier description of Rails from the perspective of a software architect. In this folder, you'll see evidence of the [model–view–controller](http://en.wikipedia.org/wiki/Model%E2%80%93View%E2%80%93Controller) design pattern. Three folders named **models/**, **views/**, and **controllers/** enforce the software architect's "separation of concerns" and impart structure to our code. As you build the application, we'll explain the role of the MVC components in greater detail.

Five folders play supporting roles. The mailers folder is for code that sends email messages. The helpers folder is for Rails *view helpers*, snippets of reusable code that generate HTML. Later, when we learn more about *views*, we'll say view helpers are like "macros" that expand a short command into a longer string of HTML tags and content. Rails 3.1 added the **assets/** folder as a location for CSS and JavaScript files. The **jobs/** folder is for background jobs built with the Rails ActiveJob feature. Rails 5.0 added the **channels/** folder for the ActionCable feature which uses WebSockets for real-time communication between web server and browser.

### Folders of Future Importance

You won't encounter these when you are a beginner:

| policies/ | Folder for code that controls access to features | | services/ | Folder for code that reduces the complexity of models and controllers |

If you join a project to work on a large and complex Rails application, you may see folders such as these in the **app/** directory. As an application grows in complexity, an experienced software architect may suggest reducing the size of models and controllers by moving code to "POROs" (*plain old Ruby objects*). Code in any folder in the **app/** directory is shared throughout a Rails application without any additional configuration (in contrast, code you add to the **lib/** directory is only available with some extra work). Rails provides a basic model–view–controller framework but it is often necessary to extend it with code in a **services/** folder. Similarly, a **policies/** folder can be used to consolidate code that controls access to various features or pages of a web application.

Use the `cd ..` command ("change directory dot dot") to return to the project directory. 

```console $ cd .. $ pwd /Users/danielkehoe/workspace/learn-rails ```

As a Rails developer, you'll spend most of your time navigating the hierarchy of folders as you create and edit files. And because Rails provides a consistent structure, you'll quickly find your way on any unfamiliar project. 