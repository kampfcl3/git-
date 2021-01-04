# git金鑰產生設定
## 一:建立Github repository(倉庫)
> ps:請事先申請github帳號和安裝git
```
1.在github中新增一個repositories
2.注意請加一個README.md在初始設定中
```
#### 基礎SSH key知識
```
加密傳輸的演算法有好多，git使用rsa，rsa要解決的一個核心問題是，如何使用一對特定的數字，使其中一個數字可以用來加密，而另外一個數字可以用來解密。
這兩個數字就是你在使用git和github的時候所遇到的public key也就是公鑰以及private key私鑰。

公鑰:就是那個用來加密的數字，這也就是為什麼你在本機生成了公鑰之後，要上傳到github的原因。從github發回來的，用那公鑰加密過的資料，可以用  
     你本地的私鑰來還原。

如果你的key丟失了，不管是公鑰還是私鑰，丟失一個都不能用了，解決方法也很簡單，重新再生成一次，然後在github.com裡再設定一次就行
```
#### 設定global數值
```
1.進入git bash視窗中
2.繫結使用者名稱和郵箱
```
##### 指令: 
> git config --global user.name "github的名字"  
> git config --global user.email "github的email"  
```
ps：使用者名稱和郵箱作為你的唯一標識，–global這個引數，表示這臺機器上的所有Git倉庫都會使用這個配置，也可以指定倉庫用不同的使用者名稱和郵箱
```

## 二:新建ssh key檔案(本地)
```
1.到.ssh檔案中查看是否有id_rsa和id_rsa.pub (有的話可跳過此段)
2.沒有的話則在本機新建 ssh key
```
安裝好 git 這裡是不會有一個叫「.ssh」的資料夾的 (*是個 git 專門用來存放 ssh key 的位置 )。
若沒有這資料夾，也表示你未曾設定過 ssh
故，請在 git bash 輸入指令
##### 指令: 
> ssh-keygen -t rsa -b 4096 -C “your_email@example.com”

```
1. 輸入完指令，git bash 會問你要安裝 ssh key 到哪個本機資料夾位置，圖中可見的路徑是自動生成的位置，也就是在前面所說的根目錄位置下，建立一新
資料夾名為「.ssh」，而字串最後的「id_rsa」就是本機端的 ssh key 檔案(沒副檔名)

輸入 enter 前往下一步 (可見下圖右側根目錄自動建立了 .ssh 資料夾)
自動在 .ssh 裡建立 ssh key 檔案

2.git bash 問未來在使用此服務時是否要密碼；在此可以設，也可以直接按兩個 enter 來跳過(等於不設定密碼)
```
```
1.「id_rsa」是本機端的 ssh key，私密設定
2.「id_rsa.pub」是給 github 網站上，設定在你的 github account 的 ssh key，公開設定 (這副檔 .pub 即 public 意思)
```
#### 將 ssh key 添加到本機 ssh-agent (私人金鑰)
1.確保ssh-agent正在運行
##### 指令: 
> eval $(ssh-agent -s)
指令輸入完，按 enter ，git bash 會反饋一行代碼「Agent pid xxxxx」也就是ssh-agent 有正確運行的意思了

2.選取在根目錄的.ssh資料夾中的「id_rsa」檔案(本機端的 ssh key 檔案)，到本機 ssh 中
> ssh-add ~/.ssh/id_rsa
```
ps:不要指定成有副檔名的 id_rsa.pub ，會噴錯誤說你在本機開放的權限太大了，而不給過
```
出現 identity 等字，表示完成本機端的私人金鑰設定 (設定完成)

## 三:github設定ssh key(公鑰)
```
1、進入github，點選settings
2、然後開啟SSH keys選單，Add SSH key新增祕鑰，填上標題（隨意，建議跟repository一致），然後將id_rsa.put檔案中的key貼上，然後Add key生成祕鑰。
```
## 四:與本地端進行版本同步實作
1.在本地端新建一個txt檔(test010.txt)
```
ps：git是藉由每個版本的"內容差異"去做更新的，所以git是不能管理空資料夾的，也就是說檔案夾了必須有檔案才能add
```
[image](https://github.com/kampfcl3/git-/blob/main/pic/github(git)002.png)  
2.初始化將你想建立本地倉庫的這個目錄變成Git可以管理的倉庫
> git init  
資料夾下將多了一個隱藏資料夾.git，這個目錄是Git用來跟蹤管理版本庫的，不要修改

3.將所有檔案新增到倉庫
> git add .  
ps:注意空格  

4.把檔案提交到倉庫和提交註釋原因  
> git commit -m "註釋內容"  

5.本地端連結github遠端倉庫
> git remote add origin git@github.com:kampfcl3/專案名稱.git  
```
"git@github.com:kampfcl3/專案名稱.git"這一段代碼可以在專案的code按鈕中的ssh書籤中找到
```
[image](https://github.com/kampfcl3/git-/blob/main/pic/github(git)001.png)  

6.push上傳原生代碼  
> git push -u origin master    
```
origin:遠端
master:為版本branches(有分主幹跟分枝)
```
[image](https://github.com/kampfcl3/git-/blob/main/pic/github(git)003.png)  

#### failed to push some refs to git錯誤
> 原因:github中的README.md檔案沒有download到原生代碼目錄中

```
解決方式:
1.將github上的README.md檔案以git pull下來
```
> git pull --rebase origin master  
```
2.直接將README.md複製進本地端倉庫
```  

```
ps:README.md是屬於倉庫的說明書，建議是要有的。
```
> [failed to push some refs to git](https://www.jianshu.com/p/835e0a48c825)
#### 更新新檔案
將test020檔案上傳
> git add .  
> git commit -m "註釋原因"  
> git push origin master  

ps:-u只需要加在第一次
## 資料來源

> [MAIN 使用git將本地庫上傳到遠端倉庫](https://www.itread01.com/content/1547628496.html)  
> [MAIN ssh key設定 github](https://medium.com/@eason920/github-%E7%9A%84-ssh-%E5%8D%94%E8%AD%B0%E8%A8%AD%E5%AE%9A-%E4%B8%8A-45f26e4564f6)  

> [Git 提交(commit)檔案](https://blog.jaycetyle.com/2018/02/git-commit/)
> [本地第一次推送至遠端的錯誤](https://codertw.com/%E8%BB%9F%E9%AB%94%E9%96%8B%E7%99%BC%E5%B7%A5%E5%85%B7/24694/)
