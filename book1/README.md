# 測試 ＧitBook 
# 2021/07/11

依據 [1]. https://www.onejar99.com/gitbook-building-and-publishing-free-unlimitedly/
使用 GitBook CLI + GitHub Pages + GitHub Actions 自動建立並發佈一本書

1. 建立 github repository 

2. 建立 book 基本架構檔案

需要檔案如下
- README.md : 是必要檔案，會成為 Introduction 頁面。github 說明檔案
- SUMMARY.md : 是必要檔案，會成為 Introduction 頁面。書本主要結構及章節設定檔案
- 建立一目錄放置文章章節 : 非必要
- book.json :  是 gitbook CLI 工具製書時的必要設定檔。

book.json
----------
* anchor-navigation-ex：支援 TOC 和「回到頂端」的功能。這個 Plugin 我覺得非常出色，有興趣客製化設定可以參考作者的教學文件。
* copy-code-button：每個 Code Block 右上角會多一個 Copy 按鈕方便複製。
* edit-link：頁面頂端會多一個「EDIT THIS PAGE」的連結，點下去會開啟 GitHub 的編輯頁面。連結的字眼可以自訂。
* ga：Google Analytics，可以填入自己的 trace code。

3. 上傳 book 檔案到 github repository
    git init
    git add -A
    git commit -m "mybook version: 1.0"
    git push origin master
4. 設定 GitHub Access Token

  讓 GitHub Actions 能自動幫我們發佈 GitBook 成果到 GitHub Pages，必須授權 GitHub 操作我們的 Repository。作法就是設定 Access Token。

產生一個 GitHub Personal Access Token：
--------
  * 點右上角帳號的頭像 -> 選擇 Settings -> 左邊列表選擇最底下的 Developer settings -> 下個頁面的左邊列表選擇Personal access tokens。
  * 點擊 Generate new token 按鈕。
  * 輸入 Token 的描述，權限勾選 repo:status 和 public_repo 兩個項目。
  * 點最下面的 Generate token 按鈕。
  * 這時候頁面上會顯示一組 Token，複製下來。注意！產生的 Token 內容只會在此時顯示一次，之後無法再查到，如果忘記 Token 就只能重新操作產生一次。

到 Repository 將剛剛的 Token 設定成 Secret：
------
 * 到想要自動發佈的 Repository -> 選擇 Settings -> 左邊列表選則 Secrets -> 點 New secret 按鈕
 * 「Name」欄位填 GH_ACCESS_TOKEN，「Value」欄位貼上剛剛複製的 Token。
 * 點 Add secret 按鈕，設定就完成了。

5. 撰寫 GitHub Actions Workflow

  設定 GitHub Actions，讓它能自動幫我們製書和發佈到 GitHub Pages。回到資料夾，新增一個 .github/workflows/build.yml 檔案

6. 將 Workflow 檔推上 GitHub，觸發自動發佈到 GitHub Pages
   
   將剛剛新增的 workflow 檔進行 commit 和 push
   
