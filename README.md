# rules-of-thumb

Rules of thumb when conducting research. In this repository I share the way I like to organize my scientific projects. This may or may not be useful to anyone, but at least it is good for me to make sure I stick to my own guidelines. These guidelines were developed through lots of trial-and-error and communication with colleagues, and are the result of what I have gathered so far. They are by no means set in stone, and I hope to improve them as I go through my scientific journey. Here are my commandments to myself.

## 1. Thou shalt make use of GitHub

I opted for a "mobile" style of work: I want to have my work accessible from anywhere, any time, which means I need a "cloud" to store all my things. I host all my projects on [GitHub](https://github.com). Here are the reasons why.

### 1.1. Storage and accessibility

As I mentioned before, GitHub makes all my work accessible from anywhere. It does not allow repositories of more than 1Gb though, so it mostly hosts code for analyses or manuscripts. For big databases, I make use of Google Drive (see further section).

### 1.2. Version control

GitHub is more than Google Drive or Dropbox in that it is a version control system: I can retrieve any older version of my work easily, and all the changes I make are registered without me having to create a thousand different copies of the same files. Branches also allow multiple versions to coexist together. More later on the branch structure I follow.

### 1.3. Collaboration

Not all my repositories are collaborative, but the branch structure of repositories makes collaboration very easy. More later on the branch structure I go for when collaborating. Of course, forks allow external contributions, which is great.

### 1.4. Visibility

I can advertise my work by sharing my GitHub account! This is basically where stuff happens and where people can look up what I am up to. People can also download my work by cloning my repo, it's that easy.

### 1.5. Reproducible science

You may have heard of the [replication crisis](https://en.wikipedia.org/wiki/Replication_crisis), this idea that scientists are realizing more and more that past results are difficult, and sometimes impossible, to reproduce. Working towards making science more reproducible is therefore rising as one of the top priorities within the future generation of scientists. Reproducibility, together with open science and pre-registration, is part of a bundle of good practices to avoid biases resulting from cherry-picking, P-hacking or HARKing. I use GitHub as a tool to be part of this effort, where my work can be reviewed and myr results reproduced easily.

### 1.6. Third party add-ons

GitHub has connexions to a lot of third party platforms to do all kinds of things. I can sync my GitHub with Overleaf to work on my manuscripts in LaTeX (more on this later), but also activate Travis or Codecov on my repository to make sure my program is working (same, see relevant section).

### 1.7. When not to use GitHub

Unfortunately the storage limit within a repository is 1Gb, which makes GitHub not suitable for storing large databases used in some studies. GitHub is therefore reserved for code, analysis output and manuscripts mainly. For databases, see the relevant section.

### 1.8. Alternatives

Similar platforms exist: [Bitbucket](https://bitbucket.org/) and [GitLab](https://about.gitlab.com/) for example.

## 2. Project organization

### 2.1. One study, one project

I like each study to be a specific project. I can make use of GitHub's projects to keep track of what needs to be done within each project. But each project can contain multiple repos.

### 2.2. One project, multiple repos

I like repos to mostly consist of the same task. Let's say a project is a simulation study. For that we need the simulation code, the simulated data, and a special folder for analyses, plots and results. We might even need a package to read all those data in R. And of course, at the end of the day there should be a report or a manuscript. For each of these elements, I would then have a separate repo. This has multiple advantages: (1) each repo mostly consists of one programming language or type of content, so easier to troubleshoot; (2) we reduce the risk of reaching GitHub's storage capacity per repo; and (3) we keep the main types of activities in a research project clearly distinct and modular. 

That does not mean that all these folders have to be standalone on my computer. On the contrary, once downloaded repos can live inside of each other, with the appropriate additions being made to the various `.gitignore` files.

For example, a typical project, say `reschoice`, would consist of the following repos:

* https://github.com/rscherrer/reschoice
* https://github.com/rscherrer/reschoice-data
* https://github.com/rscherrer/reschoice-results
* https://github.com/rscherrer/reschoice-ms

The first repo would contain the C++ source code for the simulation. The second would contain simulated data (potentially lots of them). The third some R scripts to analyze the data and make plots and tables. And the last one would contain TeX files to generate a manuscript (this one would typically be synced to Overleaf so collaborators can all work on it together in a nice interface).

I would usually make sure that the various `README.md` files in those repos contain link to the other repos from within the same project, so one can navigate from one to another on GitHub. But, locally on my computer, I like to give those the following structure:

```
-- reschoice
|-- data
|-- results
|-- ms
```

That is, I clone the three last repos inside the first one. I also change their names as folders so as to not repeat myself too much (but online they are still called `reschoice-data`, `reschoice-results` and `reschoice-ms`). Finally, I make sure that there is a line in the `.gitignore` of the `reschoice` repo that says:

```
# Repos to exclude
data/
results/
ms/
```

### 2.3. Read me's

Every repo should have a `README.md` that explains what the repo contains and how it was used. The repo containing the source code for a simulation should contain explanations for how the simulation works. The repo for the analyses of some data should explain how the scripts must be run. The repo for the data should contain and explanation of how the data were obtained (if that is not written in the manuscript). Here I invent nothing, and there are already good standards for documentation. I am not a fan of repeating everything many times though, so I am more a proponent of one `README` per repo (unless really necessary).

### 2.3.1. Simulated data

Make sure to have in the `README.md` of the data repository of a simulation study, the steps involved in simulating the data. Sometimes those are not trivial and may require extra scripts or manual tweaks, for example if the simulations had to be run in many batches on a computer cluster. Those steps won't necessarily be fully reproducible by everyone (not everybody has access to the same, let alone one, cluster). But at least there is an accurate description of what has been done, and it can be also useful for myself to come back to if I need to run extra simulations down the line.



