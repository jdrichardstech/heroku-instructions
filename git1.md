4. Getting changes from a server - git pull
   If you make updates to your repository, people can download your changes with a single command - pull:

\$ git pull origin master

From https://github.com/tutorialzine/awesome-project

- branch master -> FETCH_HEAD
  Already up-to-date.
  Since nobody else has commited since we cloned, there weren't any changes to download.

branches\_.jpg
Branches
When developing a new feature, it is considered a good practice to work on a copy of the original project, called a branch. Branches have their own history and isolate their changes from one another, until you decide to merge them back together. This is done for a couple of reasons:

An already working, stable version of the code won't be broken.
Many features can be safely developed at once by different people.
Developers can work on their own branch, without the risk of their codebase changing due to someone else's work.
When unsure what's best, multiple versions of the same feature can be developed on separate branches and then compared.

1. Creating new branches - git branch
   The default branch of every repository is called master. To create additional branches use the git branch <name> command:

\$ git branch amazing_new_feature
This just creates the new branch, which at this point is exactly the same as our master.

2. Switching branches - git checkout
   Now, when we run git branch, we will see there are two options available:

\$ git branch
amazing_new_feature

- master
  Master is the current branch and is marked with an asterisk. However, we want to work on our new amazing features, so we need to switch to the other branch. This is done with the git checkout command, expecting one parameter - the branch to switch to.

\$ git checkout amazing_new_feature

3. Merging branches - git merge
   Our "amazing new feature" is going to be just another text file called feature.txt. We will create it, add it, and commit it.

$ git add feature.txt
$ git commit -m "New feature complete."
The new feature is complete, we can go back to the master branch.

Delete a branch on github:
-- On GitHub, navigate to the main page of the repository.
-- Above the list of files, click NUMBER branches.
-- Scroll to the branch that you want to delete, then click .

You will still need to delete it from your computer though.

\$ git checkout master
Now, if we open our project in the file browser, we'll notice that feature.txt has disappeared. That's because we are back in the master branch, and here feature.txt was never created. To bring it in, we need to git merge the two branches together, applying the changes done in amazing_new_feature to the main version of the project.

git merge amazing_new_feature
The master branch is now up to date. The awesome_new_feature branch is no longer needed and can be removed.

git branch -d amazing_new_feature
advanced.png
Advanced
In the last section of this tutorial, we are going to take a look at some more advanced techniques that are very likely to come in handy.

1. Checking difference between commits
   Every commit has it's unique id in the form of a string of numbers and symbols. To see a list of all commits and their ids we can use git log:

\$ git log

commit ba25c0ff30e1b2f0259157b42b9f8f5d174d80d7
Author: Tutorialzine
Date: Mon May 30 17:15:28 2016 +0300

    New feature complete

commit b10cc1238e355c02a044ef9f9860811ff605c9b4
Author: Tutorialzine
Date: Mon May 30 16:30:04 2016 +0300

    Added content to hello.txt

commit 09bd8cc171d7084e78e4d118a2346b7487dca059
Author: Tutorialzine
Date: Sat May 28 17:52:14 2016 +0300

    Initial commit

As you can see the ids are really long, but when working with them it's not necessary to copy the whole thing - the first several symbols are usually enough.
To see what was new in a commit we can run git show [commit]:

\$ git show b10cc123

commit b10cc1238e355c02a044ef9f9860811ff605c9b4
Author: Tutorialzine
Date: Mon May 30 16:30:04 2016 +0300

    Added content to hello.txt

diff --git a/hello.txt b/hello.txt
index e69de29..b546a21 100644
--- a/hello.txt
+++ b/hello.txt
@@ -0,0 +1 @@
+Nice weather today, isn't it?
To see the difference between any two commits we can use git diff with the [commit-from]..[commit-to] syntax:

\$ git diff 09bd8cc..ba25c0ff

diff --git a/feature.txt b/feature.txt
new file mode 100644
index 0000000..e69de29
diff --git a/hello.txt b/hello.txt
index e69de29..b546a21 100644
--- a/hello.txt
+++ b/hello.txt
@@ -0,0 +1 @@
+Nice weather today, isn't it?
We've compared the first commit to the last one, so we see all the changes that have ever been made. Usually it's easier to do this using the git difftool command which brings up a graphical client showing all differences side-to-side.

2.Reverting a file to a previous version
Git allows us to return any selected file back to the way it was in a certain commit. This is done via the familiar git checkout command, which we used earlier to switch branches, but can also be used to swtich between commits (it's pretty common in Git for one command to be used for multiple seemingly unrelated tasks).

In the following example we will take hello.txt and reverse everything we've done to it since the initial commit. To do so we have to supply the id of the commit we want to go back to, as well as the full path to our file.

\$ git checkout 09bd8cc1 hello.txt

3. Fixing a commit
   If you notice that you've made a typo in your commit message, or you've forgotten to add a file and you see right after you commit, you can easily fix this with git commit --amend. This will add everything from the last commit back to the staging area, and attempt to make a new commit. This gives you a chance to fix your commit message or add more files to the staging area.

For more complex fixes that aren't in the last commit (or if you've pushed your changes already), you've got to use git revert. This will take all the changes that a commit has introduced, reverse them, and create a new commit that is the exact opposite.

The newest commit can be accessed by the HEAD alias.

\$ git revert HEAD
For other commits it's best to use an id.

\$ git revert b10cc123
When reverting older commits, keep in mind that merge conflicts are very likely to appear. This happens when a file has been altered by another more recent commit, and now Git cannot find the right lines to revert, since they aren't there anymore.

4. Resolving Merge Conflicts
   Apart from the scenario depicted in the previous point, conflicts regularly appear when merging branches or pulling someone else's work. Sometimes conflicts are handled automatically by git, but other times the person dealing with them has to decide (and usually handpick) what code stays and what is removed.

Let's look at an example where we're trying to merge two branches called john_branch and tim_branch. Both John and Tim are writing in the same file a function that displays all the elements in an array.

John is using a for loop:

// Use a for loop to console.log contents.
for(var i=0; i<arr.length; i++) {
console.log(arr[i]);
}
Tim prefers forEach:

// Use forEach to console.log contents.
arr.forEach(function(item) {
console.log(item);
});
They both commit their code on their respective branch. Now if they try to merge the two branches they will see the following error message:

\$ git merge tim_branch

Auto-merging print_array.js
CONFLICT (content): Merge conflict in print_array.js
Automatic merge failed; fix conflicts and then commit the result.
Git wasn't able to merge the branches automatically, so now it's up to the devs to manually resolve the conflict. If they open the file where the conflict resides, they'll see that Git has inserted a marker on the conflicting lines.

<<<<<<< HEAD
// Use a for loop to console.log contents.
for(var i=0; i<arr.length; i++) {
console.log(arr[i]);
}
=======
// Use forEach to console.log contents.
arr.forEach(function(item) {
console.log(item);
});

> > > > > > > Tim's commit.
> > > > > > > Above the ===== we have the current HEAD commit, and below the conflicting one. This way we can clearly see the differences, and decide which is the better version, or write a new one all together. In this situation we go for the latter and rewrite the whole thing, removing the markers to let Git know we're done.

// Not using for loop or forEach.
// Use Array.toString() to console.log contents.
console.log(arr.toString());
When everything is set, a merge commit has to be done to finish the process.

$ git add -A
$ git commit -m "Array printing conflict resolved."
As you can see this process is quite tiresome and can get extremely hard to deal with in large projects. Most developers prefer to resolve conflicts with the help of a GUI client, which makes things much easier. To run a graphical client use git mergetool.
