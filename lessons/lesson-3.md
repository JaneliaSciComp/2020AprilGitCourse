# notes for lesson 3

## prep
- laptop (plug in to power)
- water 
- quit Slack and Mail (notifications)
- iPad with lesson, next assignment notes
- Sublime x 2 running
- Terminal open, in repo dir
- repo with merge conflict ready
    + GUIs pointing to it
- Libre Office Draw with fresh copy of lesson 3 diagram
- Safari open with
    + class repo
    + workflow links
    + project guidelines lines


## summary/commentary
Udemy 5: Merge Conflicts
- sounds like something you should have prevented, if you branched right/were organized/etc; they aren't
- merge conflicts are the price you pay for enabling collaboration (including with yourself!)
- respect but do not fear them; the benefit of branching outweighs the cost of merging
- as always, git status suggest what you might want to do
- GUIs make it easier (the editor markers are a pain) (more later) 
- add/commit to finish; default merge message
- pull request = request to merge
    + I like his comment on pushback; the requester should work so the merge is clean
    + often that means merging master into your branch so your branch back into master is trivial
- tags: use to mark a commit for all time 
    + used to mark release or maybe a publication
    + but if you do this all the time, maybe just record commit hash instead
- the releases thing on GH is a GH-only thing, not git
    + basically it adds the tag, then creates some archives
    + if you tag and push tag, it happens automatically
    + better to follow common practices for versioning (there's a link on GH; it's horribly officious, though)

Udemy 6: Collaboration in GitHub
- this is where the videos and my Zoom sessions start to diverge; I'm not going to say much about all the GH stuff Eduardo covers; I'll spend in-class time on git stuff he doesn't cover
- not going to cover the colab stuff
- protect branches
- require reviews
- issues and pull requests: this is the dialog between collaborators
    + opening issues for anything significant, even if you're the only one doing it, is worthwhile; it's a form of documentation
        * we also have JIRA internally
    + in pull request, use words "fix/close/resolve #issue" to auto close issue on PR merge
    + there's a setting for automatically deleting branches after merge


## common workflows with branches
- there are many branching and merging schemes
    + which to use depends on what you want out of it
    + having something is better than nothing
    + also includes tagging
    + actual examples will follow the generic discussion
- what to consider?
    + what are the roles you want to separate?  who works on what features/bugs/etc.?  who makes decisions about the code?  who is allowed to commit or merge to master?  who needs approval, and how is that granted?  
    + how do you perform releases, and how frequently?  do you need to support old releases or can you always have users update to the next release?  how quickly must you fix bugs (hotfixes?)?  do you have explicit alpha/beta/RC stages?  
    + how do you test, validate, deploy?  do you have explicit QA or beta testers, or automated testing?  do people download from GH or is there a build/deploy phase?  do releases involve a lot of infrastructure (eg, multiple clients and servers updating together)?  do you practice CI/CD?  are releases performed by a different team?
    + do you need tool support?  there are eg macros/scripts/plugins that manage the branching in merging for some of these established and more complicated workflows
- these are the common ones I came across:
    + gitflow workflow (https://nvie.com/posts/a-successful-git-branching-model/): highly regimented dev/release stages; useful if you must support many releases; work on dev, release from master
    + GitHub flow (https://guides.github.com/introduction/flow/) = feature branch; test and release from branch before merging to master; designed for SaaS (eg web app) that is released frequently, only one version
    + Gitlab flow (https://about.gitlab.com/blog/2014/09/29/gitlab-flow/): work on master but have test/deploy branches; useful for staged deployment (eg ios app that needs approval)
    + forking workflow: open source typical; fork and work in own repo, pull request to source repo, which does gatekeeping on merges
- examples (show):
    + JW: all trusted; feature branches for long-running work; we often commit to master (no pull requests); releases are done from master and tagged (used to use branches); "hotfixes" are done from master (used to be from release branch); we run CI (build/test on every commit, email if fails); deployment is via Docker swarm of containers + client download/update (all manual); we use JIRA for issues
    + NeuTu: more open-source-like; Ting controls "master"; others work on branches and submit pull requests that he reviews and merges (even though I think I can commit to master...); multiple branches for feature testing; no CI/CD (I think); lots of issues and pull requests in GH
    + marktips: working alone, on master; tagged releases
    + always respect the project guidelines (more in upcoming Udemy section)!
        * Julia: https://github.com/JuliaLang/julia/blob/master/CONTRIBUTING.md#git-recommendations-for-pull-requests
        * CatMaid: https://github.com/catmaid/CATMAID/blob/master/CONTRIBUTING.md
- what should you do?
    + respect existing project guidelines!
    + if alone: feature branches (yes, even alone!), release from master, with tags (esp. if your code is used by a few others)
    + if open-source style collaboration, use forking workflow
    + in a lab group, with multiple people committing and/or using, probably master/dev/features, maybe with release branches depending on your user base
    + either way, add branches as your use case requires


## merge conflict tools
- GUIs much better with multiple files, multiple changes per file
- need to set up a conflict, then compare
    + merge branch new-chef into master; conflicts result (and non-conflicting changes, too!)
        * be aware of non-conflicting changes!  when they are "wrong", you'll get bitten
    + in editor
    + Sublime Merge; base/merge
        * Stuart Berg likes kdiff3 for similar reasons (shows you the two conflicting files, the resulting file, **and** the common ancestor) (but looks like a pain to config...)
    + GitHub desktop tool doesn't have a built-in merge confict tool
        * but you can configure one you like
        * eg, FileMerge on MacOS (with dev tools/Xcode installed) 
        * IntelliJ/PyCharm and others do


## git reset
- moved from week 2!
- this is a powerful and dangerous command; usually used for getting yourself out of trouble in your repo
- we now have background to understand how it works
- recall git checkout moves HEAD and updates local files to match new commit
- git reset moves both HEAD and the branch label, and working set, and staging
    + its arguments (hard, soft, mixed) determine details
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
    + be really careful
    + you can use branches to mitigate risk
- git revert: more of an "inverse commit"; rather than back up, it moves forward, but it adds a new commit that undoes previous changes
    + safer but messier
    + not sure I've ever used this or seen it used?
    + but it is appropriate to use to fix things after you've pushed


## git stash
- git is nosy and possessive; it wants to know everything that's going on in its directory (except the .gitignored stuff)
- if you try to do some operations (especially checkout, which changes local files), it will complain if some local files are in an intermediate state
    + eg, can't checkout a branch with staged files (modified files, too?  seems not?)
- git stash sets aside all changes to tracked files and all staged changes
    + basically resets to HEAD
    + does **not** affect untracked files!
- git stash apply = apply changes to files, leave in stash
- more commonly, git stash pop = apply changes, delete from stash
- it is a stack!  repeated stash/stash pop work as expected
- git stash show = shows the stack
- more options
- why?  the typical use (I find) is, "oops, I'm on the wrong branch"
    + change tracked file
    + wrong branch!  but "git checkout" won't let me swap branches
    + git stash; git checkout my-branch; git stash pop
    + (if it's a new branch, you can just create it then check it out)
- but occasionally useful for getting changes out of git's way while it does other things
    + I think IntelliJ uses it to do some trickery with its changelists?
- demo this?


## next assignment
- next set of videos: only one must-watch; others optional
- no poll this week or for week 4 (no one is responding)
- there will be a final-final poll that I hope you will fill out


## Q&A


