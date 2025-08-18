# About pull requests
A pull request is a proposal to merge a set of changes from one branch into another.
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
- 做法是：開一個 分支 → 開發 → Push → PR → code review。



# 