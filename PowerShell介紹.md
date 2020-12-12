# PowerShell介紹
[PowerShell](https://docs.microsoft.com/zh-tw/powershell/scripting/overview?view=powershell-7.1) 是跨平台的工作自動化及設定管理架構，由命令列殼層與指令碼語言組成。
1.以 .NET Common Language Runtime (CLR) 為建置基礎，並接受及傳回 .NET 物件。
2.不同於大部分的殼層可接受及傳回文字
## 輸出是以物件為基礎的
```
不同於傳統的命令列介面，PowerShell Cmdlet 是設計來處理物件。 物件是結構化的資訊，
而不僅僅是出現在畫面上的字元字串。 命令輸出一律會攜帶您在需要時可以使用的額外資訊。

```
## 命令系列可進行擴充
```
命令系列可進行擴充cmd.exe 之類的介面無法讓您直接擴充內建的命令集。 您可以建立外部命令列工具
在 cmd.exe 中執行。 但這些外部工具不會提供任何服務，例如說明整合。 cmd.exe 自己不會知道這些
外部工具是有效的命令。

PowerShell 中的命令稱為 Cmdlet 。 您可以個別使用每個 Cmdlet，但合併使用來執行複雜的工作時，
更見其功效。 如同許多殼層，PowerShell 可讓您存取電腦上的檔案系統。 PowerShell「提供者」可讓
您像存取檔案系統般容易地存取其他資料存放區 (如登錄及憑證存放區)。您可以使用經過編譯的程式碼或
指令碼，建立自己的 Cmdlet 與函式模組。 模組可將 Cmdlet 與提供者新增到殼層。 PowerShell 也支
援類似於 UNIX 殼層指令碼及 cmd.exe 批次檔案的指令碼。
```
## 支援命令別名
```
Cmdlet 名稱的輸入可能會很麻煩。為了縮短命令輸入時間並且讓習慣其他殼層的使用者更容易操作 Windows PowerShell
，因此 Windows PowerShell 支援「別名」的概念，也就是命令的其他名稱。您可以為 Cmdlet 名稱、函數名稱或是其
他執行檔名稱建立別名，這樣便可在任何命令中輸入別名，而不用輸入 (完整) 名稱。
```
```
Windows PowerShell 包括許多內建別名，而且您可以建立自己的別名。您建立的別名只在目前工作階段中有效。
若要建立永久別名，請將別名加入到您的 Windows PowerShell 設定檔。
```
## PowerShell 會處理主控台輸入和顯示
```
當您輸入命令時，PowerShell 一律會直接處理命令列輸入。 PowerShell 也會將您在畫面上看到的輸出格式化。
此差異十分重要，因為它可以減少每個 Cmdlet 所需的工作。 它會確保您一律可以使用與任何 Cmdlet 相同的方式
來執行動作。 Cmdlet 開發人員不需要撰寫程式碼來剖析命令列引數，或將輸出格式化。
```
```
ps: 如果您在 PowerShell 中執行圖形應用程式，即會開啟應用程式的視窗。 只有在處理您提供的命令列輸入或傳
回給主控台視窗的應用程式輸出時，PowerShell 才會介入。 它不會影響應用程式的內部運作方式。
```
## PowerShell 具有管線
```
管線可說是用於命令列介面中最重要的概念。 若運用得當，管線將能減少使用複雜命令，讓您能夠更清楚地觀察工作的流程。 
管線中的每個命令都會將其輸出逐項傳遞給下一個命令。 命令不需要每次處理一個以上的項目。 結果就是減少使用資源，而且立即得到輸出。
用於管線的標記法類似於其他殼層中所使用的標記法。 乍看之下，PowerShell 中的管線差異可能並不明顯。 雖然您會在畫面上看到文字
，但 PowerShell 會在命令之間使用管線來傳送物件 (而非文字)。
```
#### 範例001
```
例如，如果您使用 Out-Host Cmdlet 強制逐頁顯示另一個命令的輸
出，則輸出看起來就像畫面上所顯示的一般文字 (分成數頁)：
```
> Get-ChildItem | Out-Host -Paging

Output:
```
Directory: /mnt/c/Git/PS-Docs/PowerShell-Docs/reference/7.0/Microsoft.PowerShell.Core

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d----          05/22/2020    08:30                About
-----          05/20/2020    14:36           9044 Add-History.md
-----          05/20/2020    14:36          12227 Clear-History.md
-----          05/20/2020    14:36           3566 Clear-Host.md
-----          05/20/2020    14:36          29087 Connect-PSSession.md
-----          05/20/2020    14:36           5705 Debug-Job.md
-----          05/20/2020    14:36           3515 Disable-ExperimentalFeature.md
-----          05/20/2020    14:36          25531 Disable-PSRemoting.md
-----          05/20/2020    14:36           7852 Disable-PSSessionConfiguration.md
-----          05/20/2020    14:36          25355 Disconnect-PSSession.md
-----          05/20/2020    14:36           3491 Enable-ExperimentalFeature.md
-----          05/20/2020    14:36          13310 Enable-PSRemoting.md
-----          05/20/2020    14:36           8401 Enable-PSSessionConfiguration.md
-----          05/20/2020    14:36           9531 Enter-PSHostProcess.md
...
<SPACE> next page; <CR> next line; Q quit
```
```
分頁還會降低 CPU 使用率，因為處理控制權會在其已準備好要顯示的完成頁面時移轉給 Out-Host Cmdlet。 
管線中在它前面的 Cmdlet 會暫停執行，直到輸出的下一個分頁可供使用為止。
```
## 管線中的物件
```
當您在 PowerShell 中執行 Cmdlet 時，您會看到文字輸出，這是因為在主控台視窗中必須將物件呈現為文字。
文字輸出可能不會顯示要輸出之物件的所有屬性。
```
#### 範例002
```
請考慮 Get-Location Cmdlet。 文字輸出是資訊的摘要，並不是由 Get-Location 所傳回之物件的完整呈現。 
輸出中的標題是由處理序新增的，它會將資料格式化以便在畫面上顯示。
```
> Get-Location

Output:
```
Path
----
C:\
```
```
使用管線將輸出傳送給 Get-Member Cmdlet 時，會顯示 Get-Location 所傳回之物件的相關資訊。
```
> Get-Location | Get-Member

Output:
```
TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Equals       Method     bool Equals(System.Object obj)
GetHashCode  Method     int GetHashCode()
GetType      Method     type GetType()
ToString     Method     string ToString()
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   string Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {get;}
ProviderPath Property   string ProviderPath {get;}
```
Get-Location 會傳回 PathInfo 物件，其中包含目前的路徑與其他資訊。

## 參考
```
https://docs.microsoft.com/zh-tw/powershell/scripting/overview?view=powershell-7.1
```

