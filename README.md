About
----------

There is no code here yet. Just ideas for future development of git.

Git is sweet tool. But, the UI could use some love. For more info see
http://www.saintsjd.com/2012/01/a-better-ui-for-git/ ‎

gum is a User (interface) Makeover for Git.

This code is a small python wrapper to try out some of these improvements. gum just writes complex git commands for you. 

    # Instead of: git reset HEAD -- file just type
    > git unstage

Gum runs git rest --hard HEAD for you.

My hope is that all of these commands become part of git one day. We can make git more fun for beginners and easier for forgetful intermediates like me.

Staging files
----------

    # Stage all changes, and file deletions. Leave unknown files alone.
    # Instead of git add -u, just type:
    > git stage

    # Stage just one file change or deletion.
    # Instead of git add FILE and git rm FILE, just type:
    > git stage FILE

Unstaging Files
----------

Ooops. I staged a changed that I do not want to commit.

    # Remove one file from the stage.
    # Instead of git reset HEAD -- file, just type:
    > git unstage FILE

    # unstage all the files you have in the stage right now.
    # Instead of git reset HEAD, just type:
    > git unstage

Undoing changes I have made:
----------

Ok. I tried something. It does not work. Just get me back to the last commit.

    # Undo all the changes I made to working directory.
    # Instead of git reset --hard HEAD, just type:
    > git undo

    # Just undo the changes I made to one file.
    # Rather than git checkout FILE (side note: why is it not git reset FILE? or is it?)
    # Instead, just type:
    > git undo FILE

Deleting Files
----------

Let's get rid of git rm. Lets not even tell newbies about it. Just delete files you want from your project, then:

    # smart enough to stage files you have removed as well!!!!
    > git stage
    > git stage FILE

Status
----------

More readable. Less # signs. Less instructions.

    > git status

    Staged for commit:
        M daemon.c
        N test.txt

    Unstaged Changes (will NOT be committed):
        M hello.c
        ? new.c

Nice and clean. No reminders about how to undo things... you already know that: git undo. And, no # signs!!

Automatic Setup
----------

The first time I run git from a new computer I am most often greeted with an error. Not a very friendly way to great new users. The message says that I have not set my email and user name.

If this error occurs, shouldn't git just ask me for this information and proceed with the command I typed? Yep, it should.

    # my first ever commit with GIT! Don't greet me with an error.
    > git commit -m "yippeee git!"

    Howdy! So that git can give you credit for changes you make
        Please enter your name? Jon Saints
        Please enter your email? email@gmail.com
    Thank you! Committing...

This replaces the more confusing error message that git shows users now:

    Error 123: Look! another stupid user is _trying_ to learn git. 

    You should have known to type this first:
    > git config --global user.name "Jon Saints"
    > git config --global user.email "gmail@gmail.com"

    DUFUS!! Just give up now. Seriously.
    Switching branches

Switching branches
---------

    # I switch branches with the checkout command. Its ok, but what if we had:
    > git switch BRANCH

Showing things I have changed
---------

This is one of the most important parts of git. And, it is confusing.

    # What is the output? Can you remember which is which?
    # git diff
    # git diff HEAD
    # git diff --cached or git diff CACHED?

    # Instead we can... 

    # Show all changes from the last commit
    > git diff
    # or
    > git diff HEAD

    # Show difference between the stage and my code
    > git diff STAGE

    # Difference between my stage and last commit
    > git diff STAGE HEAD

    # Difference between two branches or revisions
    > git diff branch1 branch2
    > git diff AD34E BCDE543

Deleting a branch
---------

    # Let's be consistent with git remote command. Instead of git branch -d
    > git branch rm BRANCH
