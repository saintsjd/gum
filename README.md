About
----------

Git is an amazing tool, but the UI could use some love. For more info see:
http://www.saintsjd.com/2012/01/a-better-ui-for-git/ ‎

gum is a small set of UI improvements for git. It is very much a work in progress

Installing Gum
=====

Just add the aliases to your .gitconfig file.

    [alias]
        # gum aliases for git version 1
    
        # tell git to ignore a file
        ignore="!f() { [ -z "$@" ] && echo "git: usage git ignore [file]" || ( ([ ! -e .gitignore ] && touch .gitignore); echo $1 >>.gitignore && echo "Ignoring file $1" && git rm --cached "$@" > /dev/null 2>&1 && git status -s ); }; f"

        #add files to the staging area
        freeze="!f() { ( [ -z $@ ] && git add -A || git add -A "$@" ) && git status -s; }; f"

        # remove files from the staging area
        unfreeze="!f() { ([ -z "$@" ] && (git reset -q HEAD > /dev/null 2>&1 || echo "first commit must be unfrozen file by file. better error message coming soon") || (git reset -q HEAD -- $@ > /dev/null 2>&1 || git rm -q --cached $@ ) ) && git status -s ; }; f"
	
        # eventually we want to make nicer output but for now
        st=status -s
	
        # Navigate through the log - eventually allow for git history back and git history forward to flip through old versions like mac time machine
        history=log
		
	
Usage
======

    # stage/freeze a snapshot of my project (including new and deleted files)
    # then shows a quick preview. Commit it if you like what you see
    > git freeze

    # stage/freeze a snapshot of one file (including new and deleted files)
    # then shows a quick preview. Commit it if you like what you see.
    > git freeze <file>

    # unstage/unfreeze all changes in the snapshot (including new and deleted files)
    > git unfreeze

    # unstage/unfreeze one file in the snapshot (including new and deleted files)
    > git unfreeze <file>

    # smarter file ignoring
    # adds the file to .gitignore
    # also runs git rm --cached file for you! (I always forget to do that)
    > git ignore <file>

    # check the status of my files... right now this just runs git status -s. This will get facier.
    > git st
    
Features to Come! 
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

