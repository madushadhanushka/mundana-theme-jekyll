---
layout: post
title:  "Draw image on Github contribution graph"
author: dhanushka
categories: [ programming ]
image: https://hashnode.imgix.net/res/hashnode/image/upload/v1560259478072/X1wfy4f-v.jpeg?w=1600&h=840&fit=crop&crop=entropy&auto=format,enhance&q=60
---
Did you see the Git contribution graph of my Github account at 2016. Check this out [here](https://github.com/madushadhanushka?tab=overview&from=2016-12-01&to=2016-12-31). It print my name. This blog post is to tell you how I did it along with some underlying Git concept that might help for you as well.

![Screen Shot 2019-06-11 at 1.43.28 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1560240824616/pJLAEMLzz.png)

Github provide a way to represent your daily commitment as a graph. Github introduce this contribution graph as a measurement of daily contribution. For me, I take this feature as a motivation factor to do more commits. Lot's of contribution doesn't mean that those contribution are worth. But somehow it give some idea about the contribution you have done to the open source community.

## How Git Internally works
As programmers we use Git to save last successful state of a code. Git has simple way of keeping and versioning history in Git repository. Git keep data as combination of following objects.
- Blob : This object used to store content of single file
- Tree : Reference to another blog or sub-tree
- Commit : Commit data (Auther, Commiter ect) and reference to tree object
- Tag :  Reference to Commit object.

Blob is nothing more than a file that you have changed. Whenever you commit content into a Git repository, it will compress the changed files into a Blob type object. then it generate hash value for it. While, Git also create another object called Tree and keep reference to Blob object. If there are many files that changed, then Git generate many Blob and hash values for each of the changed files. It also generate another object called tree, to track all changed files. Once you did the commit, It generate another Object called Commit Object. This commit object will  keep reference to tree Object.

Once you change another file after the first commit, Git will again check for the change file and create new Blobs and Trees for changed files. Then it create new Commit Object that point to the Tree object. It also keep are reference to previous commit by using field called parent. 

Here's an example.


![gitinternal (2).jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1560240518713/6VeexTnO7.jpeg)

In this example, we have two files (text1.txt and text2.txt). Commits represented in green color. tree and blob represented in yellow and purple colors respectively. For the first commit(34c32) there is a tree(3a2d32) associated with it to track files. In this commit there are two files are available(4390a9 and 45c321). For the next commit, we are changing text2.txt file. Since its content changed, it generate new blob with new hash id(53a234). New commit have new tree(34c32) and the commit also pointing to previous commit by parent commit  hash.

If you read the Commit Object content with the following command, Content would be something like follows.

`git cat-file -p 1658642a6c164700c880d499da0b874c18829883`

Here "1658642a6c164700c880d499da0b874c18829883" is the commit hash id.

```
tree 03de692bf6a38ac9c98bac37dc27534fbaf020b6
parent 5436b80815fde902030d71f08957f68a366dd91f
author Dhanushka Madushan <dhanu@gmail.com> 1559998289 +0530
committer Dhanushka Madushan <dhanu@gmail.com> 1559998289 +0530
Initial commit
```
Here, Git maintain author name and the time of commit marked. As you can see, there are two timestamps in Commit object.
- Author Date: This is the timestamp when you commit the message. Once author date set, it will not change ever again.
- Commit Date: This date could be change when you rebase the commit.


## How to draw a pixel
Image is a composition of many pixel. Let's see, how to draw a pixel in contribution graph. First thing you need to do is select a git repository. This should not be a forked repository. Github doesn't count contribution for forked repository unless changes merged into original repository. Thus, remember to use original repository.
Github measure contribution by based on following facts.

- Committing to a repository's default branch or gh-pages branch
- Opening an issue
- Proposing a pull request
- Submitting a pull request review
- Co-authoring commits in a repository's default branch or gh-pages branch

Here I used first method since I can change the history by changing commits. First, I created a new file in the repository and added some random words. Then it commit. Then I took the last commit hash id by running `git log` command. Now I can put whatever date into the commit message by running following command. It replace commit hash with previously extracted commit hash.

```
git filter-branch -f --env-filter \
    'if [ $GIT_COMMIT = 943f032ac12f386ae6e9e9d14f9e1a4e269a16a4 ]
     then
         export GIT_AUTHOR_DATE=“Fri Jun 03 21:38:53 2016 -0800"
         export GIT_COMMITTER_DATE="Fri Jun 03 21:38:53 2016 -0800"
     fi'
```

When `git log` executed again, we can see the relevant commit message change it author and commit date.
Now these changes can be push into the remote branch. Since we change the commit history, Changes cannot be push with `git push origin master`. Changes should be push by force with "-f" option. Thus, the command would be `git push origin master -f`

> Warning: Once you push your changes to the Github, contribution graph draw according to the whole commit history. Always remember that you cannot remove contribution from the commit history. Which means, you can only add contribution to the Github. You cannot delete the contribution. Contribution will be permanent.

## Drawing on already contributed graph
Github contribution graph represent contribution by color scale from dark green to light green. Dark green means higher contribution and light green means lower contribution. Color scale generated dynamically, based on number of contribution done for the selected one year period. In my this year contribution graph, I have around 2000 contribution.  To print a dark dot in my contribution graph, I have needed at least 40 contribution for single day. Which means, I need to run above script 40 times. So I have created a script to generate many commit with following script.
This script will generate 100 commit messages.
```
#!/bin/bash
# Basic while loop
counter=1
while [ $counter -le 100 ]
do
echo $counter>>file.txt
echo $counter
git add file.txt
git commit -m "commit $counter"
((counter++))
done
echo All done
```

I ran following script to generate many commit massage for the same day. Number of commit per day can be change with `modcommit` variable in the script. Ten commit for ten days means 100 commit. This script read previous 100 commit and change commit timestamp history as it defined in `arr[i]` array.
```
modcommit=10
arr[0]="Mon Jul 16 21:38:53 2018 -0800"
arr[1]="Fri Jul 20 21:38:53 2018 -0800"
arr[2]="Thu Jul 19 21:38:53 2018 -0800"
arr[3]="Wed Jul 18 21:38:53 2018 -0800"
arr[4]="Fri Jul 27 21:38:53 2018 -0800"
arr[5]="Mon Jul 23 21:38:53 2018 -0800"
arr[6]="Mon Jul 30 21:38:53 2018 -0800"
arr[7]="Fri Sep 28 21:38:53 2018 -0800"
arr[8]="Thu Sep 27 21:38:53 2018 -0800"
arr[9]="Wed Sep 26 21:38:53 2018 -0800"

fix_commit_date() { 
    echo "commit id $1"
    echo "date $2"
    git filter-branch --env-filter \
    "if [ \$GIT_COMMIT =  ${1} ]
     then
         export GIT_AUTHOR_DATE=\"${2}\"
         export GIT_COMMITTER_DATE=\"${2}\"
     fi" -f
}


rm commit.txt
git log --pretty=%H>commit.txt
COUNTCOMMITS=$(awk 'END {print NR}' commit.txt)
echo $COUNTCOMMITS
input="commit.txt"
count=0
while IFS= read -r line
do
  dateid=$((count / modcommit))
  AUDATE=${arr[dateid]}
  echo "$line"
  DATE2="$( echo "${AUDATE}")"
    fix_commit_date $line "$AUDATE"

     ((count++))
  if [[ "$count" == '100' ]]; then
    break
  fi
  echo $TODO
  $($TODO)
echo ""
```
You can change this script as you want to add many contributions for an array of days. If you are trying out this, I recommend to do it for older year contribution graph. If you add a contribution to the graph, it would be permanent. Hope this article may also help you to understand underlying Git concept. Join with me on [twitter](https://twitter.com/dhanushkadev) to read more interesting tech stuff. See you in next article. Cheers :) 