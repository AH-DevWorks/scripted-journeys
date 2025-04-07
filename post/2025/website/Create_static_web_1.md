---
title: 自架網站筆記：使用Github + Hugo（上）
date: 2025-04-05 
---

+ 第一篇文章，總之先簡單記錄這個靜態網站怎麼做的，不然大概隔幾天又忘光光。
+ 寫給自己看的，有些我已經懂的部份（像是Git）寫比較簡單。如果你是無意看到這篇，想看懂但看不懂，可以私信我。


### PART 0 : 這個網站的目標
由兩大部份構成：
1. Website-Repo：負責靜態網站呈現（用 Hugo build 出來的 HTML/CSS/JS）。
2. Contents-Repo：放原始內容（markdown，如 content/notes、content/diary）。
+ 未來更新內容主要會在 Contents-Repo，然後將生成的網站部署到 Website-Repo。
+ 也會將其他專案 repo（像 side projects）整合進這個 Hugo 網站。


### PART I : 基礎設定
1. 已經有github帳號
2. Windows `winget install Hugo.Hugo.Extended` 安裝Hugo（建議安裝 `Hugo Extended`版本，方便後續自訂模板樣式）
3. github新建兩個repo：一個放內容（Contents-Repo），一個負責網站本身(Website-Repo. -- ex.AH-DevWorks.github.io)
4. 初始化git分支
```bash
touch README.md
echo "# [Website-Repo]" > README.md
git add README.md
git commit -m "Initial commit"
git push origin main
```
5. 本地clone放網站內容的repo，`hugo new site .`
   + 設在母資料夾較佳，建議別再額外新增如 `hugo new site [MySite etc.]`，否則後續要每次都手動挪動/public或額外設定自動腳本，會很麻煩。
   + 若母資料夾已有內容（如README.md），則用 `hugo new site . --force`
6. 等Hugo自動建立好內容後，cd到themes資料夾；挑個Hugo的theme，照著說明來裝（例如clone 到 themes資料夾，或用Git submodules處理）
7. 把這個theme設成預設：
    + 回到步驟5建立好的母資料夾，`vi hugo.toml`
    + 編輯toml內容： A. [baseURL]改成步驟3負責網站本身的repo網址(通常是https://[user_name].github.io/)；B. [title]改隨意（會顯示往站上）；C. [theme]改成前幾步驟挑選的
8. 初步測試：`hugo server`，應該會有空白模板或theme預設範本網頁
   + 有些theme偏舊，這步會出現問題，直接換一個theme比較省事
   + 正確的話bash或cmd會顯示網站生成的頁數、靜態檔案數量等資訊
   + 找到其中Web Server is available at `http://localhost:1313/...`這行，貼到瀏覽器，有出現看起來像網頁的樣子就對
9.  確認ok後要再提交一次更改到github
```bash
git add .
git commit -m "Set up website with theme"
git push origin main
```
 
 ---

#### [【下一回】自架網站筆記：使用Github + Hugo（中）](https://ah-devworks.github.io/notes/website/create_static_web_2/)