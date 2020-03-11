Setup username and email in terminal
`git config --global user.name "My Name"`
`git config --global user.email myEmail@example.com`

`git log` is a way of looking out our commits
`git log --oneline` allows us to see the id and commit in a single line without the other metadata.

Undoing things
(in order of danger)
GIT CHECKOUT

git config --list look for email username
git config --global user.name '<username>'
git config --global user.email '<email>'
when this is configured every time you do something in git it is stamped with your info

1. `git checkout` allows us to look back at a past commit without changing anything.
2. So if you wanted to see how something looked you could
   `git log --oneline`
3. choose a commit number then type
   `git checkout <idNumber>`
4. When you are done you can simply type
   `git checkout master` and it will return you to the top of the stack.
   You already know master I think but master is the head branch.

GIT REVERT
git revert undoes one commit

checkout commit
revert commit
reset commit

git log - shows all of your commits
git commit --amend -m "message here" this will fix if you incorrectly typed the last message you typed.

git revert HEAD (reverts the newest commit)

git revert b10cc123 reverts based on id

git branch
git branch -d name-of-branch

git checkout
branch
push to branch not master

git amend -m '<new message>' amends commit message

git log (press q at the end to exit)
git log --oneline
git shortlog -10

git pull origin master
git pull origin branchname

git remote remove origin

rm -rf .git

git merge name of branch
then git status
git commit....

git show any-part-of-id (after you have done a git log)

git diff one-id..other-id

git fetch origin <name of branch>

GITHUB IN THE BROWSER ACCOUNT
merging
add contributor ---- settings on left...manage access contributors in regular accounts have all permissions
issues
pull request-- on web you can push a branch and then do pull from site
merge conflicts
setting merge rules in settings...branches ---- remember to name it asterisk master asterisk to apply to master or whatever branch
show review before merge.
set to 1 review
show merge override
create a conflict
show accept all
show remove the stuff and keeping the code you want then recommitting.

- change same thing on master and commit but DONT push and then on a branch commit don't push. then try to merge branch to master
- after you will abort
- do it again
- this time commit again and merge
- delete branch

how to review
Under your repository name, click Pull requests.
In the list of pull requests, click the pull request you'd like to review.
On the pull request, click Files changed.
Hover over the line of code where you'd like to add a comment, and click the blue comment icon. ...
In the comment field, type your comment.

GIT WORKFLOWS 4 of them
Centralized Workflow
Feature Branch Workflow
Gitflow Workflow
Forking Workflow

RESET
This usage of git reset is a simple way to undo changes that haven’t been shared with anyone else. It’s your go-to command when you’ve started working on a feature and find yourself thinking, “Oh crap, what am I doing? I should just start over.”
git reset does alter the existing commit history.

REVERT
Reverting undoes a commit by creating a new commit. This is a safe way to undo changes, as it has no chance of re-writing the commit history.

RESOLVING DELTAS
Git uses delta encoding to store some of the objects in packfiles. However, you don't want to have to play back every single change ever on a given file in order to get the current version, so Git also has occasional snapshots of the file contents stored as well. "Resolving deltas" is the step that deals with making sure all of that stays consistent.
https://www.git-scm.com/book/en/v2/Git-Internals-Packfiles

Understanding how "checkout" works
With the "git checkout" command, you determine which revision of your project you want to work on. Git then places all of that revision's files in your working copy folder.

Normally, you use a branch name to communicate with "git checkout":

\$ git checkout development
However, you can also provide the SHA1 hash of a specific commit instead:

\$ git checkout 56a4e5c08
Note: checking out '56a4e5c08'.

You are in 'detached HEAD' state...
This exact state - when a specific commit is checked out instead of a branch - is what's called a "detached HEAD".
https://www.git-tower.com/learn/git/faq/detached-head-when-checkout-commit
