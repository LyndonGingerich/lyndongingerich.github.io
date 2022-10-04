---
layout: post
title:  "Post-Merge Hook for Deleting Local Merged Branches"
date:   2022-09-22 02:01:30 -0500
categories: git
---

Many Git repository hosts will automatically delete remote branches after they are merged into `main`, but I've had to clean up their local counterparts manually--until today. Here's the code for the post-merge commit hook:

```bash
#!/bin/bash

main_name="main"

main_head=$(git log -n 1 --pretty=format:"%H" $main_name)

original_branch=$(git branch --show-current)

original_commit=$(git rev-parse HEAD)

git checkout $main_name

for branch in $(git branch --merged "$main_head" | tr -d '*')
do
    if [[ $branch != "$main_name" ]]
    then
        git branch -d "$branch"
    fi
done

if [[ $original_branch == "" ]]
then
    git checkout "$original_commit"
else
    git checkout "$original_branch"
fi
```

Just substitute your own main branch name for the value of `main_name`.

For those not familiar with Git hooks, save this code in your repository as `.git\hooks\post-merge`, making sure to [give it the appropriate permission](https://www.liquidlight.co.uk/blog/using-a-post-merge-git-hook-to-clean-up-old-branches/).

Thanks to [Rahul Tapali on StackOverflow](https://stackoverflow.com/a/15679298/13312697) for the command to get the latest commit from a branch.

If you see a potential improvement, send me a pull request!
