# 挑戰 5 - 知識匯整

AI 可以再次幫助我們。不僅是編寫代碼，還能解決我們的問題。我們不需要編寫複雜的解析器。我們可以使用 LLM 來為我們解析文件！我們可以使用 Semantic Kernel 在 .NET 代碼中實現這一點。

[Semantic Kernel](https://learn.microsoft.com/en-us/semantic-kernel/)

我已經提交了一個包含文件解析器的拉取請求，昨晚我寫的。它已經包含了 Semantic Kernel 庫，唯一需要做的就是為 AI 編寫正確的提示，我們就有了解決方案。

我發現了一篇由 Duncan Roosma 撰寫的驚人博客，描述了我們需要做的一切。我不知道這是否是巧合，但他正在做的正是我們需要的，只是他是為汽車做的。我們需要的是為我們的音樂會。查看這篇 [Duncan 關於使用 Semantic Kernel 解析非結構化數據的博客文章](https://roosma.dev/p/parsing-unstructured-data-with-semantic-kernel/)

這是我的靈感來源。下面，我描述了我們需要做的粗略概述。

## 合併我的 PR
首先，您需要合併我的 PR，其中包含此項的樣板解決方案。它將 EventImporter 項目添加到我們的解決方案中，我們可以在其中添加 Semantic Kernel 邏輯。

## 獲取 OpenAI 訪問權限
要從 Azure OpenAI 獲取令牌，我們使用我們自己的中央代理位於 https://openai.globoticket.com/event/2bbe-5922。您可以訪問它並使用您的 GitHub 帳戶進行身份驗證。右上角有“Login with GitHub”按鈕。註冊後，您可以向下滾動並找到用於連接到我們的 API 的 URL 和 API 令牌：
![Screenshot of the token and API](Images/OpenAIProxy.png)

為了能夠使用該密鑰，請創建一個名為 `OPENAIKEY` 的 Codespace 機密。請查看如何操作 [這裡](https://docs.github.com/en/enterprise-cloud@latest/codespaces/managing-codespaces-for-your-organization/managing-development-environment-secrets-for-your-repository-or-organization#adding-secrets-for-a-repository)。

## 偽代碼
我已經創建了很多代碼。這是它的功能：
* 從存儲帳戶獲取包含所有事件的完整文件（`Parse` 方法）
* 使用 LLM 將文件分塊以將文件拆分為單獨的事件
* 處理單獨的塊以創建 CreateEventRequest 對象（`ParseEvent`）。我建議將事件文本轉換為 LLM 的 Json 對象並序列化它

## 解析

我們需要解析文件。我已經將我們需要解析的文件添加到我們的存儲帳戶中。在文件 `SemanticKernelSettings.cs` 中，您會看到對這些文件的引用：

```
"https://gdexcdn.azureedge.net/data/email.txt"
"https://gdexcdn.azureedge.net/data/edifact.txt"
"https://gdexcdn.azureedge.net/data/unparsable.txt"
```

這裡不需要您做任何工作。

## 分塊
我們需要創建可以輸入到模型中的文件塊。由於我們不知道文件會有多長，因此需要將其拆分。我已經創建了 `Chunk` 函數。

LLM 不是確定性的。如果它沒有給出正確的結果，我建議您遵循 [Duncan 的博客文章](https://roosma.dev/p/parsing-unstructured-data-with-semantic-kernel/) 並使用 GitHub Copilot 幫助您實驗以獲得正確的提示。

這裡不需要您做任何工作，除非 LLM 給出錯誤的響應。

## 解析事件
現在我們有了單獨的事件，我們需要將它們放入我們的數據庫中。當您構建解決方案時，它會在 `ParseEvents` 中斷。我們需要實現這一點。

您可以使用與 `Chunk` 方法中相同的代碼，只需調整提示即可。調整提示，使其能夠解析事件文本並輸出 JSON 字符串。

您需要找到名為 `EventFileParser` 的 C# 類。它包含一個名為 `ParseEvents` 的方法。此方法分解我們從存儲中讀取的文件，然後為我們提供可以由 LLM 處理的塊。

您唯一需要做的就是為系統提示編寫正確的提示，我們的不可解析文件將變成我們可以處理的 json 字符串。

一個好的方法是少量提示，我們首先告訴 LLM 我們期望什麼，還構建 LLM 返回的歷史記錄。這在 [這篇博客文章](https://www.promptingguide.ai/techniques/fewshot) 中有所說明。在 Semantic Kernel 中，我們稱之為 ChatHistory。

它由三部分組成：
- 系統提示
- 用戶提示
- 助理提示

系統提示示例：

```
You are tasked with converting a user's description of a music event into a structured JSON format.
Only the description provided in the latest user input should be processed into the output. Ignore all previous interactions and outputs.
Follow this template:
{
    "ContextId": "the id of the question asked by the user",
    "Artist": {
        "Name": "extracted artist name",
        "Genre": "extracted genre, if available",
    },
    "Name": "extracted event name",
    "Venue": "extracted event location",
    "Date": "date in YYYY-MM-DD format",
    "Description": "concise event description",
    "Price": extracted price as integer converted to dollar
}
```

用戶提示示例：
```
On the cusp of midnight, when the world slips into the unseen wavelengths of the 10th of January 2024, at the crucible of electrifying symphony known as Qudos Bank Arena, a rendezvous christened "Reverie Rendezvous" is to be unfurled like an unseen spectrum beneath the celestial garnish by none other than the cabal of artists recognized globally as BTS, at a ticket price that mirrors the Indian arithmetic of 144, bathing us all in ultraviolet lights cascading to an unheard rhythm.
```

助理提示示例：
```json
    {
        "Artist": {
            "Name": "BTS",
            "Genre": null
        },
        "Name": "Reverie Rendezvous",
        "Venue": "Qudos Bank Arena",
        "Date": "2024-01-10",
        "Description": "an unseen spectrum beneath the celestial garnish",
        "Price": 144
    }
```

您會看到純粹的魔法！設置斷點或 Console.Writeline，看看這發生了什麼！

如果您想將事件添加到目錄服務中，請確保您在本地啟動該服務，或者通過指向正確的 URL 指向在線服務。


## Plugins
哦，對了，當然我們希望所有票都以 USD 貨幣計價。我查看了文件，發現其中有各種貨幣。為此，您可以使用所謂的插件並將其註冊到 Kernel。當需要進行轉換時，它將調用此函數，您可以實現轉換的方法。我找到了這個免費的貨幣轉換 API，我們可以使用它並調用它來獲得 USD 值。我指的是這個：https://freecurrencyapi.com/。

在 [Duncan的文章](https://roosma.dev/p/parsing-unstructured-data-with-semantic-kernel/) ，他提到使用 ToolCallBehavior 來實現這一點。我已經創建了插件框架。

只需創建一個 HttpClient 並調用 API，並將插件註冊到 Kernel。簡單吧 ;-）。

哦，您也可以隨時詢問 Copilot 告訴您如何編寫代碼……

## 啟用 OpenAI
我在上面簡短提到過，不要忘記從 OpenAI 獲取密鑰

> 注意：要從 Azure OpenAI 獲取令牌，我們使用我們自己的中央代理位於 https://openai.globoticket.com/event/2bbe-5922。您可以訪問它並使用您的 GitHub 帳戶進行身份驗證。右上角有“Login with GitHub”按鈕。註冊後，您可以向下滾動並找到用於連接到我們的 API 的 URL 和 API 令牌：
> ![Screenshot of the token and API](Images/OpenAIProxy.png) 

然後，您需要複製 API 密鑰，並將其放入 Codespace 環境變量 OPENAIKEY 中。這是通過在存儲庫設置中創建一個新的存儲庫機密來完成的，如下圖所示：

![alt text](Images/image.png)

保存變量後，您將在您的 codespace 中看到以下彈出窗口：

![alt text](Images/image-popup.png)

確保您點擊重載並應用，以便您在工作環境中擁有該機密。
不要擔心，重載不會丟失任何數據，codespace 會重新啟動，並且您在重啟前的一切都可用。

您可以通過輸入以下命令從命令行運行應用程序：
dotnet run eventImporter.csproj
這將在控制台中顯示結果的輸出。