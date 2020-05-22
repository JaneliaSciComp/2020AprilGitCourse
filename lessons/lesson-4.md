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
    + my GH pages test page
    + citeable code link


## summary/commentary
- not much to talk about here
Udemy 7: working with open-source project
- a lot of this is process and not "how to", but process matters
- I didn't know that GH had all that templating
- commit message guidelines: to be honest, I don't agree with a lot of them, but they do appear to be widespread, and you should know they exist
    + seem tailored to command-line world
    + capitalize but no period is particularly offensive to me
    + remember Emerson: foolish consistency...
    + and remember Python: practicality beats purity
    + but as usual, follow project guidelines!

Udemy 8: Markdown
- widely used; translates almost directly into html
- other dialects exist!
    + lots of blogging platforms, editors use md
    + Jupyter notebooks
- tables are not that flexible; can't do multi-line cells

Udemy 9: Pages
- my test pages: https://olbris.github.io/GHPagesTest/
- compare wiki

Udemy 10: IDE integration

Udemy 11: CI/CD
- CI = when a commit is made, compile/build project; run tests
    + if problems, email appropriate people
    + there are cloud services that do this (circle CI)
        * JW uses circle CI
    + there are "git hooks" that do this outside GitHub, but generally require some kind of server (Hudson/Jenkins)
- CD = after CI, deploy project
    + video does a mobile app example
    + JW does not use CD; we have a specific release cycle; need all clients and servers updated together


## rebase vs merge
- git rebase = move or combine commits
    + somewhat similar to merge
- rollback commits in one location; move to new location; replay changes, forming new commits
- generally used to keep commit history neat and linear
    + if you're working and you pull a lot, each pull gives you a little loop with a new commit
    + rebase = "just keep stacking my changes on top of everyone else's"; it's a ffwd merge (no loops, no new commits)
    + BUT: doesn't cause merge conflicts!  your branch always "wins" over master
- diagram plain rebase then git pull --rebase
    + note that for pull --rebase, the two branches are the same, just one local and one remote
- demo git pull --rebase on commandline
    + edit in GH first, then local
    + show commit hash and history in GUI
    + git pull --rebase and look at history/hash again
- git rebase can be used to clean up a string of commits before pushing
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
        * remember, rebasing is mostly to keep commit history clean
        * but again be wary of non-conflicting wrongness
    + cherry picking is only for moving very small pieces of code (eg, hotfixes moved from branch to master to deploy)
    + if you're contributing to a project, follow guidelines; they may require you to rebase and squash commits
    + never rebase if you've pushed!  


## other GitHub tools
- basically, the top tab bar
- pages (covered in video)
- GitHub wiki (mentioned above)
- issue tracking (of course)
    + you can turn off issue tracking and the wiki if you like
- CI/CD (actions) (mentioned above) 
- security scanning
- insights (includes the graph)
- project: 
    + task workflows; agile/kanban stuff
    + like Trello or JIRA (but far less customizable)
    + issues, pull requests, notes
    + to do/in progress/done states; assignees, milestones, labels
    + automation; eg, new pull request > in progress; close issue > done
    + wish I hadn't been so rushed, or I would've used this while planning course; I have a text file checklist with ~50 tasks I've tracked, with lists first/next/later/done
    + process matters!  organization matters!
- settings: anything permission related is here
- gists: small text snippet to share with people (code fragments, small piece of data, etc.)
- probably others lurking that I don't know about


## advanced topics/you should know this exists

### things you will probably need/use
- stage hunks (GUIs & git add -p) (demo)
    + changes need to be distant to be detected as separate hunks
    + git unstage is strangely difficult on command line; need to carefully git reset HEAD (--soft or --mixed?)
- git remote and git remote show origin (demo)
- DoI for GitHub repo
    + https://guides.github.com/activities/citable-code/
    + via Zenodo, open access organization from CERN

### things you might or might not need
- details on how git works internally (links on GH repo resources page):
    + Pro Git book "Internals" chapter
    + https://jwiegley.github.io/git-from-the-bottom-up/
- git amend for rewriting commits, commit messages
- git bisect for finding which commit broke something
- git-lfs for improving handling of large files (caching and lazy loading)
- git submodules and subtrees
    + repo within a repo
    + can be hard to work with (though tools constantly improve)
    + I have no experience with them, but:
    + submodule points to a specific commit in another repo
        * "easier to push, harder to pull"
    + subtree is a copy that's pulled into your repo
        * "easier to pull, harder to push"
    + so I _think_ it's a matter of (a) if the included code is rapidly changing (by you or othes), and (b) how easy you want it to be for users


## wrap-up
- end of the course!
- hope it's helpful not just for technical details, but also for hints on how to improve the way you work; process and organization matters; part of being a professional is being able to complete work and deliver it; tools like git help you with that; organization and discipline is something you can learn
- you've got to use it and practice or it'll never become natural
    + start small; new/small project, trivial workflow; build from there
    + you're going to screw up
        * but we (me, SciComp) can advise you if you have problems
        * when we moved JW from svn, we had some really good messes to fix
        * remember don't push if you have problems!
        * new branch where you are and commit to that
    + #git-github channel for the Slack workspace
- want more?
    + check out Atlassian's git tutorial (on resources page)
    + more Udemy courses
- big thanks to Caroline & Rob
- last video links and final survey out on Tuesday
    + your feedback is greatly appreciated; plus, you will be benefitting future class participants


## Q&A



