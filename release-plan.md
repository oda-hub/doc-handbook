## Release planning strategy

We are following AGILE practices, prioritizing user needs and concerns and reaction to changing environment over rigid planning.
We release minor updates to the core platform often, typically once a week.
**Major releases** are driven by introduction of **major features** which deserve additional attention and **dissemination**.

Once it is decided that a **major feature** is the priority, the development of this feature is tracked in **issues**: github, gitlab(s), redmine, etc.
**Issues** blocking this **feature** may receive a correspoding **labels**. Issues which are not labeled are not blocking the feature but might still be relevant.

We are also using full-text search and NLP semantic harvesting to relate issues with goals, so unlabeled issues are not lost.

### Feature release: Gallery in MMODA

![image](https://github.com/oda-hub/doc-handbook/assets/3909535/37f151ee-2c39-4d29-bdf3-ebaa59822e00)


The coming release is driven by integratng MMODA Gallery in main MMODA UI.
The release is expected for Nov 2023.

As of early Nov 2023, this feature is blocked by insufficient responsiviness of gallery data store.

### Feature release: Crowdsourcing MMODA tool construction 

![image](https://github.com/oda-hub/doc-handbook/assets/3909535/9d64016e-cf9f-45f1-9ab6-8a91e7d217f1)


Integration between MMODA and RenkuLab allows broad range of users to construct MMODA online analysis tools in reproducible jupyterlab environment powered by gitlab, jupyterhub-like platform, and a knowledge graph.

This functionality is already used by a group of developers and astronomers, and is currently in live testing on staging platform.
The release to broad community is expected early 2024.
