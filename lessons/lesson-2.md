# notes for lesson 2

## prep
- laptop (plug in to power)
- water 
- quit Slack and Mail (notifications)
- iPad with lesson, next assignment notes
- LibreOffice Draw running, diagrams ready
- Sublime x 2 running
- Terminal open, in repo dir

## opening notes
- ask in chat if you have questions; less scrolling than raising hand in a large group
- forgot to ask about Zoom meeting length last poll; will do this time
    + I agree that 60m is best, but there is _so much_ to cover...
    + I will try to structure the interactive sessions with less general/more optional topics last, and questions throughout, so people can leave early if they need to

## summary/commentary/followup
(summary and commentary is intermingled this week)

Udemy 3: Fork and Clone (aka more basics):
- clone and fork (which is GH only, remember)
- your repo is yours!  more on this later
- more git log, git diff; HEAD and ~ notations
    + again, GUIs make this a lot easier
- git annotate > git blame is the preferred command (annotate calls blame now)
    + often built in to IDE, etc; but GH also makes it easy (hopefully you don't need it too often!)
- undoing changes
    + git checkout apparently > git restore in very latest version
    + git status gives you hints 
    + git reset later today
- git comment -a and git add .: not a fan; explicit is better than implicit

Udemy 4: Working with Branches
- branches are git's secret weapon
    + this is where it gets substantial
    + unless you've used svn etc., you have no idea how bad it was before
    + you hated branches because merging was impossible
    + use them freely for isolation, for safety, for damage control
- but branching brings along opinions; git is so flexible that the tool itself doesn't really suggest a specific way to do things; and so developers have a lot of opinions on the matter (including Eduardo)
    + part of what we want to do in this course is give you some good basic advice; others will disagree!
    + that said, his emphasis on good practices is important; it's better to have some scheme, for some reason, than no scheme
- git branch state (what's checked out) is persistant across all sessions and clients; it's a property of the repo
    + cd .git and more HEAD, refs/heads
- .gitignore
    + I have a .DS_Store in polls/ now; not just network drives, but any folder you visit in Finder
    + show a GH .gitignore, maybe NeuTu or JW one
    + not a license to be messy!  do not mix stuff that shouldn't be mixed!
    + if you're ignoring a lot of files, it's a bad sign (although admittedly some tools will require certain layouts that are not good choices)
    + remember, you commit .gitignore, so it should only be for things that other people have to worry about, too!
- he calls video 29 "Syncing Branches", and that's an important choice of words; git is not only about version control in one repository (which may have one or many contributors itself), but it's also about synchronizing changes among many repos
- tracking remotes: most commonly, you're only tracking one remote and you never change it; but it can be done, if you want to (a) change from GitHub to Bitbucket, etc, or (b) grab changes from multiple sources (eg, multiple people who have forked a project)
- remember git fetch to grab changes from remote if your client doesn't see them (more soon)
- merging: see 34: ffwd vs recursive (no commit vs commit w/multiple parents); mention octopus merge
- yes, branch deletion is normal practice!  you don't actually delete the commits, though, just the branch (more soon)
- pull requests:
    + again, just a GH thing; requests to pull and merge
    + his demos start to get a little confusing from here on as he demonstrates collaboration; watch carefully which accounts he works in


## central concept: your repo is yours (local vs remote repos)
- ie, local and remote repos and GH
- git as two tools: version control for you, and
    synchronization between repos (your repo is yours)
- git = distributed version controls, compared to earlier generation of centralized tools (eg, svn or CVS)
- so your repo is an equal peer; it contains _everything_ as of the last sync (push/pull)
    + that includes the whole history, unlike svn
    + if GH disappears, you have everything
    + if someone else pushes garbage, and you haven't pulled, you still have a good copy of the repo
- important rule for staying out of trouble: if things have gone weird in your repo, DO NOT PUSH; get help solving it on your machine before you let it loose
- corollary: if things are weird and you _have_ pushed, tell people not to pull!  keep the errors from propagating
- if you don't push branches, they are essentially private; this can be useful


## central concept: git as a graph: commits, HEAD, branches, and remotes
- kind of rethinking doing this freehand...
- LibreOffice Draw?  yes, looks like it'll do basic OmniGraffle stuff, which is all I need
    + practice!  generate some reference diagrams/starting point for what I want to demo
    + or: prepare it beforehand, so you can upload it for future reference?

- arrows point to parents!  it's tempting to point into the future, but that's not the way the data structures work here
- directed acyclical graph; a commit can have multiple parents or multiple children, but there is always a directionality back to the first commit


- detached HEAD in here?
    + and git deletion (gc) of commits unreachable from all branch heads
    + which doesn't include commits in merged branches!

- think like a git website & Pro Git book




## git reset
- full section with demo or just a mention?
- seems valuable to demonstrate as a tool for getting out of trouble
- git reset vs git checkout
- hard, soft, mixed options
- danger zone!
- lets you branching after the fact


# deleting, renaming, and moving files
- deleting files: 
    +  you can delete the file and then stage it (git add) (which is weird because the file is gone!)
    +  or you can git rm which does both
    +  then commit
    +  but you have to tell git what you did
- likewise move/rename
    + git tracks content, not files...and rename doesn't change content
    + git knows this, but how that's displayed can be weird and confusing
    + use git mv to do this
- demo this


## tips & miscellaneous
- git command docs:
    + "Pro Git" book on git-scm.com
    + demo searching on "man git command"

- branch deletion
    + showing commits aren't deleted
    + pushing deletion


## next assignment
- section 5, merge conflicts, is like the previous lessons
- section 6 is kind of a mess; read the email, ask questions early (I don't want to spend a lot of time going over it now)


## Q&A
