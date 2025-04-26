# 🎬 Movie Search Frontend (Vue + Vite)

本專案為電影搜尋網站的前端介面，基於 Vue 3 + Vite 框架開發，並已部署至 Render。

---

## 🚀 專案簡介

- 搜尋現正上映的電影資訊
- 支援關鍵字篩選功能
- 串接後端 FastAPI API
- 部署於 Render Static Site

---

## 📚 技術棧

- Vue 3 (Composition API)
- Vite
- Axios
- Render Static Site

---

## 🛠 專案架構

```plaintext
├── src/
│   ├── App.vue             # 主畫面
│   ├── components/         # 可擴充的元件目錄
│   ├── main.js              # 進入點
├── package.json             # 專案設定
├── vite.config.js           # Vite設定
└── README.md                # 專案說明文件
```
## 📦 快速啟動 (本地開發)
1. 安裝依賴套件
```bash
npm install
```

2. 啟動本地開發伺服器
```bash
npm run dev
```

3. 預設開啟於：
```bash
http://localhost:5173
```

## 🌐 已部署版本
```bash
前端網址 : https://movie-frontend-zgda.onrender.com/
```

## 🔗 API 連接設定
前端Axios預設連接的後端API：
```bash
const res = await axios.get('https://movie-backend-wlvm.onrender.com/movies')
```
確保後端API已上線並支援CORS。

## ✨ 特別感謝
本專案使用了 TMDB 公開API，特此致謝。
本專案僅作為個人學習與展示用途，不用於任何商業行為。