---
layout: post
title: "Adding git support to Terminal"
comments: false
description: "post 10"
keywords: "git, github, terminal, support"
---

![github_helper]({{site.url}}/material/2018/post_10/github_helper.jpeg?raw=true){:height="400px"}

Hello Everyone!! Hope everything is going great, I know its been sometime since I last posted anything, had a super busy semester. Anyways in todays post I thought of writing about adding `git` support to a terminal. This post is more of a **'How to?'** post, and not really an introduction to `git`. So if you have no idea what **git** is all about and you program alot, then I think you should really consider learing it, and heres why... 

>
In a nutshell, git is a version control system that programmers use to keep track of their code.

Once you start working on big projects with potentially thousands of lines of code, it becomes quite unbearable to keep track of every change one would make. Specially when one small change could potentially break the entire program. By using `git` one is able to keep versions of the same code before any significant modification, so if something bad happens and the code breaks its always possible to roll back and re-try changing the code starting off from a **correct** version. I actually learned about git not more than a year ago and it really is a life saver. I learned about git from an online free course provided by Udacity. Click [here](https://www.udacity.com/course/how-to-use-git-and-github--ud775) to check this course out. In fact, the neat trick about adding git support to terminal is also something I picked from there. 

If you are someone who is already familiar with `git`, and you only want to know how get this working then read on. But before all of that, you might wonder...

#### "What kind of features will this add?"

As you can see in the image above, if you follow the steps I mention in this post, you can view helpful git debugging information in the terminal itself as shown in the image above, which shows the status of my github repo for this website. This includes,

**`1. The current git branch`:**The git branch you're checked in is shown in green inside parenthisis. In my case, I'm checked into a branch for this post called **post_10**.

**`2. Un-commited/added changes`:**If there is any change that is not commited or added, it will be shown as a _green_ **`*`** symbol right next to the branch name. In my case, the _feed.xml_ file is modified and not commited, so there is a asterix shown.

**`3. Changes added but not commited`:**
Symilar to the above case, if there are any changes that are _added_ but not commited its shown as a **`+`** symbol. In my example, after adding the changes with `git add --all` the symbol changes from * to +.

**`4. Merge status`:**
After pulling from a branch, if a merge is required then an additional text as **`| MERGE`** will show right next to the branch name.

So as you can see, this automatic notifications inside the terminal itself really helps out when you code. Now there are two methods of adding this functionality to you're terminal, depending on wether you are using a _mac_ or some _linux_ destribution.

#### Steps if Mac 

1. Download this [file](https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash) into your home directory and name it as **`git-completion.bash`**.
2. Download this [file](https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh) into your home directory and name it as **`git-prompt.bash`**.
3. In your home directory if there is a file called `.bash_profile`, then copy the contents of the code below into it. If not then create a new file called `.bash_profile` and copy this code into it. (_Note that these colors work best when the background is white or a light color, You can change the color scheme to your taste_)

```sh
# Enable tab completion
source ~/git-completion.bash

# colors for the notifications
green="\[\033[0;32m\]"
blue="\[\033[0;34m\]"
purple="\[\033[0;35m\]"
reset="\[\033[0m\]"
 
# Change command prompt
source ~/git-prompt.sh
export GIT_PS1_SHOWDIRTYSTATE=1
export PS1="$purple\u$green\$(__git_ps1)$blue \W $ $reset"
```

#### Steps if Linux Destribution

+ If you are working on a linux destribution, then there is only one change that is required. First of all follow steps 1 and 2 as is. Afterwards, copy the above code snippet (_after changing the color scheme if needed_) into a file called `.bashrc`(not _.bash_profile_).

After all these steps are complete, then restart a new terminal and this should start working. Hope this makes it easy when working with git repositories.

##### So until next time,
##### Cheers!

**Prev: [Finding cycles in linked lists]({{site.url}}/2018/Linked-Lists/)** \\
**Next: [Time series prediction with Recurrent Neural Networks]({{site.url}}/2018/time-series-prediction/)**


<!--+ **the current git branch**: The git branch you're checked in is shown in green inside parenthisis. In my case, I'm checked into a branch for this post called **post_10**.
+ **un-commited changes**: If there is any change that is not commited or added, it will be shown as a _green_ **`*`**(asterix) symbol right next to the branch name. In my case, the _feed.xml_ file is modified and not commited, so there is a asterix shown.
+ **changes added but not commited**: Symilar to the above case, if there are any changes that are _added_ but not commited its shown as a **`+`** symbol. In my example, after adding the changes with `git add --all` the symbol changes from * to +.
+ **merge status**: After pulling from a branch, if a merge is required then an additional text as **`| MERGE`** will show right next to the branch name.

<!--the current git branch, an indication to whether a change was made or commited and so on. In this image you can see some text in green right next to my name in the prompt. This green text is what Im talking about.


 In today's post I thought writing a simple post on how to add `git` support to the terminal. So basically, I'll first start off with a bit of an into on what is **git**. If you do a lot of coding in your day to day life, whether it be in your school, research or work--something that you'd probably agree with me is that debugging code is what takes most of your time. This is where **git** comes in, to put it simply **git** is a version control system and what it does is, it enables us to have keep track of our code base in separate versions.

### What can git do?

I sort of try to think of as keeping save points in a game, so like before we go battle the final boss usually its a good idea to save up. I use git sort of like that, when I know that my code is in some working state before I add anything else, I save or `commit` it's state. So that if I mess up a future version of the code (which usually happens a lot) then I can roll back my code to a past working version. The best part is its not like maintaining folder structure that has folders like `backup OR backup_of_backup/` and so on. Which I admit before using git I did myself. Another cool thing about git is, lets say you have two ideas you could potentially implement to solve the same problem, then it's possible to create whats called `branches` so that you can work on both those versions at the same time. Later on you can integrate what works best to the actual **main** code base. In a nutshell, these are some of the features in **git** that I use most of the time.

To be clear, my post wont be an introduction to **git**, well because there are lots of online tutorials that could probably do a better job than me like this online course on [udacity](https://www.udacity.com/course/how-to-use-git-and-github--ud775){:target="blank"}. It's a free course, and what I'll be presenting today is something I learnt from there.

### Adding git support

If your reading this part of my post, then I'm assuming you have some familiarity with git. if you use some development environment like Eclipse, then its possible to have some indication of what branch your on, or if there are some changes that you have not commited and so on. But if you use the terminal then that sort of support is not in-built so it can get a bit annoying sometimes.

But fear no more, in this post I'll be going through three easy steps on how to add text that automatically show the repository status, whether there are any changed not commited, the branch your on, if a merge is needed and so on. The code Im presenting here isn't my own, and I came across it myself when I was learning on how to use git and it really has made it easy for me to control versions of my code. -->
