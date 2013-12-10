githooks
========

My personal githooks, which help me avoid silly or obvious mistakes.

These githooks were written with a Ruby-on-Rails app in mind, so most of the hecks are related common coding issues in Ruby, JavaScript, or general git use.  However, I've sprinkled a few checks here and there for problems in other languages, and I'm happy to consider more.

If you know of a common mistake, please create an issue, or better yet, a pull request.

pre-commit
----------
1. Catches common errors, such as checking in...
    1. git merge conflict markers
    2. Personalized debugging statements
    3. Calls to invoke the debugger, either in Ruby or in JavaScript
2. Catches other suspicious code, such as the addition of calls to `alert` (very uncommon for me)
3. ~~Syntax-check all .rb files~~ Temporarily deactivated
6. Check for probable private key commits. 
4. *Conditionally* prevents changes to `.ruby-version` (and `.rbenv-version`).  In my experience, those files are committed *accidentally* (by developers who changed them locally with no intention of committing the changes) far more often then they are committed intentionally.  Prevents these changes by default. 
    * Run `git config hooks.allowrubyversionchange true` in a project directory to allow it for that particular project.
5. *Conditionally* ensures that changes to assets are accompanied by a change to production.rb (required in my former employer's main work environment).  Does *not* prevent these changes by default.
    * Run `git config hooks.newassetsrequireproductionchange true` in a project directory to prevent it for that particular project.

Bypassing the Checks
--------------------
Call git commit with the `--no-verify flag` to ignore all of these checks.

There's no way to turn off individual checks (other than the "conditional" ones mentioned above).  That's why this script goes to pains to display *all* errors, rather than just the first one.  If you want to throw the `--no-verify` flag, you should clean up your code to the point where the **only** errors are the ones you feel safe ignoring, **then** throw the flag.

Installation
============
Clone this repository locally, then run its setup script, passing the location of *the repo that you want to add hooks to* as an input argument.
    
    git clone git@github.com:bobgilmore/githooks.git
    cd (into the newly-created repository directory)
    ./setup.sh path_to_repo_that_you_want_to_add_hooks_to

This will create symbolic links in the `.git` directory of the repo that you're adding to, which point to this githooks repo.

Updating the Hooks
==================
Since the githook files that we're creating in your individual repos are all symbolic links into *this* repo, updating or changing *this* repo will affect *all repos that you set this up for at once.*

Advice for For Editors
======================

Only Add Repo-Specific Changes *Conditionally*
----------------------------------------------
Since all of your affected repos have symlinks to one shared set of hooks, avoid making project-specific changes to the hook files.  Rather, consider making the behavior change based on an **optional** git configuration variable, and then setting that variable for the projects where it's necessary.

See how I handle `newassetsrequireproductionchange` in the `pre-commit` file for an example of how to do this.

Writing Checks to Run (or Ignore) for Some Extensions or Directories
-----------------------
I don't have many examples of checks that should be run (or ignored) based on extension or directory, so that code isn't really designed to scale.

If you want to add more checks like that, talk to me - we should probably make the solutions scalable.