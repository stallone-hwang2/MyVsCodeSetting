方法一：轉換為「全域代碼片段」（最推薦，100% 成功）
因為 Blazor 元件通常會跨 .razor、.html 甚至 .cs，做成全域片段最不容易失效。

在 VS Code 中按下 Ctrl + Shift + P 打開命令面板。

輸入並選擇 Preferences: Configure User Snippets（配置用户代码片段）。

在下拉選單中點選 New Global Snippets file...（新建全局代码片段文件）。

輸入檔名，例如：blazor，然後按下 Enter。

此時 VS Code 會自動幫你建立並打開一個名為 blazor.code-snippets 的檔案。

把你上面提供的這整段 JSON 內容，完整複製並覆蓋貼到這個新檔案中，儲存（Ctrl + S）即可！