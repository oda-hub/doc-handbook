# Development Handbook


## General

* When building interfaces accessible by other apps/users, try and stick to a pre-defined set of standards and schemas (e.g. swagger). Make the schemas discoverable, ideally referenced in the README.md on oda-hub repositories.
* Follow the [issue handling principles](https://github.com/oda-hub/doc-ops-reporting#issue-handling-principles) - in order to never have user issues unhandled.
* Do not be afraid to introduce large changes, but only if they respect previous interfaces.

## Do not forget to

We all do many things, but we should be concious that certain actions are crucial for the progress of collective projects: even though those may be delayed if necessary, there should always be a reason behind. Too much notifications and distractions are detrimental to productivity, but some level of engagement should  always be maintaned.

It may be advisable to make sure all actions and channels converge to email:

* on github check assigned issues, reviews, pull requests (this is all reflected in notifications, and other fields in the github page header)
* communicate by mattermost and slack

Other notifications systems are of course available, in order to increase the visibility of all the changes, but email should still be considered the main one.

## Branches, Versions, Releases

### Our previous approach and the relative problems

We used release branches for each version, like **production-V.V**. Any bugfixes were applied to these branches. In addition, **staging-V.V** were used for ongoing developments in current version. Also, for previous versions, **staging-V.V** were used to preview updates before making them live. This worked quite well.

Having on github the current development in the latest **staging-V.V** branch, whichever it happens to be at the moment, is not conveninent. So, to reduce the uncertainty on what is the current development version, we just use the **master** branch, and merge on it all the new features. 

A later transition to the **main** branch might happen, if that's the case, it will be communicated and this document adapted accordingly.

We used to mantain the current development is in the latest **staging-V.V** branch, whichever it happens to be at the moment. We knew which one this was, as the pace was slow, and the people involved were few: but this now is becoming more difficult.

Previously, **staging-V.V** deployment was automatically updated and merged with all the relative component branches. However, some components evolved very little, and it was not useful to keep creating new identical branches - this introduced confusion, since there was a lack of clarity. With faster development, more components, and in turn more branches, the development becomes more and more difficult to track. 

### Current strategy

To minimize the uncertainty on which the current development version is, we use the **master** branch for merging all new features.

Once a release needs to be made, we create a **release-YY.MM** branch and a tag **v-YY.MM.PPPP**. From that point forward, no further development will be made to the **YY.MM** version except for bugfixes. Every bug fix will yield in an increase of the patch level (**PPPP** part).

Instead of **staging-V.V**, we will make a deployment for review from each PR. This is becoming possible with the new and improved k8s cluster.
In addition, we continue maintain the current development **staging** version of the platform, made from tip of the **master** branches of all components. This one will be similar to what we did so far with the latest **staging-V.V** version.

**This approach will go along with faster development rate, and will enable a faster roll-out of new features**.

* Note that this description applies first of all to the version of the entire platform, i.e. http://github.com/oda-hub/oda-chart.git, which contains (or will contain) references to all the  components. Versions of the individual components should also follow the **calver** scheme. But until referenced in oda-chart they will not be generally deployed. However, we may semi-automatically update oda-chart with updates of some components.

**NOTE**: we should [confirm](https://github.com/oda-hub/meetings/blob/main/2021-03-29/agenda.md) the calver approach, which was recently [suggested](https://github.com/oda-hub/meetings/blob/main/2021-03-22/minutes.md)

So far we have used [SemVer](https://semver.org/), ending up with 1.2 production and 1.3 planned release. However, we found that the scope of the next planned version has been always shifting. This is not necessarily bad, but we take an opportunity of reorganizing development in new framework and more naturally adopt [CalVer](calver.org) as well as also make releases more regularly (at least yearly and/or when substantial new features annd bugfixes have been implemented and tested thus being ready to be released).

More frequent bugfixes will happen as necessary. This will be reflected in the version as so:

**release-YY.MM.PPPP**

where **YY** and **MM** correspond to the release month and year respectively, and **PPPP** is an incremental bugfix/update level since the release.

For example, next release will be **21.05.000**.

CalVer will also clearly communicate the pace of development, hopefully reducing hesitation in making a new release, thus making the development more dynamic and consistent, matching the repeated requests from the users.

In summary:

* use the master branch for current stable staging version (i.e. no need for staging-1-3 etc), as deployed in UNIGE in staging (pre-release) environment. It may also implement quick bug-fixes, but not new running feature developments (feature branches are for that)
* for production, we still use release branches, e.g. production-1-2
* use feature branches as necessary, in forks or in the base repository

## Github, Gitlab(s), etc?

We use github for common activities, as it is currently the most easily discoverable space.
UNIGE Platform is deployed with CI/CD from integral gitlab, which is synchronized with github (it is also used for internal projects).

**where to push?** we should make sure each repository which has both github and gitlab.astro.unige.ch versions to be synchronized between the two. Simple tooling is needed to ensure both locations are synchronous.

## Documentation

We aim to follow [FAIR](https://www.fairsfair.eu/news/fair-assessment-and-certification-eosc-region-report-available) documentation practices.

* Write documentation **for a purpose**, not just for the sake of it. State the purpose (reason to write, who will read, when and why) in the b
* **Writing extensive documentation is not excuse to write unclear code**. 
   * **Make your code as clear (and maybe not too "smart") as possible**, and complement with notes and comments explaining motivation when it is unclear - but do not use comments to repeat what codes does. 
* Put **documentation near the code when possible**, when not - think hard what is the purpose of a separate note.
* Make **references** to the doc and from the doc:
   *  **Make documentation discoverable! - i.e. referenced from known locations**. Not discoverable doc is all but useless and will likely lead to repetition
   *  Not be afraid to put references to diverse resources, including restricted internal resources
   *  Be sure that doc leads from somewhere and gets somewhere, **anticipate doc user flow**
   *  in particular **in document is abandoned, outdated, or moved, leave a reference to follow-up**. Dont let the reader be lost!
* Try to follow [metadata ontology](https://redmine.astro.unige.ch/projects/cdci/wiki/Metadata-Schema)


### Syncronozing git, redmine, etc

We have many sources for doc. Luckily, we have tools to synchronize them.

For example [redmine-flow] (try `pip install redmine-flow`) allows to push/pull docs from redmine similarly to git. 
To convert between doc formats, it's good to use [pandoc].
