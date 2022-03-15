# Development Handbook


## General

* When building interface accessible by other apps/users, try stick to standards and schemas (e.g. swagger). Make the schemas discoverable, reference in README.md on oda-hub repositories.
* Follow [incident handling principles](https://github.com/oda-hub/doc-ops-reporting#incident-handling-principles) - in short, do not expect user issues to be left unattended, never.
* Do not be afraid to introduce large changes, but only if they respect previous interfaces

## Do not forget to!

we all do many things, but we should be conscious that some actions are needed for smooth progress of collective project.
Even though these actions may be delayed as necessary, it should be done with intent.
Too much notifications and distractions are detrimental to productivity, but one should aim keep some level of engagement.

It may be advisable to make sure all actions and channels converge to email. 

* on github check assigned issues, reviews, pull requests (this is all reflected in notifications, and other fields in the github page header)
* communicate by mattermost and slack

## About review order

* Note that if the PR is not draft, someone will need to select reviewers. 
* If the PR is made by an internal developer, only this developer will select the first reviewers. Other internal developers may suggest new reviewers.
* If The PR is made by an external developer - any relevant internal developer will select the reviewers.
* Until PR review is requested, review is not expected to follow. Some comments on in-progress code may be made, but with caution.
* It may happen that PR by  an internal reviewer is not in a draft state, but review is not requested. This intermediate stage awaits action from the internal developer. It's best not to keep PR in this form, since it's a bit ambiguous.

## Branches, Versions, Releases

### What did we use before and what's wrong with it

We used release branches for each version, like **production-V.V**. Any bugfixes were applied to these branches.
In addition, **staging-V.V** were used for ongoing developments in current version. Also, for previous versions, **staging-V.V** were used to preview updates before making them live.
This worked rather well.

On github, it is not convenient that current development is in the latest **staging-V.V** branch, whichever it happens to be at the moment. To reduce the uncertainty on what is the current version in development, we can just use the **master** branch for merging all new features.

We did current development is in the latest **staging-V.V** branch, whichever it happens to be at the moment. We remembered which one it was, since pace was slow, and people were few. But now it is becoming more difficult.

Previously, **staging-V.V** deployment was automatically updated to all recent **staging-V.V** component branches. However, some components evolved very little, and it was not useful to keep creating new identical branches - this introduced confusion, and was not sufficiently explicit.  With faster development, more components, and more branches this becomes really unfeasible. 

### Current strategy

To reduce the uncertainty on what is the current version in development, we can just use the **master** branch for merging all new features.

Once the development justifies the release, we create a **release-YY.MM** branch and a tag **v-YY.MM.PPPP**. Since this point, no developments will be introduced to the **YY.MM** version except for bugfixes. Every bug fix will yield in increase of the patch level (**PPPP** part).

Instead of **staging-V.V**, we will make a deployment for review from each PR. This is becoming possible with the new and improved k8s cluster.
In addition, we continue maintain the current development **staging** version of the platform, made from tip of the **master** branches of all components. This one will be similar to what we did so far with the latest **staging-V.V** version.

**This approach will go along with faster development rate, and will allow to roll-out features faster**.

* Note that this description applies first of all to the version entire platform, i.e. http://github.com/oda-hub/oda-chart.git, which contains (or will contain) references to the all of the  components. Versions of the individual components should also follow the **calver** scheme. But until referenced in oda-chart they will not be generally deployed. However, we may semi-automatically update oda-chart with updates of some components.

**NOTE**: we should [confirm](https://github.com/oda-hub/meetings/blob/main/2021-03-29/agenda.md) the calver approach, which was recently [suggested](https://github.com/oda-hub/meetings/blob/main/2021-03-22/minutes.md)

So far we have used [SemVer](https://semver.org/), ending up with 1.2 production and 1.3 planned release. However, we found that scope of the next planned version has been always shifting. This is not necessarily bad, but we take an opportunity of reorganizing development in new framework and more naturally adopt [CalVer](calver.org) and make releases regularly (at least yearly).  More frequent bugfixes will happen as necessary. This will be reflected in the version as so:

**YY.MM.PPPP**

where **YY** and **MM** correspond to the release month, and **PPPP** is an incremental bugfix/update level since the release.

for example, next release will be **21.05.000**.

CalVer will also clearly communicate pace of development, hopefully reduce hesitation in making the next significant release, and make the development more dynamic, matching the repeated requests of the users.

Releases will be made as soon as accumulated features are necessary, made into release branch from the master branch, and tagged.  
If a bugfix is necessary, a dedicated bugfix branch will be made and destroyed when bugfix version is tagged.

* use master for current stable staging version (i.e. no need for staging-1-3 etc), as deployed in UNIGE in staging (pre-release) environment. It may also experience quick bug-fixes, but not new running feature developments (feature branches are for that).
* for production, we still use release branches, e.g. production-1-2.
* use feature branches as necessary, in forks or in the base repository

## Hotfixes

Sometimes, an **urgent issue** is found in production. 
A **temporary change** will be introduced in a `hotfix` branch, which will be tested with existing tests, and hopefully new ones, and promptly deployed. 
This **temporary change** will be pushed on the repository for awareness, but **will not be merged**.

Any other development of the given component will not be merged until proper solution to **the issue** requiring `hotfix` is developed and merged.
After **the issue** is resolved and merged, `hotfix` branch will be deleted and forgotten.

## Github, Gitlab(s), etc?

We use github for common activities, as it is currently most easily discoverable space.
**UNIGE Platform is deployed with CI/CD from integral gitlab**, which is pushing changes with github.
It is also used for internal astro-only projects.

Currently, no repository has two (internal and external) version.
I.e. each project is either internal (and lives in gitlab.astro, e.g. product gallery) or external (much of MMODA)

## Github project management features: Labels, Milestones, Projects

We need multi-repository management, and we can use **milestones to mark planned release versions**.

In principle, both **labels** and **milestones** are per-repository, but even if they are created independently, they can be aggregated in organization if they are called the same way.

For v21.06 release, all issues can be seen here: [v21.06 issues](https://github.com/issues?q=is%3Aopen++user%3Aoda-hub+milestone%3Av21.06+).

Projects can be used to group and preview issues more nicely. [ODA Platform project](https://github.com/orgs/oda-hub/projects/1) shows all issues/PRs for the platform, and can be filtered [for v21.06 release](https://github.com/orgs/oda-hub/projects/1?card_filter_query=milestone%3Av21.06).

To avoid duplication, **milestones** can be seen as primary indication of the issue/PR assignment to the release, and **project** is a complementary presentation feature.

**Labels**, on the other hand, describe different aspects of issues (documentation, bug, etc). Details of the labels purpose should be put in the label descriptions.

### How to pick next issue to address?

In the order of importance:

* Implementation of any [hotfixes](https://github.com/issues?q=is%3Aopen+archived%3Afalse+label%3A%22hotfix%22++org%3Aoda-hub) (since they block regular development flow).
* With [high priority](https://github.com/issues?q=is%3Aopen+archived%3Afalse+label%3A%22high+priority%22++org%3Aoda-hub) label.
* Issues highlighted as important on a meeting. Ideally, anything decided on the meeting has to follow the other guidelines (assigned labels, milestones, etc). But - do keep in mind what was discussed. 
* Issues assigned the coming milestone.
* Finally, an additional factor in selecting between issues is what appears to be more clear. 

### Pull Requests vs Pushing commits to the Branch

Regularly, code should be contributed by creating a dedicated branch, followed by a pull request.
Pull requests allow the changes to be reviewed, allowing to introduce suggestions, and/or keeping other contributors aware of the code change.

In special cases, non-reviewed changes may be contributed by pushing directly to master:

* if the contribution is made by the principal developer, and other contributors have comparatively very little awareness on the code (as it is the case for much of the frontend components)
* if a simple and small change is change is made, and it is not worth dealing with review. The choice here should be made with caution, as perceptions of what is not worth reviewing may differ. This is almost never necessary.

Technically it is also possible to push commits on a branch (with an associated PR) made by another contributor. This should be avoided since it may confuse the author of the branch and prevents review.

## Dealing with Issues emerging in review and operations

once a problem is found by a reviewer, it goes through the following stages:

* **reviewer** creates github issue in some repository, at their discretion
* if necessary, **maintainer** moves the issue to a more suitable repository
* **maintainer** assigns the milestone, if necessary after consultation with **reviewer** and other **stakeholders**  and **reviewers**
* if issue is in the current milestone, **developer** fixes it at their convenience and assigns the issue to the **reviewer**
* if **reviewer** is happy, issue is closed


## Documentation

We aim to follow [FAIR](https://www.fairsfair.eu/news/fair-assessment-and-certification-eosc-region-report-available) documentation practices.

* write documentation **for purpose**, not just for the sake of it. State purpose (reason to write, who will read, when and why) in the b
* **writing extensive documentation is not excuse to write unclear code**. 
   * **Make your code as clear (and maybe not too "smart") as possible**, and complement with notes and comments explaining motivation when it is unclear - but do not use comments to repeat what codes does. 
* put **documentation near the code when possible**, when not - think hard what is the purpose of a separate note.
* make **references** to the doc and from the doc:
   *  **Make documentation discoverable! - i.e. referenced from known locations**. Not discoverable doc is all but useless and will likely be re-done unknowing. 
   *  not be afraid to put references to diverse resources, including restricted internal resources. 
   *  be sure that doc leads from somewhere and gets somewhere, **anticipate doc user flow**
   *  in particular **in document is abandoned, outdated, or moved, leave a reference to follow-up**. Do not let reader be lost!
* try to follow [metadata ontology](https://redmine.astro.unige.ch/projects/cdci/wiki/Metadata-Schema)


### Synchronizing git, redmine, etc

We have many sources for doc. Luckily, we have tools to synchronize them.

For example [redmine-flow] (try `pip install redmine-flow`) allows to push/pull docs from redmine similarly to git. 
To convert between doc formats, it's good to use [pandoc].

## Unofficial, contributing, and third-part developments 

Sometimes, there are features not available in ODA platform or oda-api, but may be useful to many users.
This is especially relevant for user interface developments outside of `oda-api`. For example, typical [blocks of data analysis workflows](https://github.com/integral-observatory/cc-isgri-oda-spi-reference) or tools to reorganize and [optimize typical usage patterns](https://gitlab.astro.unige.ch/oda/api-clients/oda_api_wrapper/).

Key distinction of these developments from the "standard" tools in oda-api is they do not need to go through regular development and release process, involving discussion and agreement by all relevant ODA contributors.
Due to lack of guaranteed aggrement, it is possible that these tools will facilitate unintended or even unfortunate usage patterns.

Nevertheless, such developments may be recommended, with caveats, to users. If recommendation is addressed from the ODA team, the aggrement should be made in each case.

If a particular tool turns out to be useful often enough, it should be considered if some of its features should be adopted in ODA. E.g. in `oda-api`. This adoption should follow the regular discussion and development process, and eventually becomes part of the "standard", recommended, and documented way to use ODA.


### On the Style

Style is important, but it has a purpose. Let us not focus on taste too much and make style work for us. See dedicated [note](style-guide.md).
