git init ==> to initialize any non-versioned-controlled repo to be tracked by git. Tracking information is stored in ".git" folder. There are no branch after or when this is executed. Branches are yet to be born. First Branch will be created named "master" if we do first local commit. Alternatively, "git checkout -b <branch_name>" will create branch w/o any initial commit.
git branch -M [old_branch_name | current_branch_name(DEFAULT)] main ==> Github treates "main" as default branch now. To change the branch name locally we do this.
git remote add origin HTTP_URL.git  ==> Only when once branch is created, set/add/link/track the remote hosted repo to the local git repo. Here, "origin" is technically an upstream of this repo|branch.
git push -u origin main   ==> Once local repo is linked to remote repo, set the current local branch's upstream to one of the specific remote's|upstream's branch.
git push ==> how above is different from this? Well, if current working branch is made and is only known by local repo, this means that it is NOT tracking any of origin's(upstream's) branch. Which local branch is tracking which upstream's branch, its info is present in .git folder. This command will throw error as current local working branch is not linked to any of the UPSTREAM'S REMOTE BRANCH.
git push origin main ==> OR git push UPSTREAM REMOTE_BRANCH means that on whatever current local branch we are currently on, if we will run this command, we will push local commits of this branch to origin's(or any mentioned upstream) REMOTE_BRANCH. If that remote_branch is not present on remote repo, then it will be created. Hence, WE CAN PUSH FROM ANY LOCAL BRANCH TO ANY REMOTE BRANCH.
"git push" is the short hand method for "git push UPSTREAM REMOTE_BRANCH", where UPSTREAM AND REMOTE_BRANCH value is previously set using "git push -u origin main". 
git branch -u|--set-upstream[-to]=UPSTREAM_ALIAS/REMOTE_BRANCH ==> We can also set just the upstream of any local branch without waiting for anything to push.
git branch -u upstream_alias [other branch_name OR same local branch name same on remote (DEFAULT) ]

git branch --unset-upstream     ==> to unset the remote tracking branch from the local branch

git checkout newBranchName  ==> switches to that branch iff the branch exists, else gives error
git checkout -b newBranchName   ==> creates new branch IFF there is no pre-existing branch with same name. In such case, gives error, and doesn't even switch to that new branch which is laready present
git checkout -      ==> switch to previous checkout branch|detached_head_state
git branch -d|-D branchToDelete ==> deletes branch locally
git branch -M [old branch name] new_branchName
git branch --all|-a [-v] ==> shows all the branch [with the last commit ID and message]

git push
git push origin
git push origin master  ==> push changes from current branch to master branch of remote repo.
git push origin HEAD    ==> HEAD points to current branch where head points to. Hence push on remote branch whose name is same as branch where HEAD is currently pointing to.
git push origin :   ==> push to remote branch whose name is same as current local branch name.
git push origin HEAD:master     ==> push from HEAD or any_other_local_branch_name to master branch of remote repo.
git push origin :branch_to_delete   ==> delete the remote branch branch_to_delete on remote repo.

local working tree <=> local staged area <=> local commi tree <=> version control system hosts like Github, gitlab, bitbucket, etc.

Cloning already created remote repo will link the locally cloned repo to remote repo, with PULL and FETCH alias name as "origin" by default. Now we know how to change the alias name, the PULL or FETCH tracking URLs.

PR can be raised from any branch to any any branch of the project.
Once PR is raised, then till the time it is opened, every commit/changes made on that branch will be part of the PR, even if PR is raised from forked repo. Hence, it is advised to keep separate branch just for raising PR itself. Also, if more than 1 PR need to be raised, raise it from separate branch for separate PRs.

git config --global user.name="sharan jaiswal"
git config --global user.email="sharanjaiswal12@gmail.com"
git config --global --list  ==> sort of loists the contents of the git.config file
git config --global --edit  ==> this will open the editor to edit the git.config file

git branch VS git branch -v VS git branch -vv VS git branch -vv --all   ==> increasing order of information

git remote     ==> o/p just the current branch name alias, eg "origin"
git remote -v   ==> lists out the all the branches alias, their upstream tracking url, each for FETCH and PUSH
git remote add UPSTREAM_NAME URL
git remote remove UPSTREAM_NAME
git remote rename OLD_UPSTREAM_NAME NEW_UPSTREAM_NAME
git remote set-url UPSTREAM_NAME new_url <old_url>
git remote set-url --add|--delete UPSTREAM_NAME URL ==> to add more than 1 push URLs. So, while pushing any changes to this upstream, the changes will get pushed to all the push-upstreams, skipping all the upstreams URLs giving errors.

git clone HTTP_URL.git [local name of the clonned repo if we want some different name locally]

git status [--long(DEFAULT) | --short]  ==> by default --long is implicitly called. --short is used when we know what to do w/o hints, and that too with symbols. Symbols are prepended before files and their versions at every stage when --short is used. ??-untracked, A-added, D-deleted, M-modified, green-staged, red-unstaged

git restore --staged fileName ==> to remove file(s) from staging area to local working tree.
git reset COMMIT_ID [filename] ==> puts all the changes in the local working tree as unstaged changes, made after given commit_id. Hence, if commit tree is like latest_id <- second_latest_id , and we provide second last commit id to reset, then all changes made after second last commit ID will be in the unstaged area.
git restore filename ==> to restore the file currently in working tree, i.e. unstaged changed file in working tree which is already being tracked by git, to last comitted version of file. If file is untracked, then there will be error stating that the file is untracked and is not known by git.

git reset HEAD filename ==> Suppose we have deleted a file and added that information on the staging area. To restore that file, we first run this command to bring all the changes done after HEAD back to local working directory. But this didn't restore deleted file, just updated the deleted status to non-deleted status. 
git checkout -- filename ==> to bring back the deleted file, i.e., restore the file with its contents as per like it was in the last comitted version of reset. Remember this will not work if the file is not tracked by the git. Tracked deleted files will not be recovered unless checkout is used.

git checkout [HEAD(default)|commit_id] filename     ==> If a file's version is present in mentioned HEAD or commit_id provided, then any changes made to the file in local working tree or staging area or its any version after that mentioned commit will be gone and mentioned commit_id version of file will be now present in the working tree. To persist this version, we need to commit it again with this change.

git checkout [HEAD(default)|commit_id]  ==> If HEAD is not mentioned and any other commit ID is mentioned, then state of local working tree will be in state same as of mentioned commit_id. In a way, this will be READ_ONLY mode, ie, detached HEAD state where we have moved out from the current branch. Changes made in local working tree of the brach from where we came, will be kept away for time being and are not gone. We can do and commit changes to this detached head state but these changes are not happening on any branch. Moreover, once we checkout to another branch, we can only switch|checkout to commit of detached head state only if we will have the commit ID made on detached head state. So, to retain this detached head state, we need to make new branch. Already made commits will be now part of this branch, OR we can first make branch after moving to detached head state and then try to put commits on this new branch. Later we can merge|rebase this detached head version branch changes to any required branch.

git switch -    ==> after git checkout <some>, to go back to previous state after just coming into detached-head state

Suppose, we added|pushed non-required new commits to the opened PR, and now we want to remove few commits from top, or we want to remove few commits from in between latest and some_commit_id (from which all commits before it will be present, eg. latest_commit <- 2_commit <- . . . <- some_commit <- . . .); we can do "git reset some_commit". Now that we have moved changes after some_commit to local unstaged area, we can simply either force push this, or can add new commits after some_commit to local commit tree and force push this. This will update the commit tree of the remote branch on which it is pushed with this new local commit tree. This can also update commits in opened PR.
git push UPSTREAM BRANCH --force-with-lease |--force

Why do we add multiple remotes?
Situation: One remote for the actual open-sourced project, aka upstream. One remote for forked repo of the same. There are cases where forked remote repo does not automatically keeps it updated on remote from the original project repo. This might make forked remote repo outdated if few commits are added to OG project rmt repo. In such cases, on local, we can pull changes from upstream to locally cloned forked repo, and then push it with our changes to forked remote repo. Then create a PR so that forked remote repo will be at least up-to-date or ahead with the OD project remote repo. WAY: 1: git pull upstream OG_PROJ_MAIN_BRANCH_NAME  ==> git push origin main (pusing on remote forked repo's branch)
WAY: 2:   git fetch --all --prune ==> git reset --hard upstream/OG_PROJ_MAIN_BRANCH_NAME ==> git push origin main (pusing on remote forked repo's branch)

SQASH commits: 4<-3<-2<-1<-previous_stable_commits Now if we want to combine >1 commits(4,3,2) to single commit(1), we need to rebase commits.
git rebase -i previous_stable_commits ==> opens interactive rebase terminal. Instead of "pick" we need to replace word with "s" on commits (2,3,4) so that 1,2,3,4 will be merged to commit id (1). Press ":x" w/o quotes to goto terminal to provide new_commit_message. Now >> new_commit_message<-previous_stable_commits. Push or force push this new commit tree.

git rebase NEW_BASE_BRANCH [|BRANCH_TO_MOVE|CURRENT_BRANCH] ==> moves all the sequence of commits which are seemed to branched out from NEW_BASE branch, even if some intermediate commits are present on some intermediate branched out branches. In past commit histories of both branch in context, they should seem like they sharing at least one common commit, else all commits will be rebased on NEW_BASE_BRANCH
git rebase --continue ==> for moving forward in rebase operation
git rebase --abort  ==> stop rebasing, and bring back state of working directory as if no rebase cmd was triggered.
git rebase --onto NEW_BASE CHILD_BRANCH GRAND_CHILD_BRANCH ==> Instead of moving all the commits which seems to diverge from NEW_BASE_CHILD branch to GRAND_CHILD_BRANCH, we move those commits on GRAND_CHILD branch which are only diverged from CHILD_BRANCH towards GRAND_CHILD branch. Rebasing them on NEW_BASE branch.
git rebase HEAD~5 HEAD~3 HEAD   ==> On a given branch, rebase happens in such a way that last 3 commits are put upon 6th last commit, skipping 5th and 4th commit. These can be useful when assuming last 4th and 5ht commits were stale or non-required

git mv old_name new_name ==> to rename the tracked file so that git gets aware about the name change or location change of the file. Simple unix "mv" will make git consider that old_name fie has been deleted and new_name file has been added, not considering that it has been mere renamed. So, to update the git tracker that just renaming has happened, and nothing else.
git add -u ==> to keep git tracker up to date with the changes that has been made.

git add --ignore-removal files|path|.   ==> stages changes made in the working tree but not anything that has been deleted

git config --global alias.ALIAS_NAME "git log --abbrev-commit --all --oneline --decorate --graph -n 10 --stat --grep="msg pattern"      ==> git ALIAS_NAME will execute the command in quotes
git config --global --unset alias.ALIAS_NAME
git config --global --unset-all alias.ALIAS_NAME

git log SHA_LATER[...SHA_OLDER]   ==> commits b/n both SHA
git log HEAD..origin/branch_name    ==> useful when we want to compare HEAD with the fetched changes

git diff[tool] [filename] ==> difference between local working tree vs changes in stage
git diff[tool] HEAD [filename]  ==> difference between local working tree vs changes where HEAD is pointing to. Instead of HEAD we can provide the commit ID also.
git diff[tool] --staged|cached [filename]  ==> difference between staging area vs changes where HEAD is pointing to. Instead of HEAD we can provide the commit ID also.
git diff[tool] HEAD|SHA1 SHA2|HEAD  ==> comparing 2 SHAs
git diff[tool] upstream1/rmt_branch_x upstream2/rmt_branch_y    ==> we can simpe give any local branch as well. We can pass only one param as well, but in such case local current branch working directory will be comapred with that param. If we just provide rmt_branch_P w/o upstream_Q, then that branch will be considered as local branch and not remote branch.
git diff[tool] HEAD HEAD^   ==> what changes has been made in second last commit(HEAD-1) while comparing it with the latest commit(HEAD). Its like reverse comparison.
git diff[tool] local_branch remote_upstream/local_branch    ==> In local machine, remote_local_branch reference will be always equal to or lag behind its version of local_branch. But to compare what has ben updated on remote, do git fetch and then run this command. Then it will show what changes has been made to remote when compared with local branch version of it.
git diff[tool] -- path/to/file  ==> If we want to compare unstaged modified file with its last comitted version. We put "--" because there was no other switch|option we provided after diff[tool], and if if we need to provide filename, then we need to put "--".
git diff[tool] origin[/CURRENT_BRANCH|other_branch]   ==> compare unstaged local changes with the origin|fetched_changes

git fetch --all --prune ==> to pull ALL the info INCLUDING all the newly branch created and deleted branch references

It is a good practice to do diff check before accepting any incoming changes from any source(branch, remote, etc.). For that, use below:
git fetch UPSTREAM/BRANCH_NAME ==>> git diff origin[/CURRENT_BRANCH|other_branch]   ==>> git merge origin[/CURRENT_BRANCH|other_branch]             <<<<<<=======>>>>>>     git pull origin [/CURRENT_BRANCH|other_branch]

git merge some_feature_branch    ==> In case where some_feature_branch is branched out from parent and parent doesn't has any commits hence child branched. This will merge the some_feature_branch all commits after the branching, to the parent, maintaining the commit sequence and their IDs. This is called fast forward merge where commits sequence are maintained in the branch where they are merged. Actually, parent's reference moved to the latest commit of some_feature_branch giving feel that both(parent and child_feature) are pointing to same latest commit ID of child.
In cases, where parent has some commits after some_feature_branch is branched out and has few commits of its own. In such cases, while merging, recursive-merge approach is followed where changes from all commits from feature after it has been branched out of parent are consolidated into one single commit and applied as a new single merge commit on the parent.
git merge --no-ff some_feature-branch   ==> In any case, even if fast-forward merge is possible, creates a consolidated merge commit.
git merge --ff some_feature-branch   ==> prefer ff over single merge commit wherever possible.
git merge --ff-only some_feature-branch   ==> Merge changes only when ff is possible. If single-merge commit is about to happen, abort it.
git merge feature_branch --squash   ==> do not commit the merge changes but put the incoming merge changes into the staging area, probably to review.
git merge feature_branch --no-commit   ==> do not commit the merge changes but put the incoming merge changes into the staging area, probably to review.

Never do rebase of the branch which has and can be accessed by other developers because rebasing changes the commits SHAs in such way that each commits are re-commited over new base with new commit IDs. Moreover, when each commits are re-commited, chances of merge conflicts can happen for each commits and not just for the final commit. So, lots of rework. Changing hash might change and break the commit history of other devs who are working on the same branch or who access the rebased branch.

git pull --rebase[=false|true|merges|interactive] [UPSTREAM] [UP_BRANCH]   ==> do the rebase while pulling the changes. AVOID REBASING.
git pull --ff-only [UPSTREAM] [UP_BRANCH]  ==> happens by default, pulls changes only when local commits are not divergent from the incoming changes
git pull --ff [UPSTREAM] [UP_BRANCH]   ==> do fast-forward merge if possible, ie when local is not divergent from the incoming changes which eventually just moves the head to the latest incoming commit; Else make one merge commit merging all divergent changes
git pull --no-ff [UPSTREAM] [UP_BRANCH]    ==> In any case, even if fast-forward merge is possible, create a merge commit.
git pull --squash [UPSTREAM] [UP_BRANCH]    ==> DO NOT commit the changes but put them in staging area.

NOTE: git doesn't allow checkout if working directory has changes in tracked file. But will allow and move those changes to checkout place if changes are made in untracked files ONLY.
git stash [-u]  ==> including staged and untracked files and default save msg as last commit id and msg
git stash --keep-index  ==> stash only from working directory, NOIT from staging area
git stash [-u] save "msg"    ==> custom msg
git stash apply|pop [stash@{N}] ==> specifically apply Nth stash only, w/o applying stashed changes after Nth stash
git stash list [-u|-p] ==> DO NOT use -u|-p as it optputs the changed contents also
git stash show -u|-p stash@{N}  ==> -p outputs the contents as well
git stash drop [stash@{N}]
git stash clear
git stash branch branch-name [stash@{N}]

git cherry-pick commit_id   ==> copy the commit status of commit_id and put as new latest commit on current branch
git cherry-pick commit_id --no-commit|-n    ==> put the changes in staging area, but doesn't makes a new commit. Probably for review
git cherry-pick oldest_commit_id some_middle_commit_id new_commit_id    ==> to bring all these commits. Hence, we can also cherry pick more than one commits
git cherry-pick old_commit^ new_commit  ==> NOTE that we have used caret over old_commit_id. This moves all the changes between old and new commit IDs, both inclusive, to the current branch
git cherry-pick old_commit_id new_commit_id ==> copies all the changes MADE AFTER old_commit_id and including new commit id, to the current branch
GIT CHERRY PICK is like rebase, so conflicts may arise

git commit --amend --no-edit    ==> make changes to the last commit with no changes in the commit msg
git commit --amend -m "msg"     ==> make changes to the last commit with new commit msg

git reset [--mixed(def->in WD)|--soft(in stage)| --hard(deletes henceforth changes))] HEAD|commit_id [file(NOT w/ --hard)]
git clean   ==> git hard reset only resets the tracked files. To remove the untracked files, run this cmd

git revert older_commit_id  ==> removes the changes made in that particular commit and commits it as new commit. This way, unlike reset, it doesn't change the commit history. Merge conflicts mat arise.
git revert older_commit_inclusive newer_commit_exclusive    ==> between including older to commit just before newer, changes will be removed, merge conflicts will be asked to solved, if any, and single new commit with removed changes will be made.