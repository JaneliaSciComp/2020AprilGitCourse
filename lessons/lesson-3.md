# notes for lesson 3

## prep
- laptop (plug in to power)
- water 
- quit Slack and Mail (notifications)
- iPad with lesson, next assignment notes
- Sublime x 2 running
- Terminal open, in repo dir

## summary/commentary
Udemy 5: Merge Conflicts
- merge conflicts are the price you pay for enabling collaboration
- respect but do not fear them; the benefit of branching outweighs the cost of merging
- git status tells you what to do
- GUIs!
- the editor markers are a pain
    + plus, there will be multiple copies of the file in the working set!
- add/commit to finish; default merge message
- remember git fetch/git pull when needed!
- pull request = request to merge
    + I like his comment on pushback; the requester should work so the merge is clean
- tags: use to mark a commit for all time 
- the release thing on GH is a GH-only thing

Udemy 6: Collaboration in GitHub
- not going to cover the colab stuff
- protect branches
- require reviews
- issues and pull requests: this is the dialog between collaborators
    + in pull request, use fix/close/resolve #issue to auto close issue
    + there's a setting for automatically deleting branches after merge



## common workflows with branches
- there are many branching and merging schemes
    + which to use depends on what you want out of it
    + having something is better than nothing
    + also includes tagging, to some extent
- what to consider?
    + what are the roles you want to separate?  who makes decisions about the code?  who is allowed to commit or merge to master?  who needs approval, and how is that granted?
    + how do you perform releases?  do you have alpha/beta/RC stages?  do you need to support old releases or can you always roll forward to the next release?  how quickly must you fix bugs (hotfixes?)?  do you practice CI/CD?
    + how do you test and validate?  do you have explicit QA or beta testers?
    + do you need tool support?  there are eg macros/scripts/plugins that manage the branching in merging for some of these established workflows
- these are the common ones I came across:
    + gitflow workflow (https://nvie.com/posts/a-successful-git-branching-model/): highly regimented dev/release stages; useful if you must support many releases; work on dev, release from master
    + GitHub flow (https://guides.github.com/introduction/flow/) = feature branch; test and release from branch before merging to master; designed for SaaS (eg web app) that is released frequently, only one version
    + Gitlab flow (https://about.gitlab.com/blog/2014/09/29/gitlab-flow/): somewhere between; work on master but have test/deploy branches; useful for staged deployment (eg ios app that needs approval)
    + forking workflow: open source typical; fork and work in own repo, pull request to source repo, which does gatekeeping
- actual examples (show):
    + JW: all trusted; feature branches for long-running work; we often commit to master; releases are done from a branch and tagged; even "hotfixes" are done with a new release from master (not from the release branch)
    + NeuTu: more open-source-like; Ting controls "master"; others work on branches and submit pull requests that he reviews and merges (even though I think I can commit to master...)
    + marktips: working alone, on master; tagged releases
    + always respect the project guidelines (more next section)!
        * Julia: https://github.com/JuliaLang/julia/blob/master/CONTRIBUTING.md#git-recommendations-for-pull-requests
        * React: https://github.com/facebook/react
        * CatMaid: https://github.com/catmaid/CATMAID/blob/master/CONTRIBUTING.md
- what should you do?
    + respect existing project guidelines!
    + if alone: feature branches (yes!), release from master, with tags
    + then add branches as your use case requires


## merge conflict tools
- GUIs much better with multiple files, multiple changes per file
- need to set up a conflict, then compare
    + in editor
    + Sublime Merge
    + Stuart likes kdiff3 because it shows you the two conflicting files, the resulting file, **and** the common ancestor
    + maybe the GitHub desktop tool?


## git reset
- moved from week 2!
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


## git stash





## next assignment
- notes on upcoming optional stuff: what to do, ignore
- no poll this week or for week 4 (no one is responding)
- there will be a final-final poll that I hope you will fill out


## Q&A


