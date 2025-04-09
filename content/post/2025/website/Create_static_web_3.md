---
title: 自架網站筆記：使用Github + Hugo（下）
date: 2025-04-09
tags: ["hugo","blog","website"]
Description  : "——自架靜態網站的過程紀錄．下篇——"
featured: true
---

#### [自架網站筆記：使用Github + Hugo（上）](https://ah-devworks.github.io/notes/website/create_static_web_1/)
#### [自架網站筆記：使用Github + Hugo（中）](https://ah-devworks.github.io/notes/website/create_static_web_2/)

---

### 更新靜態網站內容的方法
1. 把新內容準備好（Markdown, image等檔案要放到Content-Repo裡各自對應的子資料夾），更新push。
```bash
git add .
git commit -m "新增文章：new-post"
git push origin main  # 如果檔案較多較大，push後建議等一下
```
2. 確認前一步驟content-repo已經上傳、更新好了之後，轉到Web-Repo
3. 🌟Web-Repo 更新submodule: `git submodule update --remote`
4. (可選) git status 檢查content-repo檔案有引入
5. `git add [檔案]` 後，可以先 `hugo server` 本地確認網站更新無誤；或直接 `hugo` 後把 public/ 內新檔覆蓋更新到母資料夾
6. `git add .` --> `git commit` --> `git push origin main` ，過幾分鐘 github 處理好，刷新網站即可。
   + 可以到github 的web-repo檢查進度（如下圖✅｜萬一出現❌表示哪裡出了問題，要回頭檢查）
<img src="/img/post/github_check_sucess.jpg" title="github_check_sucess_20250409">


### 常見QA
1. **【本機跑正常，GitHub Pages 樣式卻很簡陋】**：一路做到PART III都沒問題，但實際網址連到的網頁外觀卻跟「hugo server」測試時「http://localhost:1313/...」的網頁明顯不同。
    + 通常是baseURL沒設定好，或是publish的相對路徑、theme路徑或資源沒有正確被拷貝，導致Github Pages抓不到樣式
    + 建議前述PART I的步驟7第二點再次確認：baseURL應該會是「https://[你的使用者名稱].github.io/」
    + 確認hugo生成的public檔案必須全部拷貝到前一層資料夾（通常就是「/[你的使用者名稱].github.io」）
    + 且每次修正後，都要重新hugo、update一次，讓Github Pagese更新（通常push後不會即時刷新，要等一下 --> 可看github倉庫-Settings-Pages網站網址底下的小字「Last deployed by @user xxx minutes ago」來判斷刷新了沒）
    + 有時候可能是theme本身的問題，假如theme本身有exampleSite（contents, layout等資料夾），建議可以複製回去、保持樣式，之後再來把範本內文取代掉

---
---

#### 個人心得
+ 拿關鍵字去google能找到很多「X分鐘快速架設網站」的文章或影片，但實際操作發現比較適合「就只是要個網站放些簡單文章/日記而已」的人，要多些功能的話，那複雜度就會開始上升了。
+ 就我個人而言，首先構思網站的架構、層級劃分、文章類型就花了些時間；
挑theme又花了些時間，第一個挑的theme在clone時還碰到一堆缺少前製套件之類的奇怪狀況……；
再來又開始想「要把Content-Repo當成submodule？還是反過來把Web-Repo當成Content-Repo的sub？」之類，攸關彈性跟未來維護性等等的問題……
+ 明明簡單來說就只有兩個repo而已，花了快10小時，至少打掉重來三次……可能我是資質比較駑鈍的那種吧(
+ 之後或許會不定期更新有關UI調整、自動部署（GitHub Actions/Hugo Deploy）、Project導入等等的筆記。


---

> 有任何疑問歡迎[私信我](mailto:a.h.devworks@gmail.com>)
> 只是回信可能比較慢，請見諒。要是一直沒回覆，可以隔週再寄一次。

> --- A.H.Dev-Works.

---

##### 參考資源
+ [HUGO Docs](https://gohugo.io/documentation/)
+ [Creating a Blog with Hugo and Github in 10 minutes](https://www.youtube.com/watch?v=LIFvgrRxdt4)  --> 注意這教的是把Web-Repo當成submodule的方法
+ [【懶人包】使用 Hugo 5 分鐘內快速架設個人網站，號稱現在最快的自架網站方式](https://medium.com/pm的生產力工具箱/懶人包-使用-hugo-5-分鐘內快速架設個人網站-號稱現在最快的自架網站方式-99659c7c727a)  --> 主要參考Hugo
+ [從零開始: 用github pages 上傳靜態網站](https://medium.com/進擊的-git-git-git/從零開始-用github-pages-上傳靜態網站-fa2ae83e6276)
+ [Lightbi-Demo](https://lightbi-hugo-theme.netlify.app/en/)
+ [genryu-font](https://github.com/ButTaiwan/genryu-font)