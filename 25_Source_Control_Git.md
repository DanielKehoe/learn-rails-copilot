# Time Travel with Git

Now that we've looked at our Rails project directory from the viewpoint of a programmer and software architect, let's consider the viewpoint of the time traveler.

This chapter will introduce you to software *source control*, also called *version control* or *revision control*. The terms all have the same meaning. At first sight, the concept seems rather dull, like sorting your socks. But it makes professional software development possible and, at the core, it is essentially a form of time travel.

To understand time travel, we need to understand *state*. It's a term you'll encounter often in software development. We know about states of matter. Water can be ice, liquid, or steam. Imagine a machine with a button that, each time it is pressed, changes water from one state to another. We call this a *state machine*. Almost every software program is a state machine. When a program receives an input, it transitions from one state to another. Like flipping a light switch, there's no in-between. Light or dark. Ice, liquid, or steam. Or, in a web application: logged in, logged out.

When we write software code, there's a lot of in-between. We look things up, we think, we type errors and we make corrections. As humans, we spend a lot of time in a flow of undetermined state. We can save our work at any time, but we may be saving typos or unfinished code that doesn't work. Every so often, we get to a point where a task is finished; we've fixed all our errors and our code runs. We want to preserve the state of our work. That's when we need a version control system.

A version control system does more than a software application's "Save" command. Like a "Save" command, it preserves the current state of our files. It also allows us to add a short note that describes the work we've done. More importantly, it archives a snapshot of the current state in a *repository* where it can be retrieved if needed.

Here's where the time travel comes in. We can go back and recover the state of our work at any point where we committed a snapshot to the repository. In software development, travel to the past is essential because we often make mistakes or false starts and have to return to a point where we know things were working correctly.

What about time travel to the future? Often we need to try out code we may decide to discard, without disturbing work we've done earlier. Version control systems allow us to explore alternative futures by creating a *branch* for our work. If we like what we've done in our branch, we can merge it into the main trunk of our software project.

Unlike time travel in the movies, we can't travel back to any arbitrary point in the flow of time. We can only travel to past or future states we've marked as significant by checking our work into the repository.

## Git

The dominant version control system among Rails developers is [Git](http://en.wikipedia.org/wiki/Git_(software)), created by the developer of the Linux operating system.

Unlike earlier version control systems, Git is ideal for wide-scale distributed open source software development. Combined with [GitHub](https://github.com/), the "social coding" website, Git makes it easy to share and merge code. When you work with others on a project, your Git *commit messages* (the notes that accompany your snapshot) offer a narrative about the progress of the project. Well-written commit messages describe your work to co-workers or open source collaborators.

GitHub's support for *forking* (making your own copy of a repository) makes it possible to take someone else's project and modify it without impacting the original. That means you can customize an open source project for your own needs. You can also fix bugs or add a feature to an open source project and submit a *pull request* for the project maintainer to add your work to the original. Fixing bugs (large or small) and adding features to open source projects are how you build your reputation in the Rails community. Your GitHub account, which shows all your commits, both to public projects and your own projects, is more important than your resumé when a potential employer considers hiring you because it shows the real work you have done.

Collaboration is easy when you use a *branch* in Git. If you and a coworker are working on the same codebase, you can each make a branch before adding to the code or making changes. Git supports several kinds of *merges*, so you can integrate your branch with the trunk when your task is complete. If your changes collide with your coworker's changes, Git identifies the conflict so you can resolve the collision before completing the merge.

All the power of Git comes at a price. Git is difficult for a beginner to learn, largely because many of its procedures have no real-world analog. Have you noticed how time travel movies require mental gymnastics, especially when you try to make sense of alternative futures and intersecting timelines? Git is a lot like that, mostly because we use it to do things we don't ordinarily do in the real world.

In this tutorial, you won't encounter Git's advanced procedures, like resolving merges or reverting to earlier versions. We'll stick to the basics of archiving our work (and in one case, discarding work that we've done for practice). You can build the tutorial project without using Git. But I urge you to use Git and a GitHub account for this project, for two reasons. First, with your tutorial application on GitHub, you'll show potential employers or collaborators that you've successfully built a useful, functioning Rails application. More importantly, you must get to know Git if you plan to do any serious coding, either as a professional or a hobbyist.

Before I show you Git commands, I want to mention that some people use graphical client applications to manage Git. MacOS has [GitHub for Mac](http://mac.github.com/), [Git Tower](http://www.git-tower.com/), and other [Mac Git clients](http://list.ly/list/FO-mac-git-clients). Graphical applications for Git are useful for colleagues who don't use a Terminal application, such as graphic designers or writers. There's no need for you to install these applications. Every developer I've met uses Git from the command line. It will take effort to master Git; the commands are not intuitive. But it is absolutely necessary to become familiar with Git basics.

Before you do any work on the tutorial application, I'll show you the basics of setting up and using Git.

## Is Git Installed?

As a first step, make sure Git is installed on your computer: 

```console 
$ which git /usr/local/bin/git $ git version git version ... 
```

If Git is not found, install Git. See the article [Rails with Git and GitHub](http://railsapps.github.io/rails-git.html) for installation instructions.

## Is Git Configured?

Make sure Git knows who you are. Every time you update your Git repository with the `git commit` command, Git will identify you as the author of the changes. 

```console 
$ git config --get user.name $ git config --get user.email 
```

You should see your name and email address. If not, configure Git: 

```console 
$ git config --global user.name "Real Name" $ git config --global user.email "me@example.com" 
```

Use your real name so people will associate you with your work when they meet you in real life. There's no reason to use a clever name unless you have something to hide. And use your full name, not just your first name.

Use the same email address for Git, your GitHub account, and Heroku to avoid headaches.

## Create a Repository

Now we'll add a Git repository to our project. It's a basic step you'll repeat every time you create a new Rails project.

Extending the time traveler analogy, initializing a Git repository is equivalent to setting up the time machine.

Be sure you are in your project directory, not your user home directory or somewhere else. Use the `pwd` command to check:

```console 
$ pwd /Users/danielkehoe/workspace/learn-rails 
```

The `git init` command sets up a Git repository (a "repo") in the project directory. We add the Unix symbol that indicates Git should be initialized in the current directory (git init dot): 

```console 
 git init . Initialized empty Git repository in ... 
 ```

It creates a hidden folder named **.git/** in the project directory. You can peek at the contents: 

```console 
$ ls -1p .git HEAD config description hooks/ info/ objects/ refs/ 
```

All Git commands operate on the hidden files. The hidden files record the changing state of your project files each time you run the `git commit` command. There is no reason to ever edit files inside the hidden **.git/** folder (doing so could break your time machine).

## GitIgnore

The hidden **.git/** folder contains the Git repository with all the snapshots of your changing project. The snapshots are highly compressed, only containing records of changes, so the repository takes up very little file space relative to the project as a whole.

Not every file should be included in a Git snapshot. Here are some types of files that should be ignored:

- log files created by the web server - database files - configuration files that include passwords or API keys

Git gives us an easy way to ignore files. A hidden file in the project directory named **.gitignore** can specify a list of files that are never seen by Git. The `rails new` command creates a **.gitignore** file with defaults that include log files and database files. Later, when we add configuration files that include secrets, we'll update the **.gitignore** file.

Take a look at the contents of the **.gitignore** file. We use the Unix `cat` command to display the contents of the file: 

```console 
$ cat .gitignore 
# See https://help.github.com/articles/ignoring-files for more about ignoring files. 
# 
# If you find yourself ignoring temporary files generated by your text editor 
# or operating system, you probably want to add a global ignore instead: 
# git config --global core.excludesfile '~/.gitignore_global'

# Ignore bundler config. /.bundle

# Ignore the default SQLite database. 
/db/*.sqlite3 
/db/*.sqlite3-journal

# Ignore all logfiles and tempfiles. 
/log/* /tmp/* 
!/log/.keep 
!/tmp/.keep

# Ignore Byebug command history file. 
.byebug_history 
```

For a **.gitignore** file that ignores more, see an [example .gitignore file](https://github.com/RailsApps/rails-composer/blob/master/files/gitignore.txt) from the RailsApps project.

## Git Workflow

Your workflow with Git will move through four distinct phases as you add or edit files.

### Untracked Files

The first phase is a "dirty" state of untracked and changed files, before any snapshot. The `git status` command lists all folders or files that are not checked into the repository. 

```console 
$ git status 
On branch master

Initial commit

Untracked files: (use "git add <file>..." to include in what will be committed)

 .gitignore Gemfile Gemfile.lock README.md Rakefile app/ bin/ config.ru config/ db/ lib/ log/ public/ test/ tmp/ vendor/

nothing added to commit but untracked files present (use "git add" to track)
``` 

In the online version of this book (the HTML version), the example above appears in green. In the terminal window on your computer, it will be red, showing you untracked files.

Here the `git status` command tells us that we have many untracked files. We have created new files and they are saved on the computer's hard disk but nothing has been recorded in the Git repository.

### Staging

I call this step, "Pose for your snapshot."

Recording files in the Git repository takes two steps: staging and committing. There will be times when you change many files at once. For example, you may fix a bug, add a new graphic, and change a form. You might think you'd like to have Git automatically record all the changes as you save each file. But the story of your project would be confusing and overly detailed. Git requires you to mark one or more files ("staging") before recording the changes ("committing"). This gives you fine-grained control over the recorded history of your project.

You can mark individual files to be staged: 

```console 
$ git add Gemfile 
```

Adding individual files allows you to selectively record the history of your project. For example, you might stage and commit a series of bug fixes before you stage and commit new features. Applying the time traveler analogy, it will be easier to travel back to look at bug fixes if they are not mixed in with new features.

More often, you'll mark all the files to be staged. Do so now: 

```console 
$ git add -A 
```

Running `git status` will show you a long list of files that are staged and ready to commit.

There are three forms of the `git add` command:

- `git add foo.txt` adds a file named **foo.txt** - `git add .` adds all new files and changed files, except deleted files - `git add -A` adds everything, including deletions

If it seems nonsensical that the command `git add -A` "adds deletions," don't worry. Like time travel, Git will stretch your understanding of what makes sense.

Most often, you can simply use the `git add -A` form of the command.

Now that you've marked the files that will be committed to the repository, you've told everyone to pose, and you're ready to take the snapshot.

### Committing

The previous step, the "posing" step, or staging, gives you an opportunity to select particular files before you commit. If you've only worked on one feature, you'll likely stage and commit all your files.

The next step is a "commit" which I like to call, "clicking the snapshot."

When you "make a commit", you include a message that describes the work you've done. For a time traveler, the "commit message" is important; you are leaving a trail to help you find your way into the past. Google will show you dozens of blog posts about "writing better commit messages" but common sense can be your guide. For example, writing "fix registration form to catch blank email addresses" will be more helpful than merely writing "fix bugs." And if you wonder why commit messages are commonly written in the imperative not past tense ("fix" not "fixed"), it's a time traveler convention.

Now commit your project to the repository: 

```console 
$ git commit -m "Initial commit" 
```

The `-m` flag lets you add a message for the commit.

The pristine state of your new Rails application is now recorded in the repository on your local computer.

Running `git status` will tell you "nothing to commit, working directory clean."

```console 
$ git status On branch master nothing to commit, working directory clean 
``` 

You've recorded your snapshot locally. Next let's see a list of previous snapshots. Then we'll learn how to save your snapshots remotely to GitHub.

### Git Log

You can use the `git log` command to see your project history: 

```console 
$ git log commit 8da41eec9e864ed91b4a445d8cefdf7893e2faf6 Author: Daniel Kehoe <daniel@danielkehoe.com> Date: Fri Dec 18 10:30:12 2015 +0700

 Initial commit 
 ``` 
 
The long string of characters that follows "commit" is an ID, or marker, that will help you travel back in time if you need to do so.

If you get "stuck" in `git log`, type `q` to return to the command prompt.

I like to use the `git log` command with an option for a compact listing: 

```console 
$ git log --oneline 8da41ee Initial commit 
``` 

Don't worry if your console doesn't show `8da41ee`. The ID for your commit will be different.

The listing is easier to review when it is displayed in a compact format. The commit ID is abbreviated but it is all you need to travel back in time.

### Repositories

When we talk about repositories, or "repos," we mean the archive of our git commits. The local repo is located in the hidden folder named **.git/** in the project directory. Of course, if your hard drive crashes, or your computer is lost or stolen, you'll lose your local repo along with your project. So it is wise to save your repository in the cloud. The GitHub site is a place to save repositories. GitHub is also a place for collaboration. Most Rails developers save their repositories to Github, as either a public repo for open source projects, or a private repo for proprietary projects.

### Pushing to GitHub

We've seen three phases of the Git workflow: *untracked*, *staged*, and *committed*.

A fourth stage is important when you work with others: *pushing* to GitHub.

The repositories hosted on your GitHub account establish your reputation as a Rails developer for employers and developers you may work with. Even if your first project is copied from a tutorial, it shows you are serious about learning Rails and studying conscientiously.

Did you create a GitHub account? Now would be a good time to add your repo to GitHub.

Go to GitHub and [create a new empty repository](https://github.com/new) for your project. Name the repository "learn-rails" and give it a description. If the repository is public, hosting on GitHub is free. Don't be reluctant to go public with an unfinished or half-baked project; everyone expects projects on GitHub to be works in progress.

Add GitHub as a remote repository for your project and push your local project to GitHub. Before you copy and paste the command, notice that you need to insert your own GitHub account name. In other words, change `YOUR_GITHUB_ACCOUNT` in the command shown below.

\begin{aside} \label{aside:change_github_account} \heading{Warning}

STOP! Be sure to change `YOUR_GITHUB_ACCOUNT` to your GitHub user name. If you don't, you will create a mess that you have to [fix with the instructions here](https://github.com/RailsApps/learn-rails/issues/58).

\end{aside}

```console 
$ git remote add origin https://github.com/YOUR_GITHUB_ACCOUNT/learn-rails.git $ git push -u origin master 
```

The `-u` option sets up Git so you can use `git push` in the future without explicitly specifying GitHub as the destination.

Now you can view your project repository on GitHub at:

- [https://github.com/YOUR_GITHUB_ACCOUNT/learn-rails](https://github.com/YOUR_GITHUB_ACCOUNT/learn-rails)

Obviously you must change `YOUR_GITHUB_ACCOUNT` in the web address to see your own repository.

Take a look. It's an exact copy of the project on your local computer.

If you haven't used GitHub before, take some time to explore. GitHub is absolutely essential to all open source Rails development.

You may notice that the **README.md** file is automatically incorporated into the home page of the project repository on GitHub. For our next step, we'll update the README file, commit it to the local repo, and push it up to GitHub. It will be good practice for using Git.

## The README

Changing the README file is a good way to practice with Git. It's also a good habit to edit the README file whenever you create a new project. It's easy to neglect the README for little projects that you've just started. But replacing a default README file shows you are a disciplined, conscientious developer who will be a good collaborator.

The new README file can be brief. Just state your intentions and acknowledge any code you've borrowed. For this project you could say, "Excited to learn Rails with help from Daniel Kehoe's book!"

In your text editor, open the file **README.md** and replace the contents: 

```text 
# Learning Rails

Learning Rails with a tutorial from [learn-rails.com](http://learn-rails.com/).

```

GitHub lets you add formatting using your choice of markup syntax, depending on the file extension you add to the filename:

- README.md uses the [GitHub Flavored Markdown](https://help.github.com/articles/github-flavored-markdown) syntax - README.textile uses the [Textile](http://redcloth.org/hobix.com/textile/) syntax - README.rdoc uses the [rdoc](http://rdoc.rubyforge.org/RDoc.html) syntax

We'll use Markdown syntax by adding the `#` character before the first line of text to force a headline. And we'll add a link that leads to the [learn-rails.com](http://learn-rails.com/) website.

There's no requirement that you use Markdown syntax in your README file. Markdown simply is a popular way to add formatting to improve readability.

Use `git status` to see what has changed:

```console 
$ git status On branch master Changes not staged for commit: (use "git add <file>..." to update what will be committed) (use "git checkout -- <file>..." to discard changes in working directory)

 modified: README.md

no changes added to commit (use "git add" and/or "git commit -a") 
```

Here's our typical workflow. We'll stage and commit the change:

```console 
$ git add -A $ git commit -m "update README" 
``` 
Then we'll push the change to GitHub:

```console 
$ git push origin master 
```

If you decide not to use GitHub for this tutorial, you can skip this step (and skip it throughout the tutorial).

Take a look at your GitHub repository (refresh the web page). Very cool! The README file has been updated.

The `git log` command will display your project history:

```console 
$ git log --oneline 69b9b6c update README 8da41ee Initial commit 
```

To learn more about Git, I recommend the book [Learn Enough Git to Be Dangerous](https://www.learnenough.com/git-tutorial) by my colleague Michael Hartl. An online version is available for free.

Now that you're comfortable with Git, we can begin customizing our new Rails application. 