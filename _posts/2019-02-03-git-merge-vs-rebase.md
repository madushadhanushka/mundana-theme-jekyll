---
layout: post
title:  "Git Merge vs Rebase"
author: dhanushka
categories: [ git ]
image: https://hashnode.imgix.net/res/hashnode/image/upload/v1555998915146/VyaY8CzvW.jpeg?w=1600&h=840&fit=crop&crop=entropy&auto=format,enhance&q=60
tags: [summer]
---
When you are using git, most probably you may used git merge or git rebase to combine two branches. Pretty much both of these commands do the same thing. But people select either of technique based on their requirements. This post is to compare the difference between git merge vs rebase and when to use.

Here below a diagram that visualize master branch to maintain the main code base and feature branch to develop some feature. You can see that feature branch was create from the master branch. While changes happening in feature branch, master branch also changing with new commits.

![Screen Shot 2019-04-20 at 12.39.02 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1555744226145/Y0TOrCSr-.png)

Once you completed the feature implementation on feature branch, you need to combine it with the latest master branch. Here, you have two options. Either you can merge  or rebase feature branch with the master.

## Git Merge

If you merge two branches, it will create a new commit and combine master branch into the feature branch. Here, feature branch commits keep as it is and commit history does not change. We can represent above digram for git merge command as follows.

![Screen Shot 2019-04-20 at 12.39.42 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1555744252186/s4aDsj9PJ.png)

You can merge master branch into the feature branch by running following command
```
git checkout feature
git merge master
```
or with single line

```
git merge feature master
```

## Git Rebase

Rebase is little different than merge. Rebase apply all feature branch changes on top of master branch by creating new commit for each of its previous commit messages. Which means that rebase command will change your commit history and regenerate commits again on top of master branch. Final output of git rebase can be represent as follows.

![Screen Shot 2019-04-20 at 12.39.27 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1555744245792/5lb0ci21x.png)

Following command can be used to rebase feature branch on top of master branch. "-i" option used for interactive rebase. Otherwise you can simply use "git rebase  master".
```
git checkout feature
git rebase -i master
```

## Rebase or Merge
You can use either rebase or merge to combine two branches. Peoples are tend to use rebase over merge due to following facts.
1. There is no additional commit added to the merged branches
2. Rebase commit history is cleaner than merge history since rebase history does not have complex branches
3. Due to the branch complexity in merged git tree, some code changes are invisible. But rebase changes come from a specific and entitled commit.
4. Rebase make easier to use git log, git bisect, and gitk commands.

## When to not to use Rebase
As we already discussed, rebase change the commit history. Therefore, it should not be apply on the public branches(eg: master) where other people are working on. This make git confuse that your master branch diverge from others master branch.

## Conclusion
Both merge and rebase can be used to combine two branches. Merge command just unify your work with a commit without changing history. While rebase apply feature branch changes on top of master branch and change the history. If you prefer to have clean history, then you can use rebase. If you need to preserve the history changes, then merge would be the best choice. 

Hope, this article helps you to learn the difference of git merge and git rebase. 
Comment down what is your preference and the reason. See you with another article. Cheers :). 


# References
[1] [https://www.atlassian.com/git/tutorials/merging-vs-rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)