---
layout: post
title: My essential toolbox for bioinformatics
subtitle: My personal favorites
show-avatar: false
tags: [bioinformatics]
permalink: /2018/07/06/bioinformatics-toolbox/
---

Nowadays, almost every scientific endeavor relies on computers to process and analyze data. Even if you are working mostly on the bench, you can really benefit from running your own computational pipelines to process and analyze your data.

I've compiled a very personal selection of my favorite computational tools to perform common tasks associated with data analysis and/or methods development as a computational biologist and bioinformatician. I thought this could be helpful for someone new to this field, so I wrote a blog post!

A brief disclaimer: This is what has worked so far, but I am always _scavenging_ for new tools. (So I'll be happy to receive your recommendations. Let me know on my [Twitter](https://twitter.com/dcsoto_cl) account.)

## Dealing with text files

Working with some sort of text file is at least 50% of my job. Most of your input files will be a text file. To properly work with them, you need a good text editor (_don't use your PC or Macbook default apps if you don't want to have hidden characters ruining your life_). Text editors not only allow you (1) to check a file's content, but also (2) to generate documentation, like markdown notebooks, readmes, and log files, or (3) to code in any language (I will cover these topics in later sections).

- **Personal winner:** [Atom](https://atom.io/) (Windows/Mac/Linux) is my go-to for text editing. It's easy to use, super customizable and can handle highlighting for several languages, you just have to add the proper extension to the file. It also accepts Markdown syntax. To do this, just create a file with ".md" extension and press CTRL+SHFT+M. This is my current favorite tool, so I will talk more about it in the following sections.
- **Other options**: [Sublime](https://www.sublimetext.com/) (Windows/Mac/Linux), [Notepad++](https://notepad-plus-plus.org/) (Windows).

## Setting a lab notebook

Just because you are not on the bench, it doesn't mean that you shouldn't document every step of your work. So before doing anything, set up your computational lab notebook. The most basic way to document your work is to use just a Google Docs file (sometimes it's the easiest way). However, what's quite popular now is using some sort of interactive notebook that combines text, code execution, plots, and more. Do you code in Python? [Jupyter Notebooks](https://jupyter.org). Do you code in R? [Rmarkdown in RStudio](https://rmarkdown.rstudio.com/). Do you use Bash scripting, R, Python, AWK, C/C++, Perl or anything that suits your data analysis? Well... that's me.

- **Personal winner:** Just a simple basic markdown editor, like Hackmd.io (if I need to work online) or [Atom](https://atom.io/) (Mac/Windows) (press CTRL+SHFT+M for Markdown capabilities), does the job for me. Sometimes I document my pipeline directly in GitHub using Markdown, which I will explain in the version control section. (Markdown, btw, is a light markup language that allows you formatting what you are typing using some "code" embedded in the text).
- **Other options:** As I mentioned before, you can use a Google Docs or Microsoft Word document, or even a plain text file to document your pipeline step by step. Interactive notebooks are another more sophisticated alternative. Here some comments about these:
    - _When to use an interactive notebook?_ (1) If you are working mostly in Python ([Jupyter Notebooks](https://jupyter.org)) or mostly on R ([Rmarkdown](https://rmarkdown.rstudio.com/)), (2) if you are doing mostly data analysis, i.e., generating tables, plotting, doing some statistics, or (3) if you want to run code directly on your notebook (because... why not?).
    - _When not to use interactive notebooks?_ (1) If you don't need an interactive notebook, or (2) if you are using several programming languages, scheduling things to run on the cluster, saving pictures, links and useful data inside your notebook, writing down hints and hacks, etc. I am more into this last description, so _what I do is to keep a main markdown file and use interactive notebooks for certain data analysis steps that I later reference in my main notebook_.

## Coding

Let's go into coding. Even if you are not a method developer, and you are running pipelines or analyzing your own data, chances are that you will have to use somebody else's code or code your own scripts.

_Warning:_ You don't need to reinvent the wheel. A lot of software and packages are available out there to do every kind of task. You have to use them wisely and have some rough understanding of the algorithm or strategy behind them.

### How to learn a new programming language

In my opinion, coding is pretty much a way of thinking: you have to  give instructions to the computer so it can make exactly what you want. Learning a conglomerate of syntax rules is secondary, but nonetheless important. The good news is that both of these skills can be developed.

If you want to improve your programming thinking, use the **alien technique** (that I am actually introducing in this blog post, btw). So, imagine that an alien that mysteriously speaks your language but has no previous knowledge about humanity whatsoever visits you, and for some reason you want them to make a PB&J sandwich. Well, assuming that you actually know how to make a PB&J sandwich, what orders would you give to your alien friend so you can precisely and efficiently guide them through your goal? Deep. Think about this.

Ok, so let's go to syntax. I imagine that most people want to learn R or Python nowadays. To this end, you can follow all, some or none of the following steps:
- **Buy a book:** This can be very useful, specially if you are one of those people that learn by reading. O'Reilly editorial has good programming books, like [Learning R](https://smile.amazon.com/Learning-Step-Step-Function-Analysis/dp/1449357105/ref=sr_1_3?ie=UTF8&qid=1528185628&sr=8-3&keywords=learning+R) (to learn basic syntax), [R for Data Science](https://smile.amazon.com/Data-Science-Transform-Visualize-Model/dp/1491910399/ref=pd_bxgy_14_img_2?_encoding=UTF8&pd_rd_i=1491910399&pd_rd_r=8574fde3-6896-11e8-a12a-ad7a82811235&pd_rd_w=OVsHx&pd_rd_wg=byrEB&pf_rd_i=desktop-dp-sims&pf_rd_m=ATVPDKIKX0DER&pf_rd_p=3914568618330124508&pf_rd_r=ANMRWJRG0JK1G57FNBSN&pf_rd_s=desktop-dp-sims&pf_rd_t=40701&psc=1&refRID=ANMRWJRG0JK1G57FNBSN) to learn tidyverse and ggplot (we'll talk about it later), and [Fluent Python](https://www.amazon.com/Fluent-Python-Concise-Effective-Programming/dp/1491946008) to learn Python (of course).
- **Create your own "cheat sheet":** This is the most important piece of advice that I can give you. While you are learning to code, create your own file using your chosen text editor. Include all the syntax rules that you learned about that language with explanations (this part is very important), so you can go back again and again to that file and remember exactly how to do anything. I can assure you that all my programming knowledge is in these files. Alternatively, you can choose to download one of the already available cheat sheet for every programming language.
- **Choose a project for some hands-on practice with your new language:** Well, this is at least very important for me because I learn so much faster while doing. If that is your case, select a challenge and code it!

### Which languages to learn

Bioinformatics usually requires shell scripting, and some high-level programming language (i.e. slow but friendly). Most popular languages in biology nowadays are R and Python (and Perl ~~if you starting coding in the 90's and you want to stay old-school~~). Other areas of biology like systems biology also use a lot of MATLAB.

Here a short description of my personal favorites:
- **Shell scripting**: A shell script is a code designed to run in a Unix shell or command-line interpreter. It's totally necessary if you have to run jobs in a Linux computer cluster. Linux commands are also very fast to perform operations over text files. Find, replace and remove patterns, intersect lists, find unique elements, find common elements... there is a Linux command for any of that (and if not, you can do some AWK one-liners, which I personally love).
- **R**: The most popular open-source programming language for statistics, I would say. It is very good and decently fast dealing with data. Several bioinformatics tools are available in R through Bioconductor, so you will probably have to use it at some point. There is a basic R syntax, however, there is an improved syntax created by Hadley Whickham (a star in the R world), who also created one of the most popular packages for data visualization. Here a little bit about those:
    - Tidyverse: is a collection of R packages specially designed to improve the data analysis workflow. To start using Tidyverse you can install all packages with `install.packages("tidyverse")`.
    - ggplot2: is a data visualization package that allows you to create very beautiful plots with a few instructions. `ggplot2` is also included in Tidyverse, so you don't have to install it again. However, it is so useful that it deserved their own bullet point.
- **Python**: The new "trendy" programming language for data science and bioinformatics. Same as R, it is very versatile, it has an easy learning curve, a lot of packages are available, and the community is getting bigger and bigger. Actually, Python and R are kind of similar and fans from one or the other usually "fight" about which one is better. My personal opinion is... none. Both are good enough. Actually, learn a little bit of both, because chances are that you will need to use a package in one and the other. That being said, if you work in Python here there are some packages that would make your life easier, so learn to use them:
    - Numpy: is a package for scientific computing in Python, that makes available N-dimensional arrays and matrices, as well as fancy math functions.
    - Pandas: provides data structures and data analysis tools that resemble a lot of R features. So, if you like R, then it would easy for you to use Pandas in Python.
    - Matplotlib: is a 2D plotting library that creates high quality (i.e. publication ready) pictures. This is a must for plotting in Python. Commonly, people use the set of commands in `matplotlib.pyplot`, which generates plots using MATLAB syntax.
    - Seaborn: is another 2D plotting package, based on matplotlib, that adds a ggplot2-ish aesthetics to your graphs.
- **C/C++**: If you feel like learning another programming language, my personal recommendation would be to learn a lower-level programming language like C++. Its main advantage is speed for sure.
- **Other options:** In engineering school they _love_ MATLAB for some reason (maybe they really like to spend a lot of money in paid software?), so this was my first fluent programming language. I recognize that it's very powerful for some tasks and it has a good community of users and packages through MATLAB Central. However, it's way too expensive for me, and I am into open software and open science stuff. Another option is Julia, a high-level and high-performance programming language for scientific computing. This can be an interesting option if you are running computationally intensive code and you don't feel like using C/C++ because it is too "low-level" for you. However, if you are not a method developer usually performance is not an issue you need to worry about that much.

### Where to code

So now that you have decided what language you want to use, the second question is how to actually code.

The first thing to do is to actually install the programming language in your computer using the download link provided on the official webpage. This step is obviously very important.

So where to write your code? Here there are two options: you can either use a text editor or an integrated development environment (IDE). IDEs are text editors on steroids, with several features that make the life of the developer way easier. These features include highlights for syntax in a certain programming language, autocomplete so you don't have to remember all the function and variable names, something to execute your code and debugger. In the other hand, text editors have also evolved, presented several of these fancy features but preserving a more minimal approach.

What tool to choose? It really depends on what you are doing and your personal preferences. Personally, I use a mixture between Atom, Vim, Jupyter, Rstudio, and Eclipse, depending on the programming language and the task at hand. Here an explanation of each one of these:

- **Atom: my favorite text editor.** [Atom](https://atom.io/) has become one of my favorite tools ever. Ok, I'm totally biased in this answer because I'm a real fan and I shamelessly admit that I haven't really tried (beyond a quick look) other text editors. Atom has several packages available, that can allow full customization and versatility. I recommend to install `language-R` (to highlight R syntax), `language-latex` and `latex` (to render LaTeX, markup language vastly used in math), `platformio-ide-terminal` (to have access to a terminal in Mac or Linux), and `hydrogen` (to actually run and visualize Python code in Atom, similar to interactive notebooks). I use it to write Markdown, LaTeX, and Python. In case you don't like Atom, another powerful text editor is [Sublime](https://www.sublimetext.com/).
- **Vim: my favorite text editor in the terminal.** Vim is a very reliable and powerful text editor to edit text in the terminal. In the beginning, it might seem a little complicated, but it is worth the effort. Other alternative text editors for the terminal are nano (less powerful) and emacs (similar to Vim).
- **RStudio to code in R:** very popular IDE for R, that allows you all the fancy things that IDEs do, and even render RMarkdown notebooks. It is a great and friendly option for R programers. Highly recommended. An alternative to RStudio is to use Jupyter notebooks (next bullet point).
- **Jupyter to code in Python.** Jupyter notebooks are increasingly popular in the Python community. They also allow coding in other languages like R, but personally I use it mostly for Python. The same team is creating Jupyter Lab, which is a complete IDE based on Jupyter notebooks style, currently in beta. Jupyter normally runs as a tab in your browser. However, I prefer to use [nteract](https://nteract.io/), which provides Jupyter notebooks as a desktop application (because I'm always fighting with the number of tabs open!). Other alternatives to code in Python are Spyder (available through Anaconda) and PyCharm. I have tried just the former, and it is quite similar to MATLAB.
- **Eclipse to code in C/C++.** Eclipse is a very well-known IDE mostly use for coding in java, but you can code in several other languages using plugins. If you want to code in C++, then you have to install [Eclipse CDT](https://www.eclipse.org/cdt/). Other options are to use [Xcode](https://developer.apple.com/xcode/) (Mac) or [Visual Studio](https://www.visualstudio.com/) (Windows).

### The magic of version control

This is the **key** step that you have to follow to be a happy and healthy programmer. Version control is a system that records changes that you make to your code or any other type of file, and allows you to go back to any previous version. They also allow you to have "parallel universes" with different approaches to your code (which are known as branches). It might not seem very important for you at this point, but **it is important**. It's very likely that you are going to mess your code, believe me. Also, web-based hosting services for version control systems allow working collaboratively in a smooth way.

What version control systems are available? The most popular ones are [git](http://git-scm.com/) and [svn](http://subversion.apache.org/), although lately git is taking over the market.

Most popular web-based hosting services for version control based on git are [GitHub](https://github.com/) (recently acquired by Microsoft), [GitLab](https://about.gitlab.com/) (the only open source), and [Bitbucket](https://bitbucket.org/) (mostly directed to companies).

- **Personal winner:** I use Git and GitHub. Actually our lab obtained an [educational account](https://education.github.com/) for free that works perfectly. We created a private repository for every project and created Markdown files to write down all our pipelines (GitHub renders Markdown). Lately, I have been using mostly the GitHub account as a lab notebook (because that way my PI can see that I'm working, lol). A great option for every lab that does any kind of computational analysis.

### The infallible weapon for debugging

If you are running pipelines or coding, most of your time will be spent debugging and troubleshooting. **That's a fact.** I feel the social responsibility as a colleague to share the most sophisticated tool ever created for this tiresome task: [Rubber Ducking Debugging](https://rubberduckdebugging.com/). Refer to the linked website for a detailed explanation. But, in one sentence:

> Pick a rubber ducky (other objects, pets or humans also do the job) and explain your code line by line. The error will come out.

Infallible.

## Drawing figures

There is one practice in science (especially in biology) that is key for successful research. Some friends and I call it _coloromics_. Coloromics is the fine art of showing your data in an effective, efficient, compelling and aesthetically pleasing way to your audience or readers. Good coloromics can make your research succeed, and conversely, bad coloromics can make your research go unnoticed. So, it is highly recommended to develop some skills to make nice plots that effectively convey the information that you want to share.

- **Personal winner:** My go-to is a combination between `ggplot2` R package and Adobe Illustrator to handle vector drawing. Actually, I really love the latter, but this is because I really like graphic design and digital illustration. That might not be your case, and that is totally fine.
- **Other options:** Python has some good libraries to make nice plots too. The most common package for that is `matplotlib.pyplot`. A friend recently introduced me to `seaborn` which is actually very good. About dealing with images and vector graphics, there are other software available besides Adobe CC. To the best of my knowledge, the best free open-source competitor of Adobe Photoshop is Gimp and the best Adobe Illustrator competitor is Inkscape. Both available for Mac, Windows, and Linux. I think I should be using these tools and supporting free software, but I really really really love Adobe Illustrator. Other option is to use Excel (but if you are reading this, it is probably because you don't want to use Excel anymore).
- **Bonus tip**: If you are dealing with color issues (i.e. bad taste for colors), you can use online color palette builders, for example, [Adobe Color CC](https://color.adobe.com/) or [Coolors](https://coolors.co/). You can find different visually pretty combinations and save the HEX or RGB code to use it later in R or other software.

## Concluding remarks

TL;DR version: I recommend that you use Atom to explore files, create cheat sheets for your preferred programming languages, create a markdown document to use as a lab notebook to write **everything** that you did in your analysis, learn some shell scripting and R or Python (or a little bit of both), if you want to code in R - use R studio, if you want to code in Python - use Jupyter, use GitHub for version control of your code (your future self will thank you), and if your code doesn't work, explain it line by line to a friend and you'll solve all your problems.

## FAQ

- Who are you?
    - Hi, I am Daniela, engineer, computational biologist and bioinformatician (yeah, I like labels). I am part of the Genetics and Genomics PhD program at UC Davis and part of the [Dennis Lab](https://www.dennislab.org/). I work with second and third generation sequencing data identifying the variability landscape of human-specific segmental duplications to investigate their role in human evolution and disease.
- Why did you write this and why should I believe you?
    - I like to make lists and documentation for myself, but I thought that it might also be helpful for friends. So I added more explanations. Why should you believe me? Don't! Try these tools and see what works for you.

---
Comments or suggestions? <i class="fa fa-twitter"></i> [@**dcsoto_cl**](https://twitter.com/dcsoto_cl)
