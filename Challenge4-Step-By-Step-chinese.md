# 挑戰 4 - 步驟指南

## 介紹

GitHub 高級安全（GHAS）幫助團隊通過代碼掃描、秘密掃描和依賴審查等功能來提高代碼庫的安全性。本手冊將指導您啟用和配置這些功能的步驟。

## 先決條件
- 擁有組織或存儲庫設置的管理訪問權限。

## 啟用 GitHub 高級安全
1. 進入您的存儲庫設置。

![Image](Images/Challenge04-01.png)

2. 導航到 `Security` 標籤。

![Image](Images/Challenge04-02.png)

3. 啟用高級安全。

![Image](Images/Challenge04-03.png)

4. 自定義並提交您的 dependabot.yml。

![Image](Images/Challenge04-04.png)

5. 選擇以下兩個生態系統並將其添加到您的 dependabot.yml 中。

![Image](Images/Challenge04-05.png)

6. 您的 dependabot.yml 現在應該如下所示。

![Image](Images/Challenge04-06.png)

註：請注意不同的更新間隔（前端包更頻繁變更）。

7. GitHub 高級安全。

![Image](Images/Challenge04-07.png)

啟用 GHAS 時，您會看到以下提示：

![Image](Images/Challenge04-08.png)

點擊啟用。

8. 配置秘密掃描並檢查其他設置：

![Image](Images/Challenge04-09.png)

9. 設置代碼掃描：

![Image](Images/Challenge04-10.png)

![Image](Images/Challenge04-11.png)

![Image](Images/Challenge04-12.png)

這可能需要一段時間：

![Image](Images/Challenge04-13.png)

10. 啟用推送保護。

![Image](Images/Challenge04-14.png)

11. 導航到安全標籤：

![Image](Images/Challenge04-15.png)

並檢查警報：

![Image](Images/Challenge04-16.png)

查看生成的拉取請求，並從上到下依次修復，從關鍵到高優先級等。

![Image](Images/Challenge04-17.png)

查看代碼掃描：

![Image](Images/Challenge04-18.png)

12. 在 codespaces 中使用 CoPilot 修復 SQL 注入。

![Image](Images/Challenge04-19.png)

![Image](Images/Challenge04-20.png)

啟動 codespace 並使用 CoPilot。

![Image](Images/Challenge04-21.png)

![Image](Images/Challenge04-22.png)

![Image](Images/Challenge04-23.png)

![Image](Images/Challenge04-24.png)

13. 導出您的 SBOM，並將文件保存為 sbom.json。創建一個名為 sbom 的文件夾，並將其上傳/合併到主分支中。

![Image](Images/Challenge04-25.png)

## GitHub 高級安全的最佳實踐

1. 定期審查和更新安全政策
   - 確保您的安全政策定期更新以反映新出現的威脅和漏洞，包括審查代碼掃描的規則並進行更新以捕獲新興的安全問題。

2. 在開發生命周期的早期集成安全性
   - 通過在開發過程的早期集成 GHAS 功能來“左移”安全性。鼓勵開發者使用與 GitHub 安全功能集成的本地掃描工具，以在代碼到達主分支之前捕捉問題。

3. 使用分支保護規則
   - 應用分支保護規則以要求拉取請求審查並通過狀態檢查後才能合併。這確保代碼掃描和檢查必須通過，從而防止已知漏洞進入受保護的分支。

4. 在 CI/CD 管道中自動化安全性
   - 在 CI/CD 管道中自動化安全掃描，以確保每個構建都自動掃描漏洞。這有助於在部署前識別和減少風險。

5. 教育您的團隊
   - 定期舉行安全最佳實踐和編碼安全重要性的培訓會。教育您的團隊有關 GHAS 的特定功能及其有效使用方法。

6. 定期審計訪問控制
   - 定期審查誰可以訪問您的存儲庫，確保只有必要的人員擁有管理權限。收緊訪問控制以最小化內部威脅風險。

7. 監控和處理安全警報
   - 定期監控 GitHub 生成的安全警報並迅速處理。設置通知以確保當潛在問題被檢測到時相關團隊成員被通知。

8. 利用秘密掃描保護敏感信息
   - 使用 GHAS 的秘密掃描來檢測和防止 API 密鑰和憑據等秘密的暴露。這有助於防止可能導致嚴重安全漏洞的意外泄露。

9. 啟用 Dependabot 警報和安全更新
   - 充分利用 Dependabot 來保持依賴項的最新和安全。配置 Dependabot 自動為關鍵安全更新打開拉取請求。

10. 為安全事件採取應對計劃
    - 制定一個清晰的文件化計劃以應對安全事件。確保您的團隊知道在檢測到安全問題時如何反應，包括聯繫誰以及遵循哪些步驟。

11. 定期審查和完善安全功能
    - 持續審查安全措施的有效性。根據新的安全趨勢和項目的發展需要調整和完善 GHAS 功能的使用。

12. 使用 CodeQL 進行高級代碼掃描
    - 利用 GitHub 的 CodeQL 進行深度語義代碼分析，以識別其他工具可能錯過的複雜漏洞。定制 CodeQL 查詢以滿足應用程序的特定安全需求。

## 文檔
有關 GitHub 高級安全的詳細信息，請訪問 [GitHub 高級安全文檔](https://docs.github.com/en/code-security)。

## 結論
通過遵循本手冊，您的團隊可以有效利用 GitHub 高級安全來保護您的項目。保持警惕，並定期更新您的安全設置。
