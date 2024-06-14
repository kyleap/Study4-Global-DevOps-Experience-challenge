# 挑戰 3 - 測試 GitHub Copilot

團隊好，這裡是 Alex，Emily 終於批准了使用 GitHub Copilot。在將其推廣到整個組織之前，我們需要作為平台團隊先進行測試。

我們對工程師進行了關於開發者生產力和開發者幸福感的調查，結果顯示有很多需要改進的地方。因此，讓我們舉行一次黑客松，看看 GitHub Copilot 是否能幫助我們改善調查中的前三大抱怨。

### 調查結果：
1. API 不是 RESTful 的
2. 缺少單元測試
3. 內部開發者文檔

## 1. 啟用 GitHub Copilot
首先啟用 GitHub Copilot 並在 VSCode 中安裝自動完成和聊天插件。我認為特別是聊天功能在這裡會非常有幫助。

## 2. 黑客松挑戰：

### API 不是 RESTful 的
我們有一些 API 不是 RESTful 的。在這次黑客松中，讓我們專注於 `catalog` 項目中的 `EventController.cs`。使這個控制器成為 RESTful 的。

這個 API 也在前端代碼中使用，因此需要與新的 RESTful API 兼容。更改 `frontend` 項目中的 `EventCatalogService.cs` 以使用新的 RESTful API。

### 缺少單元測試
`catalog` 項目中的 `EventController.cs` 也缺少單元測試。為這個控制器編寫單元測試。

確保這些單元測試也與新的 RESTful API 兼容，並在管道中運行。

將單元測試存儲在一個新的 .Net 項目中，名為 `catalog.tests`，並將測試類命名為 `EventControllerTests.cs`。

### 內部開發者文檔
當前的 catalog API 沒有任何 OpenAPI 規範。您可以向 API 添加 Swagger 以生成 OpenAPI 規範。請嘗試使用 Copilot 為 `program.cs` 生成 Swashbuckle 的添加。
