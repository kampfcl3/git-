# git金鑰產生設定
```
在本機新建 ssh key，並將 ssh key 添加到本機 ssh-agent (私人金鑰)
```
## 新建ssh key檔案
安裝好 git 這裡是不會有一個叫「.ssh」的資料夾的 (*是個 git 專門用來存放 ssh key 的位置 )。
若沒有這資料夾，也表示你未曾設定過 ssh
故，請在 git bash 輸入指令
> ssh-keygen -t rsa -b 4096 -C “your_email@example.com”




## 資料來源

> (使用git將本地庫上傳到遠端倉庫)[https://www.itread01.com/content/1547628496.html]
