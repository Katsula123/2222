# 台灣汽車日報｜手動更新版

這是一個可以部署到 GitHub Pages 的靜態汽車新聞網站。**此版本不會自動蒐集或更新新聞**，沒有 GitHub Actions 自動更新流程，也不需要 Python 或額外套件。

## 專案檔案

- `index.html`：網站首頁、CSS 樣式、新聞分類與前端 JavaScript。
- `news.json`：手動維護的新聞資料。網站會讀取這個檔案來顯示文章。

## 部署到 GitHub Pages

1. 解壓縮專案 ZIP。
2. 將 `index.html` 與 `news.json` 上傳到 GitHub Repository 根目錄，覆蓋同名檔案。
3. 在 Repository 的 **Settings → Pages**，確認已選擇 `Deploy from a branch`、`main`、`/(root)`。
4. 等待 Pages 部署完成後，開啟網站網址並重新整理。

### 如果你沿用之前的 Repository，務必停用舊的自動更新流程

舊專案可能還留有 `.github/workflows/update-news.yml`。只上傳這個手動版 ZIP **不會自動刪除 Repository 裡舊有的檔案**，所以請：

1. 在 GitHub 的 **Code** 頁面開啟 `.github` → `workflows` → `update-news.yml`。
2. 點擊檔案頁面的刪除（垃圾桶）圖示。
3. 按 `Commit changes` 確認刪除。
4. 之後 Actions 裡的舊自動更新工作流程就不會再依排程執行。

`scripts/fetch_news.py` 與 `requirements.txt` 即使留著也不會自行執行；若想整理專案，也可以一併刪除 `scripts` 資料夾與 `requirements.txt`。

## 如何手動新增或修改新聞

1. 在 GitHub Repository 的 **Code** 頁面點擊 `news.json`。
2. 點擊鉛筆圖示（Edit this file）。
3. 在 `items` 陣列中新增一筆新聞，或修改既有新聞。
4. 修改 `updated_at` 為這次整理日期（格式 `YYYY-MM-DD`）。
5. 按 `Commit changes`。GitHub Pages 部署完成後，網站就會顯示修改內容。

每則新聞使用以下欄位：

```json
{
  "title": "新聞標題",
  "summary": "簡短摘要，請用自己的話整理",
  "category": "新車上市",
  "source": "新聞來源名稱",
  "published_at": "2026-10-19",
  "url": "https://example.com/original-article",
  "image": "https://example.com/authorized-car-photo.jpg"
}
```

可用分類必須與網站按鈕相同：`新車上市`、`試駕評測`、`車價資訊`、`品牌動態`、`交通法規`、`產業新聞`。

注意事項：

- `url` 必須是原始新聞文章的完整網址。
- 若沒有可合法使用的圖片，`image` 可以填空字串 `""`，網站會顯示汽車示意圖。
- 新聞圖片、文章與品牌素材的權利屬原始權利人；公開使用前請確認來源的授權與使用條款。
- JSON 格式很嚴格：字串要用雙引號、每個欄位之間要有逗號，但最後一個欄位後面不能多逗號。
- 本網站只展示標題、短摘要與連結，完整內容請前往原始網站閱讀。

## 常見問題

**為什麼我改了 news.json，網站卻沒有變？**

請先確認你已按 `Commit changes`，再等待 GitHub Pages 部署完成並強制重新整理頁面（Windows：`Ctrl + F5`）。

**為什麼某些新聞圖片沒有顯示？**

來源網站可能限制外部圖片顯示，或圖片網址已變更。可以換成有授權且可公開存取的圖片網址；若沒有圖片，網站會自動顯示示意圖。

**這個版本會自動更新嗎？**

不會。新聞只會在你手動修改並提交 `news.json` 後更新。
