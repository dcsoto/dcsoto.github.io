---
layout: post
title: My essential toolbox for bioinformatics - an update
subtitle: Conda and Snakemake
show-avatar: false
tags: [bioinformatics]
permalink: /2020/03/31/bioinformatics-toolbox-update/
---

More than a year after the [original post](/2018/07/06/bioinformatics-toolbox/), I decided to update this blog post with two other essential tools for the modern bioinformatician. Spoiler alert! These tools are Conda/Bioconda and Snakemake. My life without them would be incomplete, so I felt the moral imperative to share it with you.

## Installing software

This is the universal headache of all bioinformaticians, I dare say. Here is an accurate description of a normal day in the life of a researcher: You finally got your data (yay!), you have a cup of coffee in your hand, and you are ready to start running that bioinformatics analyses! Oh, wait, you need to install the software first. However, sooner than later you see yourself drowning in a sea of dependencies with cryptic names.

If you work in a shared computational cluster, the first thing that you want to do is to check if the software is available as a module. You can do that using `module avail` command. If you happen to find the desired software on the list, then you can load it using: `module load <software name / version>`. If this is not the case, you may want to submit a ticket requesting the sysadmins to install the software for you.

- **Personal winner**: I use Conda/Bioconda! Conda is a package, dependency, and environment management system that not only allows you to easily install software but also creates independent environments! Environments are basically parallel universes regarding software installation. Bioconda - on the other hand - is a repository of biological programs available to be easily installed with Conda. (Thanks to all Bioconda maintainers, you are angels.) To get all the benefits of this magical tool, [install the latest version of Miniconda and then load the Bioconda channels](https://bioconda.github.io/user/install.html#install-conda).

> Here is a pro tip: when you install software, add the version of the software you want to install explicitly. For example, if you want to use Samtools v1.9 do: `conda install samtools=1.9`. Why? If you omit the versioning in the installation command, Conda will try to install the latest version by default. This is not always desired since the latest version may not be the "official" version. So, don't forget to add the exact version.

## Automating pipelines

In bioinformatics, a pipeline is a series of steps that your data undergo in order to achieve some desired outcome from which you can extract biological insights. The latter part is key - in mind the biological questions always keep (with Yoda voice). Bioinformatics pipelines sometimes need to be applied to multiple samples, multiple treatments, multiple species, multiple batches... and so on a so forth. If you see yourself repeating the same bioinformatics pipeline, again and again, you may want to look into workflow automation management systems.

Bioinformatics workflow automation refers to a series of consecutive steps conveniently wrapped in one tool that executes them without you. The main advantage is **reproducibility**, and - let me tell you - bioinformatics is in urgent need of more reproducibility. Also, it's convenient for the researcher; it's not humanly possible to analyze hundreds to thousand of samples without automated workflows.

- **Personal winner**: The best tool for this is [Snakemake](https://snakemake.readthedocs.io/en/stable/) in my opinion. This amazing tool is Python-based, which makes it incredibly flexible and powerful. In Snakemake, a series of rules (or steps in your pipeline) are written in a text file by the user (in this case, you). Then, the `snakemake` command reads the file and executes each step on its own. This means that after you have created the workflow (the text file with rules), you can run your whole pipeline with one simple `enter`. Isn't it cool?

However, there are some caveats to take into account. First - as everything in life - there is a learning curve associated with developing your own automated pipeline. If this is not the focus of your current work, maybe it doesn't make sense to invent the wheel again. Look for automated pipelines available online, but from trustworthy and citable sources! Secondly, if you are running a particular pipeline once and that's it, maybe you don't really need to develop an automated pipeline in the first place. And finally, consider that not everything in this world deserves to be automated (!). Why? Well, data analysis requires looking at your data, checking each step, making plots, testing hypothesis, developing new hypotheses, and so on and so forth. We just cannot automate critical thinking. That's your jobs as a bioinformatician :)


## TL;DR

If you want to install bioinformatics software on your own use Conda, and if you have a bioinformatics pipeline that you have to run in multiple samples again and again use Snakemake workflows (either from trustworthy sources or written by yourself).

## Acknowledgements

I must say thank you to my Twitter connections that gave me feedback on my [original post](/2018/07/06/bioinformatics-toolbox/) and encourage me to add the tools mentioned here. It took me some time, but, in my defense, I was busy with my QE (I passed!) and finishing a paper (it's published!). Let me know if you have any opinions, suggestions or recommendations on my [Twitter](https://medium.com/r/?url=https%3A%2F%2Ftwitter.com%2Fdcsoto_cl) account.
