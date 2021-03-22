# Development Handbook


## General

* When building interface accessible by other apps/users, try stick to standards and schemas (e.g. swagger). Make the schemas discoverable, reference in README.md on oda-hub repositories.
* Follow [issue handling principles](https://github.com/oda-hub/doc-ops-reporting#issue-handling-principles) - in short, do not expect user issues to be left unattended, never.
* Do not be afraid to introduce large changes, but only if they respect previous interfaces

## Branches, Versions, Releases

So far we have used [SemVer](https://semver.org/), ending up with 1.2 production and 1.3 planned release. However, we found that scope of the next planned version has been always shifting. This is not necessarily bad, but we take an opportunity of reorganizing development in new framework and more naturally adopt [CalVer](calver.org) and make releases regularly (at least yearly).  More frequent bugfixes will happen as necessary. This will be reflected in the version as so:

**YY.MM.RRR**

where **YY** and **MM** correspond to the release month, and **RRR** is an incremental bugfix/update level since the release.

for example, next release will be **21.05.000**.

CalVer will also clearly communicate pace of development, hopefully reduce hesitation in making the next significant release, and make the development more dynamic, matching the repeated requests of the users.

Releases will be made as soon as accumunated features are necessary, made into release branch from the master branch, and tagged. Further 
If a bugfix is necessary, a dedicated bugfix branch will be made and destroyed when bugfix version is tagged.

* use master for current stable staging version (i.e. no need for staging-1-3 etc), as deployed in UNIGE in staging (pre-release) environment. It may also experience quick bug-fixes, but not new running feature developments (feature branches are for that).
* for production, we still use release branches, e.g. production-1-2.
* use feature branches as necessary, in forks or in the base repository


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
   *  in particular **in document is abandoned, outdated, or moved, leave a reference to follow-up**. Dont let reader be lost!
* try to follow [metadata ontology](https://redmine.astro.unige.ch/projects/cdci/wiki/Metadata-Schema)


### Syncronozing git, redmine, etc

We have many sources for doc. Luckily, we have tools to synchronize them.

For example [redmine-flow] (try `pip install redmine-flow`) allows to push/pull docs from redmine similarly to git. 
To convert between doc formats, it's good to use [pandoc].
