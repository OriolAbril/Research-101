# Git from bash

The commands and instrucctions in this file are directed to users of Git from bash.
That is, users of Git in Unix (linux and macosx in the command line) or users of
[GitWindows](https://gitforwindows.org/).

## Table of contents
1. [Setting up Git](#setting-up-git)
1. [Cloning a repository](#cloning-a-repository)
1. [Configuring a repository](#configuring-a-repository)
1. [Saving changes with Git](#saving-changes-with-git)
1. [Getting changes from the remote repository](#getting-changes-from-the-remote-repository)
1. [Recovering old versions](#recovering-old-versions)
1. [Miscellaneous commands](#miscellaneous-commands)

## Setting up Git
In order to start using Git, you have to install it and then configure some
variables.

#### Installation on Windows
Download the executable on [gitforwindows.org](https://gitforwindows.org/) and
install.

#### Installation on Debian/Ubuntu based systems
Open a terminal and run:

    $ sudo apt install git

#### Configuring Git
To configure Git, you only need to set two variables, the username and mail.
However, it may be interesting to also set some extra variables.

```
$ git config --global user.name "Your Name Comes Here"
$ git config --global user.email you@yourdomain.example.com
```

In GitWindows, the git editor is set during the install process, however, in
Unix systems, it is generally a good idea to choose one you are comfortable with.

    $ git config --global core.editor <editor-name>

Another generally good idea is to set the default username:

    $ git config --global credential.username yourusername

## Cloning a repository
Cloning a repository is a one-liner, however, you may also have to enter your
username and password (if the repository is private).

    $ git clone https://gitlab.com/OriolAbril/research-101.git

Now you can go crazy and edit whatever file you want in the repository. But wait, what if I don't want to track all the files in the repository?

## Configuring a repository
It is hardly the case that **all** the files in the folder must be tracked by Git,
you may have hidden files, checkpoints, binary files... of which (for whatever
the reason) you do not care. Git uses a file called `.gitignore` to exclude this
files from the repository. Moreover, there are plenty of templates on both
GitHub and GitLab of files to exclude based on the language of the repository.
One example of `.gitignore` file for Tex would be:

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

The Tex template on GitHub has 242 lines to be thorough. Nothing bad happens if some
of the extensions or folders in your `.gitignore` are not present in your repo.

## Saving changes with Git
They are quite intertwined but we are working with two different tools: Git and
GitLab. One thing is to save a change in Git (so it creates a "checkpoint") of the
saved state and another is to sync this changes with the remote repository.
In many of the cases, both actions are done at the same time, however, it is
important to know the difference because each requires a different command.
Moreover, to allow extra freedom to the user, the saving step itself can also
be divided in two commands. You will generally find 2 cases when saving changes.

#### Saving files for the first time
Git tracks the changes and versions using diffs. It defines an initial state and
then it only stores the changes progressively done to this initial state. To
create a "new initial state" in Git you have to run

    $ git add <path>

where `<path>` can be a file, a folder, multiple files and folders separated by
a space, or `.` to include all the files in the
current folder at the same time. One a file has been added, it is already known
by Git.

#### Saving files known to Git
Saving files known to Git is done with the `git commit` command.

    $ git commit <path>

The path argument works like in `git add` but it can only _see_ files known to
Git. After running `git commit`, your editor will automatically open for you
to write the commit message, which should be a description of the changes.
The commit message will generally be useful to your future self more than anyone
else, so try to be good on yourself.

`git commit` accepts to useful flags: `-m "Commit message"` can be used for
short commit messages to avoid opening the editor and set the commit message
right away, and `-a` without argument will commit all modified changes known to
Git, it is like using `.` but it may be more clear or easier to remember (`a`
for all).

Nore info on the `git commit` command can be found in Git's [documentation](https://git-scm.com/docs/git-commit).

#### Sending changes to the remote repository
To send the commited changes to the remote repository, run:

    $ git push

## Getting changes from the remote repository
This one is a pure one-liner.

    $ git pull

## Recovering old versions
From a clean working directory (that is, [`git status`](#git-status) shows no
changes to commit nor untracked files), we will use `git reset`. This one is
the boundary of basic git commands. It has an extremely large number of
possibilities but we will basically consider 2. Your default go-to reset
should be the soft reset.

Before any resetting though, you first have to know what is the commit id
(alias commit hash) of your target. One way to get it is from [`git log`](#git-log),
from GitHub/GitLab or using some of the handy alias accepted by Git. We are
not covering branches, so the only useful alias left is `HEAD`. `HEAD` is
always targeting the latest commit, so `HEAD` itself is useless for resetting
to old commits, however, `HEAD~` represents the second most recent commit,
`HEAD~2` is 2 commits back from `HEAD` and so on.

#### Soft reset
The soft reset "uncommits" all changes between `HEAD` and your target without
erasing said changes. Instead of erasing them, it leaves all the changes as
uncommited files. This allows you to edit this uncommited files to salvage
anything you can and commit the now corrected changes.

    $ git reset --soft <commit>

#### Hard reset
The hard reset does erase forever the changes! Changes undone with a hard
reset cannot be recovered afterwards. Only use it whenever you are
completely sure of what you are doing.

    $ git reset --hard <commit>

## Miscellaneous commands
This section lists some useful git commands, that do not fit inside any of the
specific actions detailed, but can be used in any of them to make the process
more verbose, more clear or to make sure you are on the right path.

#### `git status`
When in doubt, run `git status`. It will show the following information:

```
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   Git/git-bash.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        Git/git-desktop.md

no changes added to commit (use "git add" and/or "git commit -a")
```

The first line indicates which is the branch we are working on. For now it
does not matter.

The second line indicates whether or not we are up to date with the remote,
and below how to solve it (either pulling or pushing). It should be noted
though that this information will generally not be relevant unless the
`git status` is run right after a `git fetch` or a `git pull`.

The **staged/to be committed** paragraph is about files _known to Git_ whose changes are "in line" to get commited. That is, you can also run `git add <path>` to get the
files "in line", and then run `git commit` without any path to commit all
changes waiting "in line". This may be useful when working with many files
in order to clearly see which will be committed and which not, but it does not
really matter at this level.

The **not staged** paragraph is about files _known to Git_ that have been modified. These are the files _seen_ by `git commit <path>`.

The **untracked** paragraph is about new files in the repository, that is _not known
to Git_. To get files out of this paragraph, `git add` must be run or the
file included in `.gitignore`.


#### `git log`
This command can be used to see the history of the repository. It shows each
commit, its author and more importantly its commit message. To see only the
latest changes, the flag `-n` can be used. One example output of `git log` is:

```
commit f28d1bed54006716565c5f28fb98e07600258b1a (HEAD -> master, origin/master, origin/HEAD)
Author: Oriol Abril <oriol.abril.pla@gmail.com>
Date:   Thu Dec 19 16:38:40 2019 +0100

    improve proposal template

commit 0d782fd168a85579cf833b21b732c92a559f2bd3
Author: Oriol Abril <oriol.abril.pla@gmail.com>
Date:   Thu Dec 19 16:32:44 2019 +0100

    Create Git bash instructions

    Git bash tutorial on basic Git actions written in markdown

commit b78673240f6a937561afa16c06c28f51cb49f564
Author: Oriol Abril <oriol.abril.pla@gmail.com>
Date:   Tue Dec 17 17:13:06 2019 +0000

    create issue template

commit db4799185df1929a450c2dd9b717bf02bb7a0f67
Author: Oriol Abril <oriol.abril.pla@gmail.com>
Date:   Tue Dec 17 16:58:56 2019 +0000

    Update README.md

commit 408a94a96b25bc64b2c21e066f91f261afae7963
Author: Oriol Abril <oriol.abril.pla@gmail.com>
Date:   Tue Dec 17 16:21:46 2019 +0000

    Initial commit
```

The log shows several commits, each with its id, its autor and mail, its date,
and its commit message. Moreover, the commits with alias available show
the aliases in parentheses after the commit id.
