# 挑戰 6 - 步驟指南

## 介紹
我們將使用語義內核來創建推薦引擎。讓我們開始吧！

## 先決條件
我創建了一個拉取請求，您需要接受它。只需接受它，它將為解決方案提供起點。接受我創建的拉取請求後，您會發現前端代碼已經完成。它調用我們的目錄 API，其中有一個名為 `EventRecommendations` 的新控制器。此控制器已經有一個構造函數來創建您可以使用的語義內核實例。

## 獲取下個月可用的活動列表

要獲取可用的活動列表，您可以調用 `_eventRepository` 並請求它使用 `GetEvents()` 方法提供所有可用的活動。

接下來，您可以使用簡單的 LINQ 查詢過濾返回的活動列表。這樣做如下：

```csharp
var availableEvents = events.Where(e => e.Date > now && e.Date < now.AddMonths(1)).ToList();
```
我們可以使用此列表作為內核的輸入，請求它提供推薦。

## 獲取推薦
為此，我們創建了一個提示，指示 LLM 生成一個包含推薦活動的逗號分隔列表的輸出。

我們從定義提示開始。

```csharp
const string prompt = "Given the artist {{$input_artist}}, recommend similar artists from the following events: {{$event_list}}. " +
                      "ONLY return the event ids of the recommended events as a comma-separated list, nothing else.";
```

您會看到我們這裡有兩個輸入：客戶喜歡的藝術家和我們剛從自己的服務中獲得的活動列表。

接下來，我們需要以語義內核可以處理的方式定義這些參數。
這樣做如下：

```csharp
var arguments = new KernelArguments
                {
                    {"input_artist", artist},
                    {"event_list", string.Join(Environment.NewLine, availableEvents.Select(e => JsonSerializer.Serialize(e)))}
                };
```
Now we have everything ready to call the Kernel and use the LLM to get a recommendation.

現在我們已經準備好調用內核並使用 LLM 獲得推薦。

這樣做如下：
```csharp
var result = await _kernel.InvokePromptAsync(prompt, arguments);
```

最後，我們將結果返回給調用者。
```csharp
var chosenEvents = result.ToString()
                         .Split(",")
                         .Select(eventId => eventId.Trim())
                         .Select(Guid.Parse);
```
And finally, we return the results to the caller.

```csharp
availableEvents.Where(e => chosenEvents.Contains(e.EventId)).ToList();
```


## 總結
- 您從數據庫中選擇了答案中使用的事件。
- 您創建了一個提示來使用 LLM 獲得推薦。
- 您明確要求它返回一個逗號分隔的列表。
- 您解析了該結果並將事件列表返回給調用者。

完成了，您現在已經創建了一個相當先進的推薦引擎的邏輯，現在它可以幫助您的客戶購買類似於他們喜愛的藝術家的演唱會門票。

