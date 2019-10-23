# Process of development
## Our board
The main goal is to clean up column Sprint goal and in progress!!
Firstly please take tickets from Sprint Goal column if there are any unassigned!


### Column Sprint Goal

The main sprint goals are listed at the top of the "Sprint goals" column on planing.
Goal is to move all tickets from column 'Sprint Goal' to 'Done'.
At the very beginning of the sprint we get at least one ticket which describes the problem to be solved.
Tickets with hotfixes will also be added to this column.

### Column Backlog

Additional tickets to take if sprint goals are achieved. In the backlog we can find tasks with lower priority than the sprint goal - prepared for the team by PO. They come from the development team (created during retro, and in the normal course of the sprint as new issues, prioritized by PO), and from business analysis - (addressed by PO in the tool evolution plan or requested by external parties).


### Column In Progress

This column contains all tickets in progress and pr-s to review.
Pull requests will automatically move here when added to this project.
If a closed pull request in this project reopens, it will automatically move here.


### Column Done

Only merged pr-s, closed tickets


## Tickets
Tickets are fully described cases to solve in this Sprint with pipeline "Ready for Dev"

1. dividing ticket into bullets (write in the comment to the main ticket as list of checks or create new ticket). It is not necessary if ticket is too small then go to 4.
2. If its necessary create ticket to bullet otherwise draft-pr (Bullet can be presented by ticket or draft PR. It means, if we starts working on the bullet then we must create PR in draft mode or ticket)
3. Write ticket or Pr hash next to bullet (In Bullet list we have to write ticket hash or PR hash next to the bullet being prepared). If there is no hash that's mean ticket isn't in progress!
4. Solve the bullet
5. Close bullet
 - ticket -> create PR and add reviewers
 - draft PR -> set to open and add reviewers (**!Each PR must have at least one programmer reviewer and one manual tester (Roksana, Aga, Lidia)!**)
6. Wait for review,if after two days you don't get a response, report it on the meeting
7. Resolve comments and wait for approve
8. Pr-branch must be rebased to base branch before merge. If there are conflicts you can ask for re-review but isn't necessary.
9. Merge branch (**!At least one programmer and one manual tester have to approve PR to be merged!**)
10. Delete merged branch
11. !Check bullet in base ticket!
12. Base ticket can be closed if all the technical tasks have been completed. Otherwise they must be documented by the development team as separate tickets for the future developments.


### Hot Fixes
Bugs in production have the highest priority if management team does not say otherwise.


### Bullets

On meetings, Dev team divide Sprint goals into bullets as good as possible, but developer can divide bullet if it's necessary.
Bullets list can be created in separate ticket or in comment to main ticket.
Bullet is not a divisible part of problem connected to ticket or draft pr.
One PR per bullet.
Ticket can be connected to many PRs.


### Reporting lack of review
If your PR is not checked for two days, please report it to daily and make sure that someone comes to this task.


## ToDO
hotfix (label or column)?
template issues and pr
What if we not met Sprint goal?
