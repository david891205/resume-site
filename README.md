# 呂哲言履歷網站

開啟 `index.html` 即可瀏覽履歷網站。網站為靜態 HTML，樣式與互動都寫在同一個檔案內，圖片放在 `assets/` 資料夾。

一頁式 PDF 履歷已輸出為 `assets/lv-che-yen-onepage-resume.pdf`，來源檔為 `one-page-resume.html`。若日後要修改 PDF 內容，先改 HTML，再重新列印成 PDF。

## 圖片與簡報如何永久公開

網站上所有公開圖片、PDF、PPT 與簡報預覽圖都已整理到 `assets/`。部署到 GitHub Pages、Netlify、Vercel 或 Cloudflare Pages 後，這些檔案會跟 `index.html` 一起公開，不需要另外找圖床，也不要使用 `C:\Users\...` 這種本機路徑。

會議諸葛展示影片使用 Google Drive iframe 嵌入，原因是本機影片檔約 168MB，超過 GitHub 一般單檔上傳限制。若要讓外部訪客在網站上直接播放，Google Drive 檔案分享權限需設為「知道連結的任何人」且角色為「檢視者」。

若 GitHub 帳號是 `david891205`、repository 名稱是 `resume-site`，部署完成後圖片網址會像這樣：

```text
https://david891205.github.io/resume-site/assets/profile-photo.png
https://david891205.github.io/resume-site/assets/esgpb-chatbot-screenshot.png
https://david891205.github.io/resume-site/assets/smart-travel-slides/slide-01.png
https://david891205.github.io/resume-site/assets/lv-che-yen-onepage-resume.pdf
```

只要 repository 不刪除、GitHub Pages 不關閉，這些圖片連結就會持續有效。

## 讓別人可以點進網站

最簡單的方式是 GitHub Pages：

1. 建立一個 GitHub repository，例如 `resume-site`。
2. 上傳 `index.html`、`README.md` 與整個 `assets/` 資料夾。
3. 進入 repository 的 `Settings` → `Pages`。
4. Source 選 `Deploy from a branch`，branch 選 `main`，folder 選 `/root`。
5. 儲存後等待部署完成，GitHub 會給你一個網址，例如 `https://你的帳號.github.io/resume-site/`。

## 用指令上傳到 GitHub

目前 Git for Windows 與 GitHub CLI 已可執行。第一次上傳前需要先登入 GitHub：

```powershell
gh auth login
```

如果 PowerShell 顯示 `gh` 找不到，先關掉視窗重開一次；或直接改用完整路徑：

```powershell
& "C:\Program Files\GitHub CLI\gh.exe" auth login
```

登入後可在本資料夾執行：

```powershell
git init
git branch -M main
git add index.html README.md assets .gitignore .nojekyll
git commit -m "Publish resume website"
gh repo create resume-site --public --source=. --remote=origin --push
```

若重開後仍不能直接使用 `gh`，最後一行改成：

```powershell
& "C:\Program Files\GitHub CLI\gh.exe" repo create resume-site --public --source=. --remote=origin --push
```

接著到 GitHub repository 的 `Settings` → `Pages`，選 `Deploy from a branch`、`main`、`/root`。

## 不用 GitHub 的公開方式

也可以使用以下方式：

- Netlify Drop：把整個網站資料夾或 zip 檔拖進 https://app.netlify.com/drop
- Vercel：匯入 GitHub repository，或用 Vercel CLI 部署靜態網站
- Cloudflare Pages：上傳 GitHub repository 或用 Direct Upload

這個網站是純靜態頁面，只要 `index.html` 與 `assets/` 在同一層，以上平台都可以部署。
