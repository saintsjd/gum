About
----------

gum is a small set of cli improvements for git

Git is sweet tool. But, the UI could use some love. For more info see
http://www.saintsjd.com/2012/01/a-better-ui-for-git/ ‎

Example:

    # Instead of: git reset HEAD -- file just type
    > git unstage

Gum runs git reset HEAD -- file for you.

The gum project's goals:
*  Improvements are different things to different people. So, gum will never get in the way of using regular git commands.
*  Gum will work cross-platform: Mac, PC, Linux, others.
*  Gum will make the most common things we do in git a bit more friendly. If we are good at what we do, then we can make git a bit easier to learn for newbies along the way. 

There is no code here yet. Just ideas for future development of git. See the issue list to track progress.

Thank you all for your enthusiastic and generous code contributions. I will be reviewing them over the course of this coming week. Then I will post the best implementation here.


Ideas we are considering for implementation
--------

Staging files
========

    # Stage all changes, and file deletions. Leave unknown files alone.
    # Instead of git add -u, just type:
    > git stage

    # Stage just one file change or deletion.
    # Instead of git add FILE and git rm FILE, just type:
    > git stage FILE

Unstaging Files
========

Ooops. I staged a changed that I do not want to commit.

    # Remove one file from the stage.
    # Instead of git reset HEAD -- file, just type:
    > git unstage FILE

    # unstage all the files you have in the stage right now.
    # Instead of git reset HEAD, just type:
    > git unstage

Undoing changes I have made:
========

Ok. I tried something. It does not work. Just get me back to the last commit.

    # Undo all the changes I made to working directory.
    # Automatically save the user's work in a stash, then
    # Instead of git stash; git reset --hard HEAD, just type:
    > git retreat
    All files changed back to their state at the last commit. Your work has been saved in stash@{1}. 
    

    # Just undo the changes I made to one file.
    # Automatically save a stash of the user's work first
    # Rather than git checkout FILE (side note: why is it not git reset FILE? or is it?)
    # Instead, just type:
    > git retreat FILE
    The file was changed back to the it's state at last commit. Your work has been saved in stash@{1}. 

Deleting Files
========

Let's get rid of git rm. Lets not even tell newbies about it. Just delete files you want from your project, then:

    # smart enough to stage files you have removed as well!!!!
    > git stage
    > git stage FILE

Status
========

More readable. Less # signs. Less instructions.

    > git status

    Staged for commit:
        M daemon.c
        N test.txt

    Unstaged Changes (will NOT be committed):
        M hello.c
        ? new.c

Nice and clean. No reminders about how to undo things... you already know that: git undo. And, no # signs!!

Defaulting to "status -s" might be good enough here. 

Automatic Setup
========

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
========

    # I switch branches with the checkout command. Its ok, but what if we had:
    > git switch BRANCH

Showing things I have changed
========

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
========

    # Let's be consistent with git remote command. Instead of git branch -d
    > git branch rm BRANCH
