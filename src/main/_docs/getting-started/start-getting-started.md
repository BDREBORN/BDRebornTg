---
tag: [ "codenvy" ]
title: Getting Started
excerpt: ""
layout: docs
permalink: /:categories/getting-started/
---
{% include base.html %}


**Applies To**: Codenvy on-premises installs and codenvy.io hosted accounts.

---
You can get started with Codenvy through our hosted offering or by installing it yourself.

| Get Started Options | Action |
|:--- | :---: |
|Create a Free Account at codenvy.io. Everyone gets 3GB for free. Connect to a public toolchain and be coding in minutes.| [Sign up](https://codenvy.io/site/create-account)
|Download Codenvy. Install Codenvy anywhere Docker runs and connect it to your private toolchain. Control security and configuration–even add your own extensions.|[Install Now]({{base}}docs/getting-started/getting-started/index.html#install)

## Install
With Docker 1.11+ on Windows, Mac, or Linux:
```
$ docker run codenvy/cli start
```
This command will give you additional instructions on how to run the Codenvy CLI while setting your hostname, configuring volume mounts, and testing your Docker setup.


## Where To Go Next
| I am a...   | Consider going to... |
| --- | --- |
| **Developer** who will be using Codenvy for my projects. | [*The User Guide*]({{base}}/docs/getting-started/admin-intro/index.html). This will teach you how to configure and use workspaces so that they bend to your magical programming will. |
| **Developer** who will be creating custom extensions, plug-ins, and assemblies to package Codenvy and Eclipse Che into new tools. | [*Che Plugin Guide*](). These docs will help you setup your dev evironment and walk you through how to create server- and client-side extensions and plugins. If you are going to place your extensions into a Codenvy On-Prem instance please [contact us for guidance](https://codenvy.com/contact/questions/). |
| **DevOps** or **Developer Services** or **Team Lead** who will be integrating Codenvy into my agile tool chain to automate developer bootstrapping or to create a better agile experience for my developers. | [*The DevOps Guide*]({{base}}/docs/integration-guide/workspace-automation/index.html). We will give you amazing configuration fu (or `foo`, if you like) on how to define and integration on-demand workspaces into every tool. Wherever your developers go, you can create workspaces that embed into their tools that become part of their every day process. |
| **System administrator** who will be installing Codenvy On-Prem for my own organization or managing an organization of accounts at Codenvy SaaS. | [*The Admin Guide*]({{base}}/docs/admin-guide/installation/index.html). With more flexibility than a Swiss Army Knife, you will install, configure, and operate a global Codenvy cloud servicing millions of developers. |
