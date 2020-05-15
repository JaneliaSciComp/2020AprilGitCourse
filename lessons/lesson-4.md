# notes for lesson 4

## prep
- laptop (plug in to power)
- water 
- quit Slack and Mail (notifications)
- iPad with lesson
- Sublime x 2 running
- Terminal open, in repo dir
- Libre Office Draw with fresh copy of lesson 4 diagram
- Safari open with
    + class repo


## summary/commentary
- not much to talk about here
Udemy 7: working with open-source project
- a lot of this is process and not "how to", but process matters
- I didn't know that GH had all that templating
- to be honest, I don't agree with the commit guidelines, but they do appear to be widespread
    + capitalize but no period is particularly offensive to me
    + remember Emerson: foolish consistency...
    + and remember Python: practicality beats purity
    + but as usual, follow project guidelines (if they exist)

Udemy 8: Markdown
- widely used; translates almost directly into html
- other dialects exist!
    + lots of blogging platforms, editors use md
    + Jupyter notebooks
- GH turns headers into link anchors
- tables are not that flexible; can't do multi-line cells

Udemy 9: Pages
- compare wiki?

Udemy 10: IDE integration

Udemy 11: CI/CD
- CI = when a commit is made, compile/build project; run tests
    + if problems, email appropriate people
    + there are cloud services that do this (circle CI)
        * JW uses circle CI
    + there are "git hooks" that do this outside GitHub, but generally require some kind of server (Hudson/Jenkins)
- CD = after CI, deploy project
    + mobile app example
    + really not very instructive; the concept is what matters
    + JW does not use CD; we have a specific release cycle; need all clients and servers updated together


## rebase vs merge
- git rebase = move or combine commits
    + somewhat similar to merge
- rollback commits in one location; move to new location; replay changes, forming new commits
- generally used to keep commit history neat and linear
    + if you're working and you pull a lot, each pull gives you a little loop with a new commit
    + rebase = "just keep stacking my changes on top of everyone else's"; it's a ffwd merge (no loops, no new commits)
- diagram plain rebase then git pull --rebase
- can be used to clean up a string of commits before pushing
    + use interactive rebasing to squash = combine commits
    + makes a more concise commit history; easier for people to comprehend
    + not going to demo this
- NEVER REBASE WHAT YOU'VE PUSHED!
    + seriously, never ever change anything you've pushed
    + rebasing, resetting, amending = ways to rewrite history = be very careful
- cherry pick
    + not a merge or rebase
    + duplicates commit to a new branch (but new hash!)
    + often used for hotfixing or moving small changes not worth a merge
    + diagram this
- when to use which?
    + if you need to pull regularly while you're working to get new changes, especially from unrelated parts of the code, probably git pull --rebase
        * but beware: because no merge and thus no conflicts, your changes will always overwrite changes that were pulled!
        * can be a problem when editing project-wide build-related files
    + if you're integrating feature branches, bigger chunks of work that might conflict with existing work, better to explicitly merge
        * this will let you check for and resolve conflicts
        * but again be wary of non-conflicting wrongness
    + if you're contributing to a project, follow guidelines; they may require you to rebase and squash commits
    + cherry picking is only for moving very small pieces of code (eg, hotfixes moved from branch to master to deploy)


## other GitHub tools
- markdown & pages (covered in video)
- GitHub wiki (mentioned above?)
- project
- CI/CD


## advanced topics/you should know this exists

### things you will probably need/use
- demo all of these!
- stage hunks (GUIs & git add -p)
- git remote and git remote show origin 
- DoI for GitHub repo
    + https://guides.github.com/activities/citable-code/
    + via Zenodo, open access organization from CERN

### things you might or might not need
- all the details on how git works internally:
    + Pro Git book "Internals" chapter
    + https://jwiegley.github.io/git-from-the-bottom-up/
- git bisect
- git-lfs for storing large binary files
- git amend for rewriting commits, commit messages
- git submodules and subtrees
    + repo within a repo
    + can be hard to work with (but tools constantly improve)
    + I have no experience with them, but:
    + submodule points to a specific commit in another repo
        * "easier to push, harder to pull"
    + subtree is a copy that's pulled into your repo
        * "easier to pull, harder to push"


## wrap-up
- you've got to use it and practice or it'll never become natural
    + you're going to screw up
    + but we (me, SciComp) can help if you do
    + #git-and-github channel for the Slack workspace?
- want more?  check out Atlassian's git tutorial (on resources page)
- big thanks to Caroline & Rob
- video links and final survey out on Tuesday
    + your feedback is greatly appreciated; plus, you will be benefitting future class participants


## Q&A
- unmute everyone, free-for-all?



