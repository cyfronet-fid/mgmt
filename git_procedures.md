## Git repositories HOW TO

#### Pull request procedure
1. Create Pull Request
1. Organize your commit messages by squashing unnecessary commit stages. Rewrite misleading messages
1. Resolve conflicts if they appear (you may avoid them/prepare to resolve them 
earlier if you rebase to the master branch first)
1. Wait for Travis-CI to build your Pull Request. 
Travis will emulate merge before it happens and build merged code (see 
[details](https://docs.travis-ci.com/user/pull-requests/#How-Pull-Requests-are-Built))
1. Merge your branch into master branch


#### Rebasing branches to master branch

1. Checkout master branch and pull  `git checkout master` `git pull` 
1. Checkout your branch (and pull)  `git checkout pr_branch` `git pull` 
1. Rebase your branch on top of master branch `git rebase master`
1. Open your favorite IDE and resolve conflicts. Do not commit. 
In RubyMine you simply select a project, right click on it and go to `Git>Resolve Conflicts`
1. Finish rebase by typing `git rebase --continue`
1. Force push your new branch with the beutifully squashed commit `git push --force-with-lease `

#### Squashing commits 

1. Checkout your branch (and pull)  `git checkout pr_branch` `git pull` 
1. Find id of the first commit from your branch (let's call it `squash_commit_id`) `git merge-base master HEAD`
 or  `git merge-base master pr_branch`
1. Run interactive squash: `git rebase -i squash_commit_id`. Git opens an editor allowing
for interactive commit squash.  
1. Pick `squash` command for all the commits you want to merge with a preceding, 
leave `pick` for the ones you want to leave as they are. 
Save the file and close the editor.
1. Another editor opens, and allows us to pick new message for our suqashed commit. 
Save the file and close the editor.

##### Useful information

1. Shorthand for rabase in merge base 
> git rebase -i \`git merge-base master HEAD\` 
2. Aborting rebase
> git rebase --abort


