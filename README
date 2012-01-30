I recently read 3 UI books: Design of Everyday Things, About Face, and Don't make me Think. 

The books did make me think. A lot. A lot about a tool I use everyday...

git (http://git-scm.com).

Git is sweet tool. But, the UI could use some love. The UI is confusing and inconsistent for newbies (sometimes I remove things with a "rm" and others times with a "-d"). In fact, even after three years of using git, there are commands I find myself forgetting (do I want git revert or git reset... and does it need HARD HEAD or -- SOMETHING?). 

A good UI would make these commands second nature for intermediate users like myself.   

An interface should never be a by-product of the implementation of the system. The UI should be crafted apart from anything happening under the hood. This is where the Git UI goes wrong. The command git reset is a good example. I use it to undo things. But, its called reset and has a bunch of strange parameters which have to do with writes I am making to the git index when I undo something. Using the command properly requires me to have a clear understanding of the guts of git. A common command like undo should not require the user to understand how the git index works. 

    # what if we just had
    git unstage
    # or
    git undo

All the "resetting" and funny "HARD -- HEAD" parameters would happen behind the scenes. The user would be happier. 

Here are a few other questions I have about the git UI:
1. I have some files I want to stage. Do I want "git add .", "git add -u", or "git add -A"? Which does what and why? Confused.
2. Oh geez. I just staged something by accident. How do I unstage it? Its git reset? Or is it git revert? Do I do a HARD, --, HEAD, FILE, or something else. Brain damage.  
3. I want to see my changes... git diff? git diff HEAD? or git diff --cached? why not git diff CACHED? Grrrr....
4. git status. It is cluttered with commands telling me how to undo things. If the commands were easy enough to remember we would not need them in the output here. And... what does "changed but not updated mean"? I did update my file. Do you mean "changed but not staged"? And, could we get a few fewer # signs please?

Here is my shot at re-creating just a few parts of the Git UI. My hope is that all of these commands become part of git one day.

Staging files 
--------------

    # stage all changes, and file deletions. Everything except unknown files. Instead of git add -u, just type
    git stage

    # stage just one file change or deletion. Instead of git add FILE and git rm FILE, just type:
    git stage FILE

## Unstaging Files

Ooops. I staged a changed that I do not want to commit. 

    # remove one file from the stage. Instead of remembering git reset HEAD -- file, just type:
    git unstage FILE

    #unstage all the files you have in the stage right now. Instead of git reset HEAD, just type:
    git unstage


## Undoing changes I have made:

Ok. I tried something. It does not work. Just get me back to the last commit.

    # undo all the changes I made to working directory. Instead of git reset --hard HEAD, just type:
    git undo

    #just undo the changes I made to one file. Rather than git checkout FILE (side note: why is it not git reset FILE? or is it?) instead, just type: 
    git undo FILE

## Deleting Files

Let's get rid of git rm. Lets not even tell newbies about it. Just delete files you want from your project, then:

    # smart enough to stage files you have removed as well!
    git stage
    git stage FILE

## Status

More readable. Less # signs. Less instructions.

    git status

    Staged for commit:
        M daemon.c
        N test.txt

    Unstaged Changes (will NOT be committed):
        M hello.c
        ? new.c

## Automatic Setup

The first time I run git from a new computer I am most often greeted with an error. Not a very friendly way to great new users. The message says that I have not set my email and user name. 

If this error occurs, shouldn't git just ask me for this information and proceed with the command I typed? Yep, it should. 

    # my first ever commit with GIT! I would prefer not to get an error.
    git commit -m "yippeee git!"

    Before git commits your changes, please tell git your name and email so it can attribute this change to you.
    
        Please enter your name? Jon Saints
        Please enter your email? saintsjd@gmail.com

    Thank you! Committing...

This replaces the more confusing:

    ERROR! Stupid user... you should have known to enter your name and email by typing this first:
    git config --global user.name "Scott Chacon"
    git config --global user.email "schacon@gmail.com"

## Switching branches

    # I switch branches with the checkout command. I am being picky. But what if we had:
    git switch BRANCH

## Showing things I have changed.

This part of git is confusing. Instead of git diff HEAD, git diff, and git diff --cached

    # Show all changes from the last commit
    git diff
    git diff HEAD

    # show difference between the stage and my code
    git diff STAGE

    # difference between my stage and last commit
    git diff STAGE HEAD

    # difference between two branches or revisions
    git diff branch1 branch2
    git diff AD34E BCDE543

## Deleting a branch

    # Let's be consistent with git remote command. Instead of git branch -d 
    git branch rm BRANCH

I am going to make a small python wrapper to try out these commands. It will be called gum. And, it will just write git commands for you. 

gum = Git User (interface) Makeover. "gum unstage" here we come!

The code is on github: https://github.com/saintsjd/gum

Comments welcome.
