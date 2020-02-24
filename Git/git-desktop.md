# GitHub Desktop guide

The commands and instrucctions in this file are directed to users of
[GitHub Desktop](https://desktop.github.com/). Only available for macosx and
Windows.

## Table of contents
1. [Setting up Git](#setting-up-git)
1. [Cloning a repository](#cloning-a-repository)
1. [Configuring a repository](#configuring-a-repository)
1. [Saving changes with Git](#saving-changes-with-git)
1. [Getting changes from the remote repository](#getting-changes-from-the-remote-repository)
1. [Recovering old versions](#recovering-old-versions)
1. [Miscellaneous commands](#miscellaneous-commands)

## Setting up Git
In order to start using Git, you have to download and install
[GitHub Desktop](https://desktop.github.com/). This interface is
maintained by GitHub, so its default values tend to be tailored to
GitHub users instead of GitLab users, but it is still possible to use
all features with any remote.

Right after the installation you will see a screen similar to the following
one:

![welcome](GH_Desktop_images/0-GH_desktop_welcome.png)

If you are not GitHub users, select "Skip this step" to enter your
username and mail. If you are a GitHub user, you can log in so the
interface gets your data from GitHub. The page to enter username and
mail looks like this:

![gitconfig](GH_Desktop_images/0-GH_desktop_gitconfig.png)

## Cloning a repository
Right after configuring GitHub Desktop, you will get to a page where one
of the options is to clone a repository (see below). Otherwise, you can
clone repositories from the menu bar doing `File`->`Clone repository...`. You should see screens like these:

![clone](GH_Desktop_images/1-GH_desktop_clone.png)

![clone_url](GH_Desktop_images/2-GH_desktop_clone_url.png)


At some point, you may also have to enter your
username and password (if the repository is private).

![authenticate](GH_Desktop_images/3-GH_desktop_authenticate.png)

![done](GH_Desktop_images/4-GH_desktop_done.png)

Now you can go crazy and edit whatever file you want in the repository. But wait, what if I don't want to track all the files in the repository?

## Configuring a repository
It is hardly the case that **all** the files in the folder must be tracked by Git,
you may have hidden files, checkpoints, binary files... of which (for whatever
the reason) you do not care. Git uses a file called `.gitignore` to exclude this
files from the repository. Moreover, there are plenty of templates on both
GitHub and GitLab of files to exclude based on the language of the repository.
One example of `.gitignore` file for tex would be:

```
## Core latex/pdflatex auxiliary files:
*.aux
*.lof
*.log
*.lot
*.fls
*.out
*.toc
*.fmt
*.fot
*.cb
*.cb2
.*.lb

## Intermediate documents:
*.dvi
*/build/*.pdf
```

The Tex template on GitHub has 242 lines to be thorough. Nothing bad happens
if some of the extensions or folders in your `.gitignore` are not present
in your repo.

## Saving changes with Git
They are quite intertwined but we are working with two different tools: Git and
GitLab. One thing is to save a change in Git (so it creates a "checkpoint") of the
saved state and another is to sync this changes with the remote repository.
In many of the cases, both actions are done at the same time, however, it is
important to know the difference because each requires a different command.
Moreover, to allow extra freedom to the user, the saving step itself can also
be divided in two commands. You will generally find 2 cases when saving changes.

#### Saving files
NOTE: In case you are comparing with Git bash, it should be noted that
in this case there is no difference between saving files known and
unknown to Git.
If you have changed files, the repository's page on the interface will
show them with a checkbox. The checkbox allows you to save the files in
different commits (which may be better for clarity of the history and/or
for resetting changes only on one of the files easily). For example,
here I want to commit the files related to Git bash and Git desktop
separately:

![commit](GH_Desktop_images/5-GH_desktop_commit.png)


#### Sending changes to the remote repository
After committing the changes, the local version will be more advanced than the
remote. To sync them click on `Push origin`:

![push](GH_Desktop_images/6-GH_desktop_push.png)

## Getting changes from the remote repository
This one will generally require 2 clicks, one to `Fetch origin` and another
to `Pull origin`

![pull](GH_Desktop_images/7-GH_desktop_pull.png)

Note that the `Pull origin` will only appear after running `Fetch origin`
if there have been changes in the remote. If you are working in multiple
machines or with other people, you should keep in mind to always fetch
and pull before starting to work.

## Recovering old versions
The capabilities of recovering old versions using the GitHub desktop are
exaggeratedly limited compared to Git bash, but it is still useful for basic
cases.

Before resetting though, two notes taken directly from the [official
docs](https://help.github.com/en/desktop/contributing-to-projects/reverting-a-commit):

1. When you revert multiple commits, it's best to revert in order
from newest to oldest. If you revert commits in a different order,
you may see merge conflicts.
1. When you revert to a previous commit, the revert is also a commit.
The original commit also remains in the repository's history. As opposed
to what happens generally with Git bash.

To revert commits (effectively recovering the version before said commit)
click on `History`, then right click on the commit to be reverted and
`Revert commit`.

![revert](GH_Desktop_images/8-GH_desktop_revert.png)

## Miscellaneous commands
This section lists some useful git commands, that do not fit inside any of the
specific actions detailed, but can be used in any of them to make the process
more verbose, more clear or to make sure you are on the right path.

#### `git status`
The `git status` equivalent is the `Changes` tab.

#### `git log`
The `git log` equivalent is the `History` tab.
