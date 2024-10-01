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

Every repo should have a `README.md` that explains what the repo contains and how it was used. The repo containing the source code for a simulation should contain explanations for how the simulation works. The repo for the analyses of some data should explain how the scripts must be run. The repo for the data should contain and explanation of how the data were obtained (if that is not written in the manuscript). Here I invent nothing, and there are already good standards for documentation. I am not a fan of repeating everything many times though, so I am more a proponent of one `README` per repo (unless really necessary). Check out [this](https://github.com/rscherrer/reschoice) for an example of good repo documentation.

### 2.3.1. Simulated data

Make sure to have in the `README.md` of the data repository of a simulation study, the steps involved in simulating the data. Sometimes those are not trivial and may require extra scripts or manual tweaks, for example if the simulations had to be run in many batches on a computer cluster. Those steps won't necessarily be fully reproducible by everyone (not everybody has access to the same, let alone one, cluster). But at least there is an accurate description of what has been done, and it can be also useful for myself to come back to if I need to run extra simulations down the line.

### 2.4. Versioning

I LOVE to use the GitHub option to "draft a new release" whenever I am kind of done with a repo. If my simulation code is done, I'll version it 1.0. If a new feature is added, that's version 1.1. Major change making back-compatibility difficult? 2.0. I do this also with repos that are not source code for a program. For example, is the manuscript repo ready to be sent to supervisors for revision? That's version 1.0. Am I implementing their comments and feedback? That's version 1.1, 1.2, etc. Are we ready to submit to a journal? 2.0. Same for repos containing R scripts, Mathematica notebooks or even simulated data. Version, just so we can go back to a previous, clearly identified archive if need be.

I also do it with [courses](https://github.com/rscherrer/evo-theo-manual) or [lectures](https://github.com/rscherrer/evo-bio-cc) that iterate every year with some change. Here, the versioning can even have the name of the year (e.g. version 2024).

## 3. Good practices

### 3.1. Documentation

Document, annotate and write README files **early** on in the development of a project. Otherwise, it really quickly gets out of hand (either the analysis branches off in a hundred directions, or there ends up being many copies of the same file --- see [this](https://github.com/rscherrer/brachypode-nb) for an example of what not-to-do). You do not want to come back to those files at a later stage (say, just before submitting to a journal) and having to reverse engineer what is what. And do that, **even if** you know that many of the scripts or analyses or figures produced will not make it into the final manuscript.

## 4. Literature review

### 4.1. Workflow

How do I conduct literature review when working on a paper?

1. Make a specific directory in Zotero for the current review.
2. Initial search by keywords in Google Scholar, and save a lot of references into Zotero. That is my first line of defense.
3. Go through each downloaded paper to get a general idea of what is being said. Take notes from each paper: what I learned in them.
4. Write a summary of what we have learned for each paper, in one or a few sentences.
5. Identify which ones were reviews or which ones were particularly relevant for my research question.
6. Plug those into Connected Papers to get a network of papers. This is the second line of defense.
7. Go through the connected papers and write a (directed) text with the review, augmenting it at every relevant fact. This is in case we are writing the literature review from scratch. If this is upon adding relevant literature to an already-drafted introduction or discussion, add a citation in the relevant place in the text for each paper we go through (at the risk of having more cited papers than necessary).
8. Refactor the written review based on how I want to organize the flow of the argument, and if needed, go back to some key papers to add details that I may have missed but only later figured were important.
9. Remove superfluous citations when we realize those don't really add much. But keep a line as comments in the LaTeX source code explaining in one sentence what they are about (we may want to add them back in).

(Subdirectories?)

### 4.2. Collections

In my reference manager, I like to organize collections by manuscript or project I am working on (those can also be for a presentation or a lecture, for example). This makes it easy to export the collection of references to the BibTeX format into a single file that I can then use in my LaTeX manuscript.

### 4.2. Wrapping things up

When the manuscript is almost ready, I like to clean up my reference manager library (here Zotero). First, I use Zotero's function to remove duplicate items. Then, I make sure all titles are in the right case (journals like _Evolution_ love to capitalize the titles of papers). Finally, I export the collection, recompile my (LaTeX) manuscript and go through it to make sure to correct any BibTeX keys that may have changed (and so make sure that each source is properly cited).

## 5. Figures

Figures live in the repo of the manuscript. Makes sense, that's where they matter. So, the manuscript should have a `figures/` folder. Now, I see two types of figures:

1. "Hand-made" figures (e.g. with Inkscape or Illustrator) that required some manual editing. Often times those are photos (as in [this](https://github.com/rscherrer/dewlap) repo) or overview diagrams showing the workings of a model (as in [this](https://github.com/rscherrer/speciome) one). They only live in the manuscript repository, and if they were built with some graphics tool (e.g. Inkscape or Gimp) then they have their own folder with the raw project file used to edit them (e.g. the original SVG file in Inkscape so we can modify the figure if needed).
   
2. Programmatic figures, produced by a third-party software. Most of the time that would be R. However, I do not like to host R scripts used to generate figures in the same place as the manuscript, because that makes the manuscript repo way too large. Instead, all the analyses are usually hosted within their own repository. This is also convenient in that I can generate many more figures (e.g. to visually check many things) than will eventually make it into the manuscript (and interested readers can always go check the analysis repo to see those extra figures). Of course, the important bit there is that I need to make sure to move copies of the relevant figures from the analysis (or `results/`) repo into the manuscript repo. Then, because this gives rise to two copies of each figure present in the manuscript, it is important that they have the same name (to be able to find the source figure easily if it has been updated and needs to be replaced in the manuscript, for example). Hence the importance of giving figures **meaningful names**. Alternatively, it is also possible to write a shell script to automatically import the required figures from the analysis repo to the manuscript one.

As a general rule I go for the PNG format, as it is easy to resize and does not take much space for complicated figures.
