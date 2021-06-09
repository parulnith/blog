---
toc: false
layout: post
description: Streamline your data science code repository and tooling quickly and efficiently
comments: true
categories: [Data Science]
image: images/2021-06-7-Automate your data science project structure in three easy step/0.png
show_image: false
show_tags: true
title: "Automate your data science project structure in three easy steps"
---

*The article was originally published [here](https://towardsdatascience.com/automate-your-data-science-project-structure-in-three-easy-steps-277c92328d24?sk=72df9f0f306dd6deb4be757008e3b956f)*



![](https://cdn-images-1.medium.com/max/2000/1*z0VoWoaLTXXPv2MN_7b1GQ.png)

<sub>Free Vector illustrations from [Scale](https://2.flexiple.com/scale/all-illustrations?search=code&gender-option-field=Female%7CMale%7CBoth)

> # Good Code is its own best documentation

[Dr. Rachael Tatman](https://twitter.com/rctatman?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor), in one of her [presentations](http://www.rctatman.com/files/Tatman_2018_ReproducibleML.pdf), highlighted the importance of code reproducibility in a very subtle way :
>  “Why should you care about reproducibility? Because the person most likely to need to reproduce your work… is you.”

This is true on so many levels. Have you ever found yourself in a situation where it became difficult to decipher your codebase? Do you often end up with multiple files like untitled1.py or untitled2.ipynb? Well, if not all, a few of us must have undoubtedly faced the brunt of bad coding practices on few occasions. The situation is even more common in data science. Often, we limit our focus on the analysis and the end product while ignoring the quality of the code that is responsible for the analysis.

Why is reproducibility a vital ingredient in the data science pipeline? I have touched upon this topic in [another blog post](https://towardsdatascience.com/getting-more-out-of-your-kaggle-notebooks-fb2530ece942?sk=99d718e3b75d8de58e4c1fb23cdc09c4), and I’ll borrow a few lines from there. A reproducible example allows someone else to recreate your analysis using the same data. This makes a lot of sense since you put your work out in the public for them to use. This purpose gets defeated if others cannot reproduce your work. In this article, let’s look at three useful tools that can streamline and help you in creating structured and reproducible projects.

## Creating a good project structure

Let’s say you want to create a project which contains code to analyze the sentiments of the movie reviews. There are three essential steps to create a good project structure:

![](https://cdn-images-1.medium.com/max/2294/1*TwzEaKcZUff8VQkt6ooGsw.png)
<sub>The pipeline of creating a project template | Image by Author

### 1. Automating project template creation with [Cookiecutter Data Science](https://github.com/drivendata/cookiecutter-data-science)

![[](https://thenounproject.com/term/baking/2870320) 
<sub> Icon by @NounProject| CC: Creative Commons](https://cdn-images-1.medium.com/max/2000/1*Gw61dGYG48pd5VO3srkgGg.png)

There is not a clear consensus in the community on best practices for organizing machine learning projects. That is why they are a plethora of choices, and this lack of clarity leads to confusion. Fortunately, there is a workaround, thanks to people at DrivenData. They have created a tool called **Cookiecutter Data Science** which is a [standardized but flexible project structure for doing and sharing data science work](https://github.com/drivendata/cookiecutter-data-science). A few lines of code set up a whole series of subdirectories and make it easier to start, structure, and share analysis. You can read more about the tool on their [project home page](http://drivendata.github.io/cookiecutter-data-science/). Let’s get to in interesting part and see it in action.

### Installation

    pip install cookiecutter

    or

    conda config --add channels conda-forge
    conda install cookiecutter

### Starting a new project

Head over to your terminal and run the following command. It will automatically populate a directory with the required files.

    cookiecutter [https://github.com/drivendata/cookiecutter-data-science](https://github.com/drivendata/cookiecutter-data-science)

![](https://cdn-images-1.medium.com/max/2210/1*w-_2fdm2vXINDfg7j5m10Q.gif)
<sub> Using Cookiecutter DataScience | Image by Author

A sentiment Analysis directory gets created on the specified path, which in the above case is the Desktop.

![The directory structure of the newly created project | Image by Author](https://cdn-images-1.medium.com/max/2000/1*XNDkQBEsy07bHOlQNHohig.png)
>  **Note** : Cookiecutter data science will be moving to version 2 soon, and hence there slight change in how the command is used in the future. This means you will have to use *ccds ...* rather than *cookiecutter ... *in the command above. As per the Github repository, this version of the template will still be available but one would have to explicitly use *-c v1* to select it. Keep an eye on the [documentaion](https://github.com/drivendata/cookiecutter-data-science#new-version-of-cookiecutter-data-science), when the change happens.

## Creating a good Readme with [readme.so](https://readme.so/)

![[Icon by @NounProject](https://thenounproject.com/search/?q=Page&i=2359483) | CC: Creative Commons](https://cdn-images-1.medium.com/max/2000/1*pFC6ZB0FMVita5OHWVpF_g.png)

After creating the skeleton of the project next, you need to populate it. But before that, there is an important file to be updated — the [README](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-repository-on-github/about-readmes). A README is a markdown file that communicates essential information about your project. It tells others what the project is about, the project’s license, how others can contribute to the project, etc. I have seen many people putting tremendous effort into their projects but failing to create decent READMEs. If you are one of them, there is some good news in the form of a project called [**readme.so](https://readme.so/).**

A good soul has just put an end to writing READMEs manually. [Katherine Peterson](https://twitter.com/katherinecodes) recently created a simple editor allowing you to create and customize your project’s readme quickly.

 <iframe src="https://medium.com/media/c1ab59be4e3029a30adae1cf3dd6577a" frameborder=0></iframe>

The editor is pretty intuitive. You only need to click on a section to edit the content, and the section gets added to your readme. Choose the ones you like from an extensive collection. You can also move the sections depending upon the location where you want them on the page. Once you have all things in place, go ahead and copy the content or download the file and add it to your existing project.

![Generate automatic READMEs with readme.so | Image by Author](https://cdn-images-1.medium.com/max/3126/1*Le7xvk0HTxsGR-_xb6eNvA.gif)

## Push your code to Github

![[Icon by @NounProject](https://thenounproject.com/search/?q=Github&i=2346914) | CC: Creative Commons](https://cdn-images-1.medium.com/max/2000/1*7cBYwVhMG_NSHLXifrkmeg.png)

We are almost done. The only thing left is to push the code to Github(or any version control platform of your choice). You can do that easily via Git. Here is a handy cheat sheet containing the [most important and commonly used Git commands for easy reference.](https://education.github.com/git-cheat-sheet-education.pdf)

 <iframe src="https://medium.com/media/58585761cded8c233f1568e936719f27" frameborder=0></iframe>

Alternatively, if you use [Visual Studio Code](https://code.visualstudio.com/)(VS Code), like me, it is already taken care of. VS Code makes it possible to publish any project directly to GitHub without having to create a repository first. VS Code will create the repository for you and control whether or not it should be public or private. The only thing required from your side is to provide authentication to GitHub through VS Code.

![Pushing Code to Github via Visual Studio Code | Image by Author](https://cdn-images-1.medium.com/max/3588/1*XCJ5_8uE1n8B8jf3iUWRAw.gif)

That is all you need to set up a robust and structured project base. All the above steps have been summarized in the following video in case you want to look at all the steps in sync.

 <iframe src="https://medium.com/media/482da1aaaf65139b92d6f68f8b29b328" frameborder=0></iframe>

## Conclusion

Creating structured and reproducible projects might seem difficult in the beginning but offer advantages in the long run. In this article, we looked at three useful tools that can help us in this task. While **cookiecutter data science** gives a clean project template, **readme.so** automatically populates a readme file. Finally, the VS Code can help us push the project onto the web for source control and collaboration. This creates the necessary foundation for a good data science project. Now you can begin working on your data and derive insights from it to be shared with various stakeholders.
