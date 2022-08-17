---
layout: post
title:  "Speed-Stacking Branches"
date:   2022-08-17 09:06:30 -0500
categories: git
---

Jerry has two branches, a feature and a refactor. He has worked hard all week, but now they are finally ready for submission. Jerry leans back in his chair and grins with anticipation. But suddenly, a realization jerks him upright. His feature slightly modified function `foo`, but his refactor moved function `foo` to a completely different part of the code. A devious merge conflict--but not quite devious enough, for he had noticed the trap before sticking his leg into it. And without even looking at the code! He must be improving in branch management.

No problem will be seen here. Jerry can simply rebase his refactor branch atop his feature branch. But Arnie, the repository maintainer and reviewer of all pull requests, understandably dislikes trying to sort out multiple diffs at once, so Jerry will leave the refactor pull request a draft until the feature is merged. Then he can merge `main` into the refactor branch to sort out the diff and publish away.

But as his mouse cursor hovers over the "Force Push" button, a notification pops onto the screen. Jerry has been assigned to resolve an urgent bug--and in function `foo`, of all places!

What a mess. The bug takes priority, but what about all his hard work? The feature is no problem. Arnie reviews all open pull requests every day at 2:00 PM, and fixing the bug will take at least until 3:00. But the refactor was going to subtly shift a paradigm so as to allow a simplification of the entire module! Jerry doesn't want to have to rethink the whole branch again. What to do?

Jerry feels that he should probably create a pull request for the feature, then fix the bug, and figure out the refactor later. It seems the responsible thing to do somehow--keeping everything organized and in its place, with no merge conflicts.

But wait. Arnie trusts his few contributors reasonably and hates redundant approvals, so his policies do not reset his approval of a pull request when new changes are pushed to its branch. What if Jerry were simply to submit both the feature and the refactor PRs immediately and resolve the merge conflict once one was merged into `main`? Arnie would still review both the modification and the move of function `foo`, just not in concert. Then both branches will be merged soon after 2:00, allowing regretless debugging.

***

So yes, I've done what Jerry is considering here. It feels a little like a hack, but it seems to work, and so long as I don't modify the code substantially while resolving conflicts, what's the harm? Our goal is to ship good code. If we can get the code shipped without losing its quality, we win.

Or maybe I'm horrendously wrong here. I haven't figured out comments yet, so if you want to respond, I guess you should post on your own blog and email me the link. (You do [have your own blog]({% post_url 2022-08-16-f1rst-p0st %}), right?)