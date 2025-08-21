# About pull requests
A pull request is a proposal to merge a set of changes from one branch into another.
Anyone with read access to a repository can create a pull request.
## About collaborative development models
https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/getting-started/about-collaborative-development-models#fork-and-pull-model
### a. Fork and pull model
1. Accessibility
 - Be aware that a fork and its upstream share the same git data. 
 - This means that all content uploaded to a fork is accessible from the upstream and all other forks of that upstream.
2. Collaboration
 - You do not need permission from the upstream repository to push to a fork of it you created. 
 - You can optionally allow anyone with push access to the upstream repository to make changes to your pull request branch.
3. This model is popular with open-source projects

#### Point
- 你在 fork 上傳的 commit，不是只有你看得到，而是 upstream 和其他 fork 也能看到。
- 送 PR 時，勾選「Allow edits from maintainers」。 這樣 upstream 的維護者就能幫你改 branch，例如修小錯誤或調整格式，不需要你自己再改一次。
- Fork → 開發 → Push → Pull Request → Review → Merge


### b. Shared repository model
1. **collaborators are granted push access** to a single shared repository and **topic branches are created when changes need to be made.**(e.g. feature/login) 
2. Pull requests are useful in this model as they initiate code review and general discussion about a set of changes before the changes are merged into the main development branch.
3. This model is more prevalent with small teams and organizations collaborating on private projects.

#### Point
- 雖然大家都有 push 權限，但最好不要直接推到 main/master 分支。
- 做法是：開一個 分支 → 開發 → Push → PR → Review → Merge



# Practice how to make an PR
Here's two github project guide you how to make your first contribution.
[first-contributions](https://github.com/halzq/first-contributions/blob/main/README.md)
[code-contributions](https://github.com/Roshanjossey/code-contributions/pulls)
[Creating a pull request from a fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork)

## steps
```bash
# Fork + Clone
git clone https://github.com/你的帳號/專案.git
cd 專案
git remote add upstream https://github.com/原作者/專案.git

# 建新分支修改
git switch -c feature-branch
# (修改檔案)
git add . # stage
git commit -m "新增功能或修正 bug" # commit
git push -u origin feature-branch # push to origin
# the -u stands for --set-upstream. It links your local branch with the remote branch you’re pushing to.

# → 然後到 GitHub 開 PR
# go to your github origin repo
# find the button "Compare and pull request"
# submit a PR
```

### where to find your PR history
1. 打開你的 GitHub 頁面，例如：
https://github.com/<你的帳號>


2. 點選上方的 Pull requests 分頁。
網址長這樣： https://github.com/pulls

3. 這裡會顯示你建立或參與過的所有 PR（跨所有 repo，不管是 upstream 還是 origin）。

### compare the branches
* Your topic branch (also known as “feature branch”) is the branch where you’re making your changes in your forked repository (e.g. my-topic-branch).
* The base branch is the branch in the upstream (central) repository that you want to merge your changes into (e.g. main).
* The pull request compares the changes proposed by the topic branch (my-topic-branch) with the base branch (main), so my-topic-branch is known as the “compare branch”.

```txt
[the branch of upstream you want to merge to] <- [your feature branch]
```



# [Continuing making changes to files in your pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request?tool=desktop#making-changes-to-files-in-your-pull-request)
After you have opened your pull request, you can continue making changes to the files **by adding new commits** to your head branch.
(head branch is the one which you make an PR on)

* head branch
    → 就是你用來開 PR 的那個分支（例如 feature-abc）。

* add new commits
    → 你在本地端繼續修改檔案，git add → git commit → git push 到同一個分支。

→ GitHub 會自動把這些新 commit 加進你原本的 PR 裡，PR 內容會更新，不需要再另外開一個新的 PR。

## Steps
1. you have made an PR：
origin/feature-abc → upstream/main

2. Reviewer says：
請修正文件格式，還有多加一個測試。

3. 你在"本地" feature-abc 分支修改and push to origin
```bash
git add . #(or specified file name)
git commit -m "Fix docs and add test"
git push -u origin feature-abc #(This have to be your feature branch / head branch) 
```

3. 這個新 commit 會自動出現在你已經開的 PR 裡。

e.g. code-contribution
```bash
git add contributors\halzq.html       
git commit -m "continue making changes and test pull request"
> [add-halzq 520fb11] continue making changes and test pull request
> 1 file changed, 2 insertions(+), 1 deletion(-)
git remote -v
>origin  https://github.com/halzq/code-contributions.git (fetch)
>origin  https://github.com/halzq/code-contributions.git (push)
>upstream        https://github.com/Roshanjossey/code-contributions.git (fetch)
>upstream        https://github.com/Roshanjossey/code-contributions.git (push)
git push -u origin add-halzq
> Enumerating objects: 7, done.
> Counting objects: 100% (7/7), done.
> Delta compression using up to 16 threads
> Compressing objects: 100% (4/4), done.
> Writing objects: 100% (4/4), 484 bytes | 484.00 KiB/s, done. 
> Total 4 (delta 3), reused 0 (delta 0), pack-reused 0 (from 0)
> upstream        https://github.com/Roshanjossey/code-contributions.git (push)
```



# [Enabling repository maintainer permissions on existing pull requests](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/allowing-changes-to-a-pull-request-branch-created-from-a-fork)

When you open a Pull Request from your fork to the upstream repo, GitHub shows you a checkbox option:
> Allow edits by maintainers

Normally this just means the upstream maintainers can push commits directly to your PR branch (on your fork) — useful if they want to fix small things.

## Security
If you allow maintainers to edit your PR branch, and your fork has GitHub Actions workflows, then they also get the ability to edit your workflows.

Editing workflows could expose your secrets (sensitive values stored in your fork’s settings) and give them more access to your repo than you might expect.



# [Comparing commits](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/viewing-and-comparing-commits/comparing-commits)

You can compare the state of your repository across branches, tags, commits, forks through **changing the path**. 

[first, find the page for compare.]((https://docs.github.com/en/repositories/releasing-projects-on-github/comparing-releases))

## Comparing branches
The most common use of Compare is to compare branches, such as when you're starting a new pull request.

To compare different versions of your repository, **append /compare to your repository's path.**

e.g
> https://github.com/octocat/linguist/compare/master...octocat:linguist:an-example-comparison-for-docs

This means that we are comparing master branch and an-example-comparison-for-docs branch under octocat/linguist repository.

## [Comparing tags]
e.g
> https://github.com/octocat/linguist/compare/v2.2.0...octocat:v2.3.3

we are comparing base:v2.2.0 <- compare:v2.3.3

## Comparing commits
To quickly compare two commits or Git Object IDs (OIDs) directly with each other in a **two-dot diff comparison** on GitHub, edit the URL of your repository's "Comparing changes" page.

For example, 
this URL uses the shortened SHA codes to compare commits f75c570 and 3391dcc: 
> https://github.com/github-linguist/linguist/compare/f75c570..3391dcc.

## Comparing across forks
You can also preface the branch name with a user name and a repository name. For example, specifying octocat:awesome-app:main would use the main branch in the octocat/awesome-app repository

e.g.
> https://github.com/6un9-h0-Dan/linguist/compare/master...1974kpkpkp:linguist:master

>  6un9-h0-Dan/linguist: master < 1974kpkpkp/linguist:master

## Comparisons across commits
You can compare a single commit in Git to the commit's predecessors using two types of notation.
>96d29b7^^^^^
>> Represents the commit five commits prior to 96d29b7.
>> https://github.com/octocat/linguist/compare/octocat:96d29b7%5E%5E%5E%5E%5E...octocat:96d29b7

> 96d29b7~5
>> Represents the commit five commits prior to 96d29b7.
>> https://github.com/octocat/linguist/compare/octocat:96d29b7%7E5...octocat:96d29b7





# [Three-dot and two-dot Git diff comparisons](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-comparing-branches-in-pull-requests#three-dot-and-two-dot-git-diff-comparisons)

```
A -- B -- C  (main)
       \
        D -- E  (feature)
```
## Three-dot Git diff comparison
The three-dot comparison shows the difference between the latest common commit of both branches (merge base) and the most recent version of the topic branch.
* git diff main..feature
- Comparing C (base latest commit) and E (topic latast commit)


## Two-dot Git diff comparison
The two-dot comparison shows the difference between the latest state of the base branch (for example, main) and the most recent version of the 
topic branch.
* git diff main...feature
- Comparing B (common ancestor) and E (topic latast commit)


### Conclusion
Two-dot (..) → 看兩個分支的 最終差異，適合 **合併前的狀態比對**。
Three-dot (...) → 看 某分支自分岔以來的改動，適合 **PR / code review**。

### Solution: Merging often
- To avoid getting confused, merge the base branch (for example, main) into your topic branch frequently. 
- By merging the base branch, the diffs shown by two-dot and three-dot comparisons are the same. 
- We recommend merging a pull request as soon as possible.
- This encourages contributors to make pull requests smaller, which is recommended in general.

情境 1：你直接在公司/團隊的 主 repo 開發
```bash
git fetch origin
git checkout topic
git merge origin/main   # 或 git rebase origin/main
```

情境 2：你在 Fork 的 repo 開發（典型 GitHub 開源協作）
```bash
# 第一次設定 upstream
git remote add upstream https://github.com/official/project.git

# 取得 upstream 的最新更新
git fetch upstream

# 把官方的 main 合併回你的分支
git checkout topic
git merge upstream/main   # 或 git rebase upstream/main

# 4. 把更新後的分支 push 回自己的 repo (fork)
git push origin topic

# 5. make PR
```