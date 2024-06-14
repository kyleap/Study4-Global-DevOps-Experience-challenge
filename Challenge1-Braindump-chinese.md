# 挑戰 1 - 知識匯整

好的團隊，Jordan 希望我們為我們的存儲庫創建一個工作空間，以便我們能夠快速上線新的開發團隊。我真的認為這對我們有好處，所以我已經進行了一些研究。這裡是我的初步想法和我找到的文檔連結：

### Codespace 設置：
- 要設置工作空間，您可以查看 [這個 Github 連結](https://docs.github.com/en/codespaces/developing-in-a-codespace/creating-a-codespace-for-a-repository)。確保我們可以在工作空間中運行 C# 程式碼。
- Jordan 也提到了一些他希望安裝的擴展。通過瀏覽擴展標籤，您可以安裝這些插件。我發現了 [這個快速入門](https://docs.github.com/en/codespaces/getting-started/quickstart)，簡要說明了它的工作原理，可以給您一些想法。看起來並不太困難。
- 一旦您點擊 "Add to devcontainer.json"，您就有機會安裝其他功能。

### 調試
我們需要檢查是否可以從工作空間運行和調試應用程序。只需按 F5 並確保所有應用程序都啟動。如果沒有，您可能需要更改 VSCode 中的啟動設置。還請檢查應用程序是否支持斷點調試，我們需要能夠調試我們的代碼！

### 端口轉發
有一些關於工作空間中端口轉發的文檔 [在這裡](https://docs.github.com/en/codespaces/developing-in-a-codespace/forwarding-ports-in-your-codespace)。這應該可以幫助您開始。

### 最後
我們需要確保 devcontainer.json 文件是完整的並推送到存儲庫的主分支，否則其他人無法使用它。
