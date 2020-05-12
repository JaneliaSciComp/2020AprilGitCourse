# notes for lesson 2

## prep
- laptop (plug in to power)
- water 
- quit Slack and Mail (notifications)
- iPad with lesson, next assignment notes
- LibreOffice Draw running, diagrams ready (fresh duplicate file)
- Sublime x 2 running
- Terminal open, in repo dir

## opening notes
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
- git commit -a and git add .
    + not a fan; explicit is better than implicit; caught people committing core dumps, etc.
    + but understandable if using command line

Udemy 4: Working with Branches
- branches are git's secret weapon
    + this is where it gets substantial
    + unless you've used svn etc., you have no idea how bad it was before
    + you hated branches because merging was impossible
    + use them freely for isolation: safety, damage control
- but branching brings along opinions; git is so flexible that the tool itself doesn't really suggest a specific way to do things; and so developers have a lot of opinions on the matter (including Eduardo)
    + part of what we want to do in this course is give you some good basic advice; others will disagree!
    + my presentation on branching workflows will be next class
    + that said, his emphasis on good practices is important; it's better to have some scheme, for some reason, than no scheme
- git branch state (what's checked out) is persistant across all sessions and clients; it's a property of the repo
    + cd .git and more HEAD, refs/heads
- .gitignore
    + I have a .DS_Store in polls/ now; not just network drives, but any folder you visit in Finder
    + show GH .gitignores: JW, NeuTu, marktips
    + not a license to be messy!  do not mix stuff that shouldn't be mixed!
    + if you're ignoring a lot of files, it's a bad sign (although admittedly some tools will require certain layouts that are not good choices)
    + remember, you commit .gitignore, so it should only be for things that other people have to worry about, too!
    + edit it in Sublime merge, show "untracked files" change, and commit and push
- he calls video 29 "Syncing Branches", and that's an important choice of words; git is not only about version control in one repository (which may have one or many contributors itself), but it's also about synchronizing changes among many repos
- tracking remotes: most commonly, you're only tracking one remote and you never change it; but it can be done, if you want to (a) change from GitHub to Bitbucket, etc, or (b) grab changes from multiple sources (eg, multiple people who have forked a project)
- lots more that I'll cover in "graph" part
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
- this will be a very big section; going to explain the central concept of git commits as nodes in a graph
    + important unifying framework for making sense of commits, branching and merging, and pushing and pulling
    + will answer questions like how merges differ, why it's OK to delete branches, and the difference between git pull and git fetch
    + see think like a git website & Pro Git book (resources in course GH page)
- directed acyclical graph (DAG); a commit can have multiple parents or  children, but there is a directionality back to the first commit; no loops

commits, master, HEAD
- commits have parents
    + commit has metadata (who/when/etc)
    + commit has data (generally stored as diff from parent)
- HEAD is a label pointing to parent of next commit
    + look into .git: HEAD and refs/master/head (= hash of HEAD commit)
    + advances when you commit
branching and merging
- branches are also labels pointing to commits
    + also advance when you commit on that branch
    + and HEAD actually knows what branch you're on, so it points to branch
    + explains why branching is so easy (compare svn)
    + I hate Eduardo's train-track diagram
- merges
    + commit on a branch, but not on master, then merge: just move the pointer
    + there's no new commit = ffwd merge
    + but do work on master first, then merge: now we're combining changes from two (or more) branches, so we need a new commit that has multiple parents = recursive strategy merge
    + either way, the old branch label is now unneeded; it can be deleted; the commits don't disappear or change; the recursive merge even keeps the branch name in the commit message (by default)
detached HEAD
- you can checkout any commit you like; if it's not a branch label, it's a detached HEAD
    + you should be wary but not afraid of this
    + if you just checkout another branch, no worries
    + if you do work, though...danger!  
        * git will periodically look for commits it can't reach from branch labels; it will then delete them
        * so any commits done on a detached HEAD are vulnerable, after you move HEAD to somewhere else
        * what to do?  just add a branch label right there!
- likewise, if you delete an unmerged branch, you're just removing the label
    + for a while, that commit may be reachable
    + but the git gc will delete it at some point
    + note that most of the time, git/GitHub will complain loudly if you try to delete an unmerged branch (just as it will suggest deleting a branch you've merged)
remotes & fetch/push/pull
- this is where we see git as repo synchronization tool (as opposed to just version control)
- your repo and its remote are linked and have a common history
    + remote has its own branch labels
    + your local remote has a copy of those branches (eg, origin/master)
    + this is the "tracking branch"
- make a local change: master advances, origin/master does not
    + then you push; assume no changes on origin
    + commit is copied to origin, master advances on origin
    + and your o/m label advances
- someone else pushes a change, local unchanged
    + git status doesn't help; it only knows what's local
    + if you pulled, though, you'd get the change without issue; what's happening?
    + git pull = git fetch + git merge
    + git fetch updates all remote branches and tags
    + now git status = one behind
    + in fact, you can git branch -a to show all branches, including remotes
    + you can git log origin/master to show its history 
    + and in this case, git merge is ffwd
- someone pushes a change, but local changed
    + git status says one ahead (it's just local)
    + push: rejected!  but git status doesn't change?
    + git fetch grabs remote branches
    + now git status = diverged (ahead and behind)
    + git pull/git merge = new commit
    + now git status is one ahead
    + then git push
- demo the push/pull parts on the command line, especially the rejected message
- that is a lot to take in...but hopefully that framework will give you a useful way to think about git commits and branches


## deleting, renaming, and moving files
- like creating or editing files, anything else you do to local files is something git wants to know about
- deleting files: 
    +  you can delete the file and then stage it (git add) (which is weird because the file is gone!)
    +  or you can git rm which does both
    +  then commit
    +  either way tells git what you did
- likewise move/rename
    + git tracks content, not files...and rename doesn't change content
        * corollary: you can't add/commit empty folders!
    + git knows this, but how that's displayed can be weird and confusing
        * sometimes you need to force it to "follow history" to get history across moves/renames
    + use git mv (source file) (destination file) to do this
    + question from Slack: collaborator renamed folder, then git pull leaves her with original name folder, but empty, and git status doesn't care?
        * couldn't reproduce in limited testing; generally should work; you'll have to remove the folder manually; as long as it's empty and git status doesn't show it, you should be fine
- demo this


## tips & miscellaneous
- (peek ahead) tags are labels like branches, but they never advance
- if you delete branches locally, you need to delete them remotely, too
    + git branch -d (branchname) is local
    + git push origin --delete (branchname) is remote
- never commit passwords, API keys, etc.!  
    + it's a pain to remove them, since you have to remove from history as well as current file; worse if you push; there are tools, if just changing them isn't feasible
    + put secrets in separate files or environment variables or deployment scripts
    + there are GH bots that look for these, some friendly, some not!


## git reset
- **moved to week 3!**
- this is a powerful and dangerous command; usually used for getting yourself out of trouble in your repo
- we now have background to understand how it works
- as we've seen, git checkout moves HEAD
- git reset moves both HEAD and the branch label
    + its arguments (hard, soft, mixed) determine what happens to local files and staged files
    + note staging area = staging index = "the index"
    + --hard = most common, most dangerous; sets local/staged files = HEAD
        * basically, discards everything and resets HEAD and branch to chosen commit
        * it's a drastic go-back-in-time option
        * it discards information
    + --mixed = default = staged files removed, changes moved back to local files, which are unchanged
        * doesn't discard uncommitted changes, but leaves none of them staged
    + --soft = only branch moved; no staged/local files changed
- git reset by default works on HEAD; this has the effect of cleaning up the staging area and local files; not that dangerous
    + and GUI tools often make this easy to do manually anyway (discard changes and unstage files)
- git reset on an older commit is where it gets dangerous (and useful)
    + once you git reset --hard back to an earlier commit, the later commits on that branch become orphaned and vulnerable to gc
    + NEVER DO THIS IF YOU'VE PUSHED
    + you're rewriting history, and you should not rewrite history that you've shared
    + from Atlassian tutorial: "As soon as you add new commits after the reset, Git will think that your local history has diverged from origin/master, and the merge commit required to synchronize your repositories is likely to confuse and frustrate your team."
    + the fix (in my experience) might involve one person fixing the repo and everyone else re-cloning, for example
- branching after the fact
    + get to a point, uh oh, should have branched
    + make the branch now!
    + git reset master back to where you wanted it
    + checkout new branch and continue
- so the bottom line on git reset is:
    + never after pushing
    + be really really careful
    + you can use branches (after the fact) to mitigate risk
- git revert: more of an "inverse commit"; rather than back up, it moves forward, but it adds a new commit that undoes previous changes
    + safer but messier?
    + not sure I've ever used this or seen it used?
    + but it is appropriate to fix things after you've pushed
- kind of don't want to demo, but I could...


## next assignment
- section 5, merge conflicts, is like the previous lessons
- section 6 is kind of a mess; read the email, ask questions early (I don't want to spend a lot of time going over it now)


## Q&A


