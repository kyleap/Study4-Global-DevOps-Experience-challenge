# 挑戰 2 - 知識匯整

## 發佈管道配置
在我們的管道中，我們需要創建一個生產環境以保護此環境。為此，我們需要更新我們的 `ordering`、`frontend` 和 `catalog` 管道，以包含一個目標環境為 `production` 的任務。

我們可以在存儲庫的設置頁面中創建環境。

在 [GitHub 上了解更多有關如何創建環境和目標環境的信息](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment)。

## 分支保護規則
為了確保沒有人在沒有審查或拉取請求的情況下直接提交到主分支，我們需要設置一些分支保護規則。

確保檢查正確的選項以獲得最佳保護：

- 限制刪除
- 要求線性歷史
- 合併前需要拉取請求
  - 需要批准：1
  - 當新提交被推送時，撤銷過時的拉取請求批准
  - 需要代碼所有者的審查
  - 需要最近可審查推送的批准
  - 合併前需要解決對話
- 阻止強制推送

新的分支規則看起來是這項任務的理想功能。[了解更多](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets)。

## Codeowners 設置
為了確保合適的人審查合適的內容，我們可以使用 CODEOWNERS。將其設置為我們團隊是審查者。[在 GitHub 上了解更多信息](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners)。不要忘記保護 `CODEOWNERS` 文件本身免於未授權的更改。

## Rebase 策略實施
有很多方式可以將更改合併到代碼庫中。過去，由於這麼多人在分支上提交代碼然後合併，找出發生了什麼變得非常困難。讓我們試著保持乾淨的歷史記錄！

看起來 GitHub 允許我們配置這種所需的合併方法。讓我們禁用合併提交並實施 Rebase。

在 [這裡了解更多有關合併策略的信息](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/about-merge-methods-on-github)。
