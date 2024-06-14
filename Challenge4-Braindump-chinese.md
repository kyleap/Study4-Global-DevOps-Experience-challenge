# 挑戰 4 - 知識匯整

## GitHub 高級安全

### 啟用 GHAS 並激活所有功能
首先，我們需要設置 GHAS。這很簡單。只需按照 [這裡的指示](https://docs.github.com/en/enterprise-cloud@latest/code-security/getting-started/github-security-features) 進行操作，確保開啟所有功能。

### 生成 SBOM

軟體材料清單（SBOM）是詳細列出軟體中包含的所有組件的清單。這包括直接和間接依賴項，如來自第三方供應商的庫、包和模塊。SBOM 類似於食品產品上的成分表，提供軟體內部的透明度。

導出 SBOM 至關重要的原因有：

1. **安全性**：通過導出 SBOM，組織可以更輕鬆地識別和管理軟體組件中的安全漏洞。當發現包含的組件中存在安全漏洞時，能夠迅速評估和緩解。
2. **合規性**：許多行業需要遵守法規，要求軟體組件的透明度，尤其是在關鍵基礎設施或處理敏感數據的產品中。SBOM 有助於證明符合這些法規。
3. **軟體保障**：導出 SBOM 有助於管理軟體許可證，確保遵守開源許可證。它還有助於避免因誤用專有或開源軟體而產生的潛在法律問題。
4. **供應鏈管理**：在當今互聯的軟體開發生態系統中，SBOM 提供了軟體供應鏈的清晰視圖。它幫助組織追踪每個組件的來源和完整性，增強對供應鏈攻擊的整體安全防護。

因此，SBOM 不僅增強了軟體的透明度和安全性，還支持合規性、法律和運營實踐。導出和保持最新的 SBOM 正成為軟體開發和管理的最佳實踐。

詳細文檔請參閱 [這裡](https://docs.github.com/en/code-security/supply-chain-security/understanding-your-software-supply-chain/exporting-a-software-bill-of-materials-for-your-repository)。

### Dependabot

GitHub Dependabot 是 GitHub 集成的自動化工具，幫助開發者維護軟體依賴項的安全性和可靠性。Dependabot 定期掃描項目的依賴文件，如 npm、Maven 或 Pip 的依賴文件，並識別過時或存在漏洞的庫。當檢測到需要更新的依賴項時，Dependabot 會自動生成拉取請求以更新到最新版本，這可能包括安全漏洞的修補或其他重要錯誤的修復。

使用 GitHub Dependabot 的好處：

1. **增強安全性**：Dependabot 通過確保依賴項使用最新的安全修補程序來幫助保護應用程序。這種主動措施減少了舊版本中存在的可利用漏洞的風險。
2. **節省時間**：通過自動更新依賴項，Dependabot 節省了開發者手動跟踪和更新每個依賴項所需的大量時間和精力，使開發者能夠更多地專注於開發功能和改進產品。
3. **提高可靠性**：定期更新確保軟體使用最穩定的依賴項版本，這可以提高整體可靠性和性能。Dependabot 也通過確保更新與軟體的其他部分兼容來最小化兼容性問題。
4. **簡單易用**：Dependabot 直接集成在 GitHub 中，使其易於設置和使用，無需額外的工具或平台。

總的來說，GitHub Dependabot 是任何旨在保持高標準軟體安全性和完整性的開發團隊的必備工具，同時優化開發工作流程。

請參閱 [這裡的快速入門指南](https://docs.github.com/en/code-security/getting-started/dependabot-quickstart-guide) 獲取詳細說明。

### 代碼掃描

GitHub 代碼掃描是一個集成在 GitHub 中的開發工具，用於自動掃描代碼庫以識別安全漏洞和代碼錯誤。該工具利用 GitHub Actions 或第三方集成，持續分析每次提交或拉取請求的代碼，檢查潛在的安全問題或可能損害軟體完整性的錯誤。

使用 GitHub 代碼掃描的好處：

1. **主動安全措施**：通過在代碼合併到主分支之前掃描漏洞，GitHub 代碼掃描有助於防止安全問題進入生產環境。這種早期檢測對於減少安全漏洞風險至關重要。
2. **簡化代碼審查**：該工具直接在拉取請求中突出顯示潛在問題，使開發者更容易審查代碼更改。這種集成不僅節省時間，還通過將注意力集中在可能的問題上來提高同行評審的質量。
3. **確保合規**：對於需要遵守特定代碼標準和安全法規的組織，GitHub 代碼掃描確保所有代碼在部署前符合這些規則。這對於保持法規遵從性和避免罰款至關重要。
4. **開發者教育**：通過定期暴露自動掃描標記的問題，幫助開發者即時了解常見錯誤和最佳實踐，提升其編碼技能和安全意識。

總的來說，GitHub 代碼掃描是任何優先考慮安全性和質量的軟體開發團隊的重要工具。它無縫地將安全性集成到開發工作流程中，確保漏洞得到迅速有效地解決。

請參閱 [這裡的說明](https://docs.github.com/en/code-security/code-scanning/introduction-to-code-scanning/about-code-scanning) 獲取詳細說明。

### 修復與 SQL 相關的 OWASP 漏洞

解決和修復 OWASP 前 10 名漏洞，特別是與 SQL 注入相關的漏洞，對於保護 Web 應用程序至關重要。OWASP 前 10 名是一份定期更新的報告，概述了對 Web 應用程序最嚴重的安全風險。SQL 注入（SQLi）漏洞，即將惡意 SQL 語句插入到輸入字段中進行執行，由於其可能危及數據庫安全，因此在此列表中排名很高。

**解決 SQL 注入漏洞的步驟：**

1. **使用預備語句和參數化查詢**：這些方法確保即使攻擊者插入 SQL 命令也無法更改查詢的意圖。對於 SQL，大多數現代 SQL 數據庫支持此功能。
2. **使用存儲過程**：通過使用存儲過程，您可以避免來自用戶輸入的直接 SQL 查詢。這將 SQL 封裝在數據庫內，並最小化攻擊面。
3. **實施適當的錯誤處理**：不要向最終用戶暴露數據庫錯誤信息。錯誤可能為攻擊者提供線索，幫助其進一步攻擊。
4. **定期更新和修補**：保持數據庫管理系統（DBMS）和應用程序的最新安全修補程序和更新。
5. **進行安全測試**：定期使用自動化工具和手動滲透測試檢查 Web 應用程序的漏洞。

**進一步學習和文檔：**

有關如何實施這些措施並修復與 SQL 實踐相關的漏洞的實用指南，以下是一些官方文檔和資源的有用連結：

- [OWASP SQL 注入防護備忘單](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)：此備忘單提供了有關特定應用程序安全主題的高價值信息的簡明集合。
- [OWASP SQL 注入測試指南](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web_Application_Security_Testing/07-Input_Validation_Testing/05-Testing_for_SQL_Injection.html)：此指南有助於了解如何測
- [SQL 中的參數化查詢](https://learn.microsoft.com/en-us/sql/relational-databases/security/sql-injection?view=sql-server-ver16)：Microsoft 關於使用參數化 SQL 命令防止 SQL 注入的指南。

這些資源將提供全面的概述和詳細指南，說明如何有效保護您的應用程序免受 OWASP 前 10 名列表中的 SQL 相關漏洞的侵害。

提示💡：使用 GitHub Copilot 來解決這些問題。