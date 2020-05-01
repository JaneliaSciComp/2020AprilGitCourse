# notes for lesson 1

## prep
- laptop (plug in to power)
- AirPods?
- water 
- quit Slack and Mail (notifications)
- open IJ, Sublime x 2, GitHub app, terminal (cd to the class repo)
- iPad with lesson 1 notes (and assignment 2 notes)

## course intro
- up-front honesty: there's going to be some rough edges
    + we planned to do a course maybe later in the year
    + rushed to put this together right now
    + but some of this will be less well prepared than I would like (ask questions!)
- the course is really fluid
    + overall Udemy + SciComp = lots of flexibility
    + before the class, request specific content/topics (give me lead time!)
    + that goes for pace, too; kind of worried the pace is too aggressive
- Zoom logistics
    + webinar mode: I can't see you! (share screen?)
    + raise hand for question; moderators will unmute you
    + or v. quick comments in chat (eg, bigger font, can't hear, etc)
    + recorded; Zoom links Monday
    + in case of sudden disconnects, watch Slack channel
    + I'll send a link to a poll after each class
- Udemy:
    + I really liked this instructor's approach; very close to the way I would present things
    + I hope he is understandable; accent light, grammar excellent, and either very well rehearsed or well edited or both
    + when he plays with repos and code, you don't need to understand what he's doing or follow it slavishly; you could, for example, just create random text files and edit them instead of html and css
    + likewise, when he forks/clones other outside repositories, you don't need to use the same ones he does; you can work with repos you're already familiar with, or you can use the repo for this class
    + however, if you feel more comfortable being able to compare directly to his output, it's best to follow him closely
- the course repo
    + linked from Slack; show
    + meant both as example but will contain a lot of my notes and things
        * curriculum (updated) and resources on wiki
        * including lesson plans; they are not admittedly meant for you to read, but they might help
        * also my notes on the videos
    + will use as scratch space for demos, etc.


## summary/commentary
Udemy 1: Getting Started with Git
- what is version control
- git vs GitHub
- install, setup commandline, config name/email
- git init, add, commit
- git diff; git sha hashes

Udemy 2: Getting Started with GitHub
- git vs GitHub 
- create account
- push and pull
- edit, commit on GH
- git status

### commentary
- git vs GH: think of git as version control plus collaboration tools
    + GH adds a remote repository hosting service, then adds even more tools for development and collaboration
- the staging area: 
    + kind of a pain (two stage to commit) (but notice GH skips this!)
    + it does allow you to more carefully control what you commit
    + often you may find yourself making a small change (eg, fixing a misspelling) somewhere else while working; careful staging lets you isolate that change in one commit while not affecting your ongoing work 
    + later: staging hunks
    + gotcha: need to re-stage files if you make more changes!  staging area is a copy from working directory
    + tip: mostly I never stage until I'm ready to commit
- git diff 
    + on the command line: ugh; see GUI comments
    + however, git diff usually isolates changes well; sometimes it just flags the whole things as changed
    + gotcha: change file permissions is not well shown in most git diffs
- SHA
    + aka git hash
- GitHub changes UI often; I didn't see the "contributors" tab shown in the video 
- naming conventions: remote = origin, and branch = master; don't change these
- git status is your friend!  we will see this over and over; it shows you the state of the repo and suggests what to do next; it's never wrong, although you may not always understand what you're seeing


## thoughts on git command-line & GUI
- why command-line?
    + it's the most consistent interface, and the reference interface; lots of GUI clients, but only one command-line, basically
    + GUI clients use the command line underneath; many will even show you the exact commands they are executing; knowing commandline = understanding what they are really doing, regardless of what they call it
    + if you get into trouble (and you will), solutions online (eg Stack Overflow) will show you the answers on the command-line; it's the common language of git
- purists might reject the need for GUIs, but I believe they are very useful
    + I use command-line, GUI client, IDE integration, and GitHub interchangeably, depending on the task
    + typically much better for showing info, browsing; GUIs will usually show you a lot of info by default, in a well-organized fashion that is much better than "git log" output
        * and that goes double for "git diff"
    + I'm frankly too lazy to remember all the command line options and syntax
- examples (demo these, compare against commandline):
    + you can see VSCode a bit on Eduardo's screen
    + IntelliJ/PyCharm
    + Sublime Text/Merge
    + GitHub Desktop
- there are apparently tools for Matlab, but I am not familiar with them
- if you use one of the common IDEs, watch the applicable section 10 video
- I encourage you to experiment with the git integration of the tools you already used; it's valuable to run them side-by-side with the command line as you learn, so you can understand the mapping betwen them


## GitHub organizations
- show the SciComp org
- makes it obvious when repos belong to a group and not an individual
- provides tools for managing permissions of groups of repos and developers
- recent change make these teams/orgs now mostly free


## what should I commit? when should I commit?
- time for practical stuff!
- lots of opinions in git, because it's very flexible; my goal is to give you advice that will work, practically, as a beginner, most of the time
- what to commit?  git is intended for code, but useful for anything with similar characteristics:
    + need to keep version history
        * reproducibility
        * keep stable version/fix errors
    + thus changeable things; if something (eg data, results) is kept forever, don't put it in git (mostly...); there are other ways to archive static things
    + best for text and text-like things; git can compare and store those efficiently
        * binaries should not in general be put in git, unless they are small and change rarely
        * otherwise your repo, which stores all changes, will get big fast
    + you want to enable safe group editing on the content
- as a result, some things like Jupyter (Python, etc.) notebooks make an uncomfortable fit
    + they combine code and results
    + while text, it's structured in a way that makes it hard to generate git diffs
- likewise, you should try to separate input from code
    + you should not need to edit code to run it!
    + read your input from another file, which probably doesn't belong in git
    + and that implies you shouldn't run your code inside the repo if it saves files!  
- when to commit?  there are multiple schools of thought here
    + often enough to prevent losing work to various disasters (computer or cognitive (ie, "what the heck am I doing?  I want to back up!"))
    + after each change that works correctly, so you can return to it if you make later errors
    + in small enough chunks that it will be obvious later which commit contains the change that may need fixing
    + generally, pretty darn often
    + show some of my commits, maybe from NeuTu?
- there are similar concerns with pushes, too
    + generally you don't push every commit, only larger groups of commits that make up a coherent feature
        * unless you're the only one working on a branch, maybe
    + still keep in mind the hardward disaster angle (how often you feel comfortable getting the code off you computer)
    + but not so often it annoys your collaborators!  some projects have guidelines about how commits should be structured; follow guidelines of projects you contribute to
        * later we'll talk about squashing commits, where you can combine multiple commits into one before pushing, so your collaborators see something cleaned up compared to what you really did

## tips & miscellaneous
- the git repository is located inside your folder in an invisible .git folder
- don't mess with it!  it holds everything--every change, every version 
    + this can take significant disk space in a big, old project

- there are two basic ways to create a repo and link it to GitHub
- create the repo on GitHub first with at least one file (eg, README)
    + then clone that repo into a local folder and start working there
    + you don't do "git init" in this case, just "git clone"
- or: create the repo on GitHub without any files
    + create it simultaneously on your local disk with "git init"
    + create, add, and commit files
    + or possibly copy files in and add and commit
    + then set the remote as the instructor does
    + and push
- honestly, I find the first way easier, because GUI tools will usually set up the remote and branch tracking automatically if you do


## looking forward...next assignment
- see "assignment 2.txt"
- and note that it'll be sent out after class
- Zoom recording takes some time to process; I expect to send links Monday morning


## Q&A



