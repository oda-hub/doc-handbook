h1. FAIR Project Organization Tools - the handbook

|_. Prepared-By | "VS":https://vs.solidcommunity.net/ |
|_. Prepared-For | writers of text, code, and the so |

h2. Motivation

We have a diversity of software tools for different aspects of project organization, complicated by some diversity of associated projects (e.g. CDCI, INTEGRAL, and some scientific projects are co-developed and interlinked) and organizations.

In all cases it is necessary to ensure that documents are findable, accessible, and interoperable.

h2. Linked Documentation Principles


* Maintaining *bidirectional references with "suitable metadata":https://redmine.astro.unige.ch/projects/cdci/wiki/Metadata-Schema for all developments and activities*.

* *References* are implemented as entity *URI*, and should be annotated (cmp the "Linked Data":https://www.w3.org/standards/semanticweb/data principles).</pre>

* Metadata will indicate what is the purpose of the document, to prevent production of not-findable not-accessible not-understandable/usable documents.

Additional considerations:

* one shall not write a document when a "script will suffice":https://www.oilshell.org/blog/2021/01/shell-doc.html:
* as one shall not trap code in text when self-documented clear code can be made, just as you would not trap data in text "without computable provenance":https://github.com/oda-hub/linked-data-latex/
* it is because documented code is no excuse for unclear (bad) code
* one shall think before writing document if it is needed
* one shall think before writing document if it has been written, and attempt to find it using references 
* one shall use "tools to help organizing documentation for this purpose":https://github.com/volodymyrss/oda-doc

h2. Available platforms

List here are the platforms used in the Department, with read-write access. I.e. not external documentation sources. Some platforms are ambigious in this respect, specifically the institutional ones.

* https://redmine.astro.unige.ch/

the best available solution for issue management in the Department seems to be the redmine. It also supports

* https://gitlab.astro.unige.ch/

code-heavy projects yield inevitably actions in code projects, such as Merge Requests (Pull Requests) and possibly issues.

* https://gitlab.unige.ch/

there is also an institutional solution, which has andvantage of authenticating many Swiss institutions, as well as any user with free SWITCHedu account.

* https://gitlab.in2p3.fr/

for projects with strong French contribution, we use highly advanced platform of CNRS/IN2P3.

* https://github.com/

for projects with wide public reach, it is suitable to use a world-wide platform, with high potential for code discoverability and cross-institute collaboration

_examples_: https://github.com/volodymyrss/pygcn

* https://overleaf.com/

an ideal and widely used solution for collaborative editing

* https://www.astro.unige.ch/wiki/projects/cdci

* google docs

* office365



* ESA's SOCCI (confluece, etc)

handles document management, issue tracking, workflows, for ESA projects. Considered the reference for ESA collaboration.

_example_ :https://issues.cosmos.esa.int/socciwiki/display/INT/ISDC-EXPRO-TN-0005

* taskwarrior, or other personal management tools

a tool for private management, as no shared task server is available (or should be available).

h2. Activity aspects


h3. Document management

Writing documentation: documentaiton for the people, not for literal value. Unfortunately people do not read our help pages, and/or do not pay attention to the instructions (50scw limit, OSA11 validity, effect of repeating requests). 


redmine.astro.unige.ch wiki

overleaf

h3. Code management

gitlab and github instances are associated with code management.

*recommendation*: for every project, insert a reference in an upstream document, and add metadata

h3. Issue tracking

All of the issue tracking systems have suitable API's, which can be integrated, for example, with bugwarrior. The upstream issue management is considered to be *redmine*, meaning that only those issues that end up in redmine are ensured to be followed up.

Collaborators are not, however, restricted from making private TODO lists, possibly managed by taskwarrior.


h2. Interactive Meeting

Prepare for the meeting:

* list completed issues
* list planned issues

to be done by manager and participants

[tools handbook](https://redmine.astro.unige.ch/projects/integral/wiki/Project_Organization_Tools_-_the_handbook)



META: upstream, https://redmine.astro.unige.ch/projects/cdci/wiki/Integration_and_release_cycle_management

h1. Metadata

Metadata is relevant for each record: document, issue, code, meeting, etc - all of the things should be FAIR.

Metadata constitutes entity provenance (past) and directions for operating the document (future).

obligatory:

* primary location reference
* reference to the latest version of this document
* responsible author (i.e. reference to a person)
* last modified

optional

* also-known-as refrences

metadata might be derived from the location. I.e. git yields author, version, time, provenance


h1. Best practices

documents:

* Use *Redmine for reference* copies of the documents. 
* Redmine *issues* will contain a trace of the activity, but they are a bit too conversational, keep summary in the notes/README.
* Use gitlab for *code management* and next-to-the-code notes/README

issues/tickets (general):

* when issue is *created*, instructions to refer to the relevant explanatory documents
* performing a task should usually *complement* instructions or make the necessary documents
* in case of *problems and questions*, principally use Redmine to define issues and assign them to the person who should react. It can be yourself or anyone else.
* *Assigning* issues is not just about assigning work, it is about direction actions/questions - hence no problem to assign tickets to managers.
* We should not hesitate to use *Estimated Time* (even if unclear) and *Spent Time*, especially since we have some activities in the off-time.
* We should use *issue relations*, in particular *Blocked By* (task dependency)
* gitlab merge requests will yield issues. Also gitlab, confluence have issues. The can be used in limited circle, but one should be cautious with these, since the only issues which are guaranteed to be followed-up are in redmine.

routine practice:
* check [my tasks in redmine](https://redmine.astro.unige.ch/my/page)
* pick *any* interesting task which is not  *Blocked By* another task
* all unblocked tasks are equally good, unless some have high priority. It might be suitable to progress on a couple of tasks at once, but one should be cautious not to spread too much, accounting for large gaps between high-engaugement work in our schedule.
* for the completed tasks, it's very useful to share journal, document (redmine), and *code/notebooks (gitlab)*.

in case of new questions/issues:
* check the [handbook](https://gitlab.astro.unige.ch/integral/isgri-calibration/handbook/)
* look through the relevant [issues](https://redmine.astro.unige.ch/projects/integral-isdc-critical-activities/issues)
* ask a colleague by [mattermost](https://mattermost.astro.unige.ch/isgri-calibration/channels/town-square)/email
* create a [new issue](https://redmine.astro.unige.ch/projects/integral-isdc-critical-activities/issues/new)

detailization level of the tasks should be:
* high enough to allow as much as possible autonomous work of the entasked one
* low enough to avoid unjustified assumptions about the realtime sitations: very detailed steps may become obsolete with a single realtime finding
* not so high as to increase the burden on the task writer