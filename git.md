### Development 

1. Create new branch from **base branch** (`master`) and name it  `<ticket id>-<your branch name>`
1. Do your development and write CHANGELOG.md entry 
1. Create Pull Request 
   * Describe your changes. Use magic tags like `fixes <ticket id>` 
   * If your work is in progress name PR `[WIP] <description>`
   * If your work is done name it `[<ticket_id>]  <description>`
   * Wait for 2 approvals in review (1 dev and product owner)
1. Merge changes to the **base branch** 

### Release 

1. When changes in the **base branch** (`master`) are ready to be released _@wojt_ creates branch version `<a>.<b>.x` originating form the **base branch**
1. _@wojt_ takes care of CHANGELOG.md entry in this branch (gives _Unreleased_ section appropriate version number)
1. _@wojt_ creates Pull Request to `production` branch 
   * we treat deployment of this branch as a test deployment for the release candidate 
1. Release is performed by _@wojt_
   * An appropriate `<a>.<b>.<c>` tag is added in `<a>.<b>.x` branch 
   * PR to `production` branch is merged when the released version is deployed to production
   
### Fixes 

Like Development and Resease but with following changes:

1. **Base branch** is `<a>.<b>.x`
1. When release is performed and tag `<a>.<b>.<c>` is created _@wojt_ creates a PR from `<a>.<b>.x` to `master`
1. Developer resolves conflicts and merges `<a>.<b>.x` to `master` (watching CHANGELOG.md)
