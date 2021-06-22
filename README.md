# Development Handbook


## General

* When building interface accessible by other apps/users, try stick to standards and schemas (e.g. swagger). Make the schemas discoverable, reference in README.md on oda-hub repositories.
* Follow [issue handling principles](https://github.com/oda-hub/doc-ops-reporting#issue-handling-principles) - in short, do not expect user issues to be left unattended, never.
* Do not be afraid to introduce large changes, but only if they respect previous interfaces

## Do not forget to

we all do many things, but we should be conscious that some actions are needed for smooth progress of collective project.
Even though these actions may be delayed as necessary, it should be done with intent.
Too much notifications and distractions are detrimental to productivity, but one should aim keep some level of engagement.

It may be advisable to make sure all actions and channels converge to email. 

* on github check assigned issues, reviews, pull requests (this is all reflected in notifications, and other fields in the github page header)
* communicate by mattermost and slack

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

Releases will be made as soon as accumulated features are necessary, made into release branch from the master branch, and tagged. Further 
If a bugfix is necessary, a dedicated bugfix branch will be made and destroyed when bugfix version is tagged.

* use master for current stable staging version (i.e. no need for staging-1-3 etc), as deployed in UNIGE in staging (pre-release) environment. It may also experience quick bug-fixes, but not new running feature developments (feature branches are for that).
* for production, we still use release branches, e.g. production-1-2.
* use feature branches as necessary, in forks or in the base repository

## Github, Gitlab(s), etc?

We use github for common activities, as it is currently most easily discoverable space.
**UNIGE Platform is deployed with CI/CD from integral gitlab**, which is pushing changes with github.
It is also used for internal astro-only projects.

**where to push?** 
* Any change to gitlab.astro.unige.ch is synchronized to github.
* not every change to github is is synchronized to gitlab.

Since PRs are made on github, changes from github need to be propagated to gitlab, possibly customly.

## Github project management features: Labels, Milestones, Projects

We need multi-repository management, and we can use **milestones to mark planned release versions**.

In principle, both **labels** and **milestones** are per-repository, but even if they are created independently, they can be aggregated in organization if they are called the same way.

For v21.06 release, all issues can be seen here: [v21.06 issues](https://github.com/issues?q=is%3Aopen++user%3Aoda-hub+milestone%3Av21.06+).

Projects can be used to group and preview issues more nicely. [ODA Platform project](https://github.com/orgs/oda-hub/projects/1) shows all issues/PRs for the platform, and can be filtered [for v21.06 release](https://github.com/orgs/oda-hub/projects/1?card_filter_query=milestone%3Av21.06).

To avoid duplication, **milestones** can be seen as primary indication of the issue/PR assignment to the release, and **project** is a complementary presentation feature.

**Labels**, on the other hand, describe different aspects of issues (documentation, bug, etc). Details of the labels purpose should be put in the label descriptions.

## Dealing with Issues emerging in review and operations

once a problem is found by a reviewer, it goes through the following stages:

* **reviewer** creates github issue in some repository, at their discression
* if necessary, **maintainer** moves the issue to a more suitable repository
* **maintainer** assigns the milestone, if necessary after consulatation with **reviewer** and other **stakeholders**  and **reviewers**
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


### On the Style

Style is important, but it has a purpose. Let us not focus on taste too much and make style work for us. See dedicated [note](style-guide.md).
