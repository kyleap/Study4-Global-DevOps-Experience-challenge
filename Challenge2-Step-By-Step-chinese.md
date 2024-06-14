# 挑戰 2 - 步驟指南

## 介紹
作為 Globoticket 的開發團隊，確保所有團隊成員擁有一致且高效的開發環境至關重要。設置標準化的工作空間可以通過提供預配置所有必要工具和擴展的雲端開發環境來實現這一目標。本指南將帶您完成創建、配置和維護能夠運行 C# 程式碼的工作空間的步驟，確保每個開發人員都擁有相同的設置。這將最小化設置時間，減少配置錯誤，並讓團隊專注於構建和改進應用程序。

## 先決條件
在開始之前，請確保您具備以下先決條件：

1. **完成挑戰 1** - 確保您已完成挑戰 1 中的步驟，並設置包含必要擴展的工作空間。

## 發佈管道配置

確保工作流程目標是 `production` 環境：

1. 編輯 `.github/workflows/build-deploy-catalog.yml`，確保您在 `deploy` 任務中添加 `environment: production`。
2. 編輯 `.github/workflows/build-deploy-frontend.yml`，確保您在 `deploy` 任務中添加 `environment: production`。
3. 編輯 `.github/workflows/build-deploy-ordering.yml`，確保您在 `deploy` 任務中添加 `environment: production`。

創建/更新 `production` 環境：

1. 導航到存儲庫的 **Settings** 標籤。
2. 打開 **Environments** 部分。
3. 如果不存在名為 `production` 的環境，點擊 **New environment** 並創建一個名為 `production` 的新環境，否則打開 `production` 環境。
4. 設置以下選項：
	- 勾選 **Required Reviewers** 並添加您的團隊作為審查者。
	- 勾選 **Prevent self-review**。
	- 確保點擊 **Save protection rules**。
5. 在 **Deployment branches and tags** 下選擇 **Protected Branched Only**。

## 分支保護規則

1. 導航到存儲庫的 **Settings** 標籤。
2. 打開 **Rules** 部分。
3. 點擊 **Rulesets**。
4. 點擊 **New Ruleset** 按鈕並選擇 **New Branch ruleset** 選項。
5. 設置以下選項：
	- 規則集名稱：**Protect main branch**
	- 執行狀態：**Active**
	- 在 **Target branches** 下，點擊 **Add Target** 並選擇 **Include default branch**。
	- 在 **Rules** 下，勾選以下規則：
		- **Restrict deletions**
		- **Require linear history**
		- **Require a pull request before merging**
			- **Require Approvals**：1	 
			- **Dismiss stale pull request approvals when new commits are pushed**
			- **Require review from Code Owners**
			- **Require approval of the most recent reviewable push**
			- **Require conversation resolution before merging**
		- **Block force pushes**

## Codeowners 設置

1. 在 `.github` 文件夾中向存儲庫添加一個名為 `CODEOWNERS` 的新文件。
2. 對於每個需要保護的文件夾和文件，添加一行包含文件夾或文件名稱以及應審查任何更改的 GitHub 團隊。例如：

```
/catalog/ @globaldevopsexperience/your-team
/frontend/ @globaldevopsexperience/your-team
/ordering/ @globaldevopsexperience/your-team
```

3. 還需添加一行來保護 `CODEOWNERS` 文件本身：
```
/.github/CODEOWNERS @globaldevopsexperience/your-team
```

4. 將文件提交到存儲庫。如果需要，將更改合併到 `main` 分支。

## Rebase 策略

1. 導航到存儲庫的 ⚙️ **Settings** 標籤。
2. 點擊 **General** 部分。
3. 向下滾動到 **Pull Requests** 部分。
4. 確保取消選中 **Allow merge commits**。
