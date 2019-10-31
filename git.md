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
   creates branch version `<a>.<b>.x` originating form the `master` branch. This
   branch is called **release candidate branch**.
1. Into the **base branch** branch next development features can be merged
   (these changes will not be release in described release).
1. **release candidate branch** is automatically build and can be used to test release candidate
1. When some problems are discovered in **release candidate branch** fixes are
   done similar like described in [Fixes Development](#fixes-development) section.
1. When everyting is OK, _@wojt_ runs script/github action which is performing following steps:
   * **Version** is calculated using following algorithm:
     * Find all tags with following pattern `<a>.<b>.<anything>`
     * If no maching branch is found version is set to `<a>.<b>.0`
     * If maching branches are found version is set to `<a>.<b>.<MAX(anything) + 1>`
   * Unreleased section header in `CHANGELOG.md` is renamed into
    `[<version>] <release_date>`, content of `VERSION` file is changed to
    **version**. These changes are commited to `<a>.<b>.x` branch with `<version> release` message.
   * An appropriate `<version>` tag is added for last commit in `<a>.<b>.x` branch
   * github `<version>` release is creted via github API
   * `Unreleased` template is added to `CHANGELOG.md`. This change is commited to
     `<a>.<b>.x` branch with `Next development cycle` message.
   * Pull Request from `<a>.<b>.x` branch to `master` is created
   * Notification about new release is sent to email/slack/etc.
1. The _Developer_ resolves conflicts and merges `<a>.<b>.x` to `master` (watching `CHANGELOG.md`)
1. `<a>.<b>.x` branch is **not** removed from github

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

