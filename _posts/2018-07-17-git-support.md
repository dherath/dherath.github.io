---
layout: post
title: "Adding git support to terminal"
comments: false
description: "post 10"
keywords: "git, github, terminal, support"
---

![git-terminal](https://raw.githubusercontent.com/dherath/WebsiteMaterial/master/2018/post_10_git/welcome_image.jpeg){:height="400px"}


Hello Everyone!! Hope everything is going great. In today's post I thought of writing a simple post on how to add `git` support to the terminal. So basically, I'll first start off with a bit of an into on what is **git**. If you do a lot of coding in your day to day life, whether it be in your school, research or work--something that you'd probably agree with me is that debugging code is what takes most of your time. This is where **git** comes in, to put it simply **git** is a version control system and what it does is, it enables us to have keep track of our code base in separate versions.

### What can git do?

I sort of try to think of as keeping save points in a game, so like before we go battle the final boss usually its a good idea to save up. I use git sort of like that, when I know that my code is in some working state before I add anything else, I save or `commit` it's state. So that if I mess up a future version of the code (which usually happens a lot) then I can roll back my code to a past working version. The best part is its not like maintaining folder structure that has folders like `backup OR backup_of_backup/` and so on. Which I admit before using git I did myself. Another cool thing about git is, lets say you have two ideas you could potentially implement to solve the same problem, then it's possible to create whats called `branches` so that you can work on both those versions at the same time. Later on you can integrate what works best to the actual **main** code base. In a nutshell, these are some of the features in **git** that I use most of the time.

To be clear, my post wont be an introduction to **git**, well because there are lots of online tutorials that could probably do a better job than me like this online course on [udacity](https://www.udacity.com/course/how-to-use-git-and-github--ud775){:target="blank"}. It's a free course, and what I'll be presenting today is something I learnt from there.

### Adding git support

If your reading this part of my post, then I'm assuming you have some familiarity with git. if you use some development environment like Eclipse, then its possible to have some indication of what branch your on, or if there are some changes that you have not commited and so on. But if you use the terminal then that sort of support is not in-built so it can get a bit annoying sometimes.

But fear no more, in this post I'll be going through three easy steps on how to add text that automatically show the repository status, whether there are any changed not commited, the branch your on, if a merge is needed and so on. The code Im presenting here isn't my own, and I came across it myself when I was learning on how to use git and it really has made it easy for me to control versions of my code. Since I use a mac, I'll explain it for a mac but the steps for using it in linux is pretty much the same.

### Step 1 





**Prev: [Finding cycles in linked lists]({{site.url}}/2018/Linked-Lists/)**
