# Fork a repository (如何實際操作fork)
https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo?tool=desktop
For example, you can use forks to propose changes related to fixing a bug.
Rather than logging an issue for a bug you have found, you can:

1. Fork the repository.
2. Make the fix.
3. Submit a pull request to the project owner.

## I. Forking a repository (一 fork)
1. On GitHub, navigate to the octocat/Spoon-Knife repository.
在 GitHub 上，前往 octocat/Spoon-Knife 儲存庫。

2. In the top-right corner of the page, click Fork.
在頁面右上角，點擊 Fork。

3. Then this repository would be forked to your own github account.
這樣就會被fork到我的帳號內了

## II. Cloning your forked repository (二 clone)
This step is to have the files in that repository locally on your computer.

1. On GitHub, navigate to your own fork of the Spoon-Knife repository.

2. Above the list of files, click <> Code. Copy the URL for the repository.

3. Open terminal and type
```bash
git clone https://github.com/YOUR-USERNAME/Spoon-Knife
```

4. Press Enter. Your local clone will be created.

## III. sync your fork with the upstream repository (三 remote add)
When you fork a project in order to propose changes to the upstream repository,
you can configure Git to pull changes from the upstream repository into the local clone of your fork.
1. look up the status
```bash
$ git remote -v
> origin  https://github.com/YOUR-USERNAME/YOUR-FORK.git (fetch)
> origin  https://github.com/YOUR-USERNAME/YOUR-FORK.git (push)
```

2. add upsteam or origin to the local repo
```bash
git remote add upstream https://github.com/ORIGINAL-OWNER/Spoon-Knife.git
git remote add origin https://github.com/YOUR-USERNAME/YOUR-FORK.git
```

3. To verify the new upstream repository you have specified for your fork, type git remote -v again.
You should see the URL for your fork as origin, and the URL for the upstream repository as upstream.
```bash
$ git remote -v
> origin    https://github.com/YOUR-USERNAME/YOUR-FORK.git (fetch)
> origin    https://github.com/YOUR-USERNAME/YOUR-FORK.git (push)
> upstream  https://github.com/ORIGINAL-OWNER/ORIGINAL-REPOSITORY.git (fetch)
> upstream  https://github.com/ORIGINAL-OWNER/ORIGINAL-REPOSITORY.git (push)
```

## IV. Syncing a fork(與upstream保持同步)
https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork

1. Change the current working directory to your local project.
```bash
cd .\aspnetcore
```
2. Fetch the branches and their respective commits from the upstream repository. Commits to BRANCH-NAME will be stored in the local branch upstream/BRANCH-NAME.
從 upstream 儲存庫抓取所有分支與其提交紀錄。分支 BRANCH-NAME 的提交會存到本地對應的upstream/BRANCH-NAME 裡。
```bash
git fetch upstream
> * [new branch]      safia/forward-headers -> upstream/safia/forward-headers
> * [new tag]         2.1.1 -> 2.1.1
```
- upstream 倉庫新增了一個叫做 safia/forward-headers 的分支。
Git 幫你把它同步到本地，並標記成 upstream/safia/forward-headers（這是個 遠端追蹤分支，不是你本地的 branch）。
- upstream 倉庫新增了一個 tag 2.1.1。
Git 幫你把這個 tag 同步下來，所以你本地現在也有 2.1.1 這個標籤了。可以用指令查看。
```bash 
git tag -l
```

這些訊息代表 上游有新分支或新標籤，Git 把它們抓下來給你，並建立了對應的「遠端追蹤分支」與「tag」。這並不會自動合併到你本地的分支，你需要自己 checkout 或 merge/rebase 才能使用。

3. Check out your fork's local default branch - in this case, we use main.
```bash
PS C:\Users\hyou0\source\open-source\aspnetcore> git checkout main
> Already on 'main'
> Your branch is up to date with 'origin/main'. 
```

4. Merge the changes from the upstream default branch - in this case, upstream/main - into your local default branch. This brings your fork's default branch into sync with the upstream repository, without losing your local changes.
把上游預設分支（這裡是 upstream/main）的更新合併到你本地的 main。這樣可以讓你的 fork 的 main 與 upstream 同步，而且不會丟失你的本地修改。
```bash
PS C:\Users\hyou0\source\open-source\aspnetcore> git merge upstream/main
Updating e65607698d..89bd3386c7
Fast-forward
 .azure/pipelines/ci-public.yml                     |  21 +-
 .azure/pipelines/ci.yml                            |  23 +-
 .azure/pipelines/components-e2e-tests.yml          |   4 - 
 .github/workflows/backport.yml                     |   2 +-
 .github/workflows/browsertesting-open-issue.yml    |   2 +-
 .github/workflows/copilot-setup-steps.yml          |   2 +
....
```
如果你的本地分支沒有獨有的 commit，Git 就會做 fast-forward。
解釋：fast-forward 就是「直接移動指標」，而不是產生新的合併 commit。

5. conclusion
- git fetch upstream → 從上游抓最新更新（放到所有upstream/XXXX分支內）。
- git checkout main → 切換到本地 main。
- git merge upstream/main → 把 upstream 的更新合併到本地 main。

6. Tip: Syncing your fork only updates your local copy of the repository. To update your fork on GitHub.com, you must push your changes.
當你 同步 upstream (上游倉庫) 的時候，更新的內容只會反映到 你電腦本地的 fork 倉庫，並不會自動更新到 GitHub 網站上的 fork。
所以還要做一步：
**你需要把本地同步好的內容 push (推送) 上去，這樣你 GitHub.com 上的 fork 才會和 upstream 保持一致。**
https://docs.github.com/en/get-started/using-git/pushing-commits-to-a-remote-repository

- 先前執行
```bash
git fetch upstream
git merge upstream/main
```
這樣你的 本地 fork 就更新了。
但是 GitHub 網站上的 fork 還沒變。

- 必須再執行：
```bash
git push origin main
```
才能把更新後的本地分支推到 自己的 GitHub.com 上。



# 完整流程：從 fork → 修改 → 提交回 upstream
1. Fork 專案（一次性動作）
在 GitHub 上 Fork 原專案，得到你自己的副本。

2. Clone 你的 fork 到本地
```bash
git clone https://github.com/你的帳號/專案名稱.git
cd 專案名稱
```

3. 設定 upstream（一次性動作）
這樣才能保持和原專案的連結：
```bash
git remote add upstream https://github.com/原作者帳號/專案名稱.git
```
之後就能 git fetch upstream 來同步。

4. 建立新分支來做修改
**千萬不要直接在 main 分支上改，最好開新分支。**
例如你要修一個 bug：
```bash
git checkout -b fix-bug-typo
```

5. 修改程式碼

在編輯器（VS Code 等）修改程式碼，然後存檔。

6. 提交修改
```bash
git add .
git commit -m "Fix typo in README"
```

7. Push 到你的 fork（origin）
```bash
git push origin fix-bug-typo
```
這樣這個分支就會出現在你 GitHub 帳號的 fork 裡。

8. 建立 Pull Request（PR）
到 GitHub 上你的 fork 頁面。
會看到 "Compare & Pull Request" 按鈕，點它。
選擇要把 fix-bug-typo 這個分支的修改，送到 upstream 專案的 main 分支。
填寫說明（你修改了什麼、為什麼要改），然後送出。

9. 等待 Review
專案維護者會審查你的 PR。
如果需要修改，他們會留言，你只要在 同一個分支 做更改，再 git push origin fix-bug-typo 就會自動更新 PR。

一旦被接受 → 你的修改就會正式進到 upstream 🎉

# 整個流程簡化版命令
```bash
# Fork + Clone
git clone https://github.com/你的帳號/專案.git
cd 專案
git remote add upstream https://github.com/原作者/專案.git

# 建新分支修改
git checkout -b feature-branch
# (修改檔案)
git add .
git commit -m "新增功能或修正 bug"
git push origin feature-branch

# → 然後到 GitHub 開 PR
```

## 核心觀念：
- origin → 你的 fork
- upstream → 原專案
- 你只能 push 到 origin，然後透過github網頁的 PR 請 upstream 合併。
