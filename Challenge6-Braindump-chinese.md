# 挑戰 6 - 知識匯整

好的，我已經創建了一個新的拉取請求，印度團隊更新了前端代碼。請將其合併到您的 `main` 分支中。您會發現 `EventCatalogController` 現在可以調用我們的目錄 API 上的新方法 `EventRecommendations`。此控制器已經有一個構造函數來創建您可以使用的語義內核實例。

您唯一需要做的就是在目錄項目的 `EventRecommendations.cs` 文件中實現 `GetRecommendations` 方法。此方法需要查詢事件存儲庫並獲取下個月可用的事件。

您可以使用 [Basic InvokePromptAsync](https://learn.microsoft.com/en-us/semantic-kernel/prompts/your-first-prompt?tabs=Csharp) 方法。只需從數據庫中獲取事件並將這些事件作為參數提供給您的提示。

這些事件用於請求內核向您提供建議。為此，您需要編寫一個提示，該提示將結果作為逗號分隔的事件標識符列表返回。這些標識符可用於從您檢索的事件列表中選擇正確的事件，然後將其作為函數的結果返回。

與您之前使用的功能（我們的 AI 事件解析器）一樣，您創建了一個提示，指示 LLM 返回與客戶的需求匹配的事件列表，該列表基於他們提供的最喜歡的藝術家。
