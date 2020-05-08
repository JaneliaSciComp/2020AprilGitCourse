# notes for lesson 3

## prep
- laptop (plug in to power)
- water 
- quit Slack and Mail (notifications)
- iPad with lesson, next assignment notes

## summary/commentary

-- check: issue and pr linking; "solves" word required?



## merge conflict tools
- Stuart?


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
- these are the ones I came across over and over:
    + centralized workflow: svn-like; everyone trusted
    + gitflow workflow (https://nvie.com/posts/a-successful-git-branching-model/): highly regimented dev/release stages; useful if you must support many releases; work on dev, release from master
    + GitHub flow (https://guides.github.com/introduction/flow/) = feature branch workflow into master; much simpler than gitflow but still has a lot of trust
    + Gitlab flow (https://about.gitlab.com/blog/2014/09/29/gitlab-flow/): somewhere between; work on master but have test/deploy branches
    + forking workflow (OpenSource flow): this is best for cross-organization development, with gatekeeping on the master branch
- actual examples (show):
    + JW: all trusted; feature branches for long-running work; we often commit to master; releases are done from a branch and tagged; even "hotfixes" are done with a new release from master (not from the release branch)
    + NeuTu: more open-source-like; Ting controls "master"; others work on branches and submit pull requests that he reviews and merges (even though I think I can commit to master...)
    + marktips: working alone, on master; tagged releases
    + always respect the project guidelines!



## rebase vs merge


## git stash



## advanced topics I


## you should know this exists
- git remote and get remote show origin 
- git checkout > two new commands
    + git switch = for switching branches
    + git restore = for getting file from repo
- git bisect


## tips & miscellaneous
- embed git version in output when running scripts



## next assignment
- notes on upcoming optional stuff: what to do, ignore



## Q&A


