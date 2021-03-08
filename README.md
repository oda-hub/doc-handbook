# Development Handbook


## General

* When building interface accessible by other apps/users, try stick to standards and schemas (e.g. swagger). Make the schemas discoverable, reference in README.md on oda-hub repositories.
* Follow [issue handling principles](https://github.com/oda-hub/doc-ops-reporting#issue-handling-principles) - in short, do not expect user issues to be left unattended, never.
* Do not be afraid to introduce large changes, but only if they respect previous interfaces

## Branches

* use master for current development version, as deployed in UNIGE. It may also experience quick bug-fixes, but not new running feature developments (feature branches are for that).
* for production, use e.g. production-1-2 and for staging - staging-1-2 (as of now, with dashes)
* use feature branches as necessary, in forks or in the base repository
* latest staging might or might not coincide with master. 


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
