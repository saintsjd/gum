About
----------

Git is an amazing tool, but the UI could use some love. For more info see:
http://www.saintsjd.com/2012/01/a-better-ui-for-git/ ‎

gum is a small set of UI improvements for git. It is very much a work in progress

Installing Gum
=====

Just add the aliases to your .gitconfig file.

    [alias]
        # gum aliases for git version 3
    
        #add files to the staging area
        freeze="!f() { ( [ -z $@ ] && git add -A || git add -A "$@" ) && git st; }; f"

        # remove files from the staging area
        unfreeze="!f() { ([ -z "$@" ] && (git reset -q HEAD > /dev/null 2>&1 || echo "first commit must be unfrozen file by file. better error message coming soon") || (git reset -q HEAD -- $@ > /dev/null 2>&1 || git rm -q --cached $@ ) ) && git st; }; f"
	
        # Show short status with current branch name
        st="!f() { br=$(git status | head -1) && echo "${br}" && git status -s; }; f"
    			
	
Usage
======

    # stage/freeze a snapshot of my project (including new and deleted files)
    # also shows a quick preview. Commit it if you like what you see. unfreeze if you don't.
    > git freeze

    # stage/freeze a snapshot of one file (including new and deleted files)
    # also shows a quick preview. Commit it if you like it. unfreeze if you don't.
    > git freeze <file>

    # unstage/unfreeze all changes in the snapshot (including new and deleted files)
    > git unfreeze

    # unstage/unfreeze one file in the snapshot (including new and deleted files)
    > git unfreeze <file>

    # check the status of my files... right now this just runs git status -s. This will get fancier.
    > git st
    
Feature Ideas! 
=====

    # cleaner output by default for status
    > git status
    Frozen snapshot ready for commit:
        M daemon.c
        N test.txt

    Unfrozen Changes (will NOT be committed):
        M hello.c
        ? new.c
        
    # synchronize all changes with my remote branch
    # like github for mac and legit... automatically runs stash, pull, push, unstash
    > git sync <remote>
    
    
    # browse old revisions like Mac TimeMachine...
    
    # go back one revision
    > git history back
    
    # go forward one revision
    > git history forward
    
    # go back, back, back, then return to latest
    > git history back
    > git history back
    > git history back
    > git history latest
    
    # display log
    > git history

