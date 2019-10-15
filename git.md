### <a name="development"></a>Development

1. Create a new branch from **base branch** (`master`) and name it  `<ticket id>-<your branch name>`
1. Do your development and write `CHANGELOG.md` entry
1. Create Pull Request
   * Describe your changes. Use magic tags like `fixes <ticket id>`
   * If your work is in progress create
     [draft PR](https://github.blog/2019-02-14-introducing-draft-pull-requests/)
   * If your work is done convert draft PR to ready to review PR
   * Wait for 2 approvals in review (1 dev and product owner)
1. Merge changes to the **base branch**

### <a name="release"></a>Release

1. When changes in the **base branch** (`master`) are ready to be released _@wojt_
   creates branch version `<a>.<b>.0` originating form the `master` branch. This
   branch is called **release candidate branch**.
1. Into the **base branch** branch next development features can be merged
   (these changes will not be release in described release).
1. **release candidate branch** is automatically build and can be used to test release candidate
1. When some problems are discovered in **release candidate branch** fixes are
   done similar like described in [Fixes Development](#fixes-development) section
   with one modification: **base branch** is `<a>.<b>.0`.
1. When everyting is OK, _@wojt_ runs script/github action which is performing following steps:
   * Unreleased section header is renamed into `[<a>.<b>.0] <release_date>`.
     This change is commited to `<a>.<b>.0` branch with `<a>.<b>.0 release` message.
   * An appropriate `<a>.<b>.0` tag is added for last commit in `<a>.<b>.0` branch
   * github `<a>.<b>.0` release is creted via github API
   * `Unreleased` template is added to `CHANGELOG.md`. This change is commited to
     `<a>.<b>.0` branch with `Next development cycle` message.
   * Pull Request from `<a>.<b>.0` branch to `master` is created
   * Notification about new release is sent to email/slack/etc.
1. The _Developer_ resolves conflicts and merges `<a>.<b>.0` to `master` (watching `CHANGELOG.md`)
1. `<a>.<b>.0` branch is removed from github

### Production deployment

Access to `production` branch is restricted to **release owners** (_@wojt_, _@bwilk_)

There is script/github action which takes as a argument `<a>.<b>.<c>` tag name
and perform following steps:

1. `production` branch is switched to `<a>.<b>.<c>` tag and pushed to github
1. `production` branch is deployed to production
1. All lower branches than selected are removed from github (e.g. when `1.2.3`
   is releases `1.0.x` and `1.1.x` are removed but not `1.2.x`)
1. Notification about new deploy is sent to email/slack/etc.

### Fixes

#### <a name="fixes-development"></a>Development

Fixes Pull Requests should be done similar like
[normal development](#development) with following modifications:

* **base branch** is `<a>.<b>.x`. This branch can already exist in github or
  should be created by the developer from `<a>.<b>.0` tag
  (`git branch -b v<a>.<b>.0`).

#### Release

Fix release is following basically the same set of rules that
[Resease](#release) phase with following modifications:

1. **release candidate branch** is `<a>.<b>.x`.
1. When a release is performed by the script `<a>.<b>.<c>`  tag is created
   (`<c>` is `<pre-c + 1>` calculated from latest `<a>.<b>.<prev-c>` tag)
1. `<a>.<b>.x` is **not** removed until next feature ritch version is not pushed
   to production.

