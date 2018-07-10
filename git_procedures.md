## Git repositories HOW TO


#### Pull requests


1. Checkout master branch and pull  `git checkout master` `git pull` 
1. Checkout your branch (and pull)  `git checkout pr-branch` `git pull` 
1. Find id of the first commit from your branch (let's call it `squash_commit_id`) `git log master..pr-branch --oneline | tail -1`
1. Run interactive squash: `git rebase -i squash_commit_id`. Git opens an editor allowing
for interactive commit squash.  
1. Pick `squash` command for all the commits other than our `squash_commit_id`. 
Save the file and close the editor.
1. Another editor opens, and allows us to pick new message for our suqashed commit. 
You may copy the name from the pull request title, then provide pull request id and fixed issues ids - 
remember hashtags huh? `#111`. Save the file and close the editor.
1. Rebase your branch on top of master branch `git rebase master`
1. Open your favorite IDE and resolve conflicts. Do not commit. 
In RubyMine you simply select a project, right click on it and go to `Git>Resolve Conflicts`
1. Finish rebase by typing `git rebase --continue`
1. Force push your new branch with the beutifully squashed commit `git push -f`
1. Congratulations! As soon as the Travis-CI build finishes the build yo are ready to merge 
by clicking `Rebase and merge` in GitHub