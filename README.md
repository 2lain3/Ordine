# 歸序 Ordine — 現代簡約個人記帳 Web App / Minimalist Expense Tracker

<p align="center">
  <b>🌿 一款專為行動裝置打造的極簡風格個人記帳 Web App，支援中英雙語、智慧語音解析、Supabase 雲端同步與 iOS 捷徑自動化。</b><br>
  <i>A mobile-first, minimalist personal expense tracker with bilingual UI, smart NLP/voice parsing, Supabase sync, and iOS Shortcuts integration.</i>
</p>

---

## 🇹🇼 繁體中文說明 (Traditional Chinese)

### ✨ 核心亮點
- 📱 **手機優先排版（Mobile-First）**：專為智慧型手機設計，加入主畫面（PWA）後全螢幕無網址列運行。
- 🌐 **一鍵雙語切換**：支援「繁體中文」與「English」無縫即時切換。
- 🎙️ **智慧語音與自然語言解析**：
  - 支援 Web Speech API 語音輸入。
  - 自然語言解析：例如輸入或說出 `午餐 麥當勞 150 信用卡` 或 `星巴克 160`，自動識別類別、金額與店家。
- 📊 **即時儀表板與圓餅圖**：
  - 本月總支出、動態預算進度條、超支警示與剩餘天數。
  - Chart.js 圓餅圖動態統計 6 大類別（餐飲、交通、購物、娛樂、日常、其他）。
- ☁️ **Supabase 雲端同步 & 離線支援**：
  - 未填寫 Key 時自動存於本機瀏覽器（localStorage）。
  - 設定 Supabase 後自動開啟即時雲端同步。
- ⚡ **iOS 捷徑（Shortcuts）自動記帳**：提供專屬 Webhook API 規格，搭配 Siri 或信用卡消費簡訊自動新增明細。
- 📥 **CSV 報表匯出**：一鍵將所有收支明細匯出為標準 CSV 試算表。

---

### 🚀 快速上手（免本機下載，直接使用 GitHub Pages）

1. **建立 GitHub 儲存庫**：
   - 在 GitHub 建立一個公開專案 `ordine`。
2. **新增檔案**：
   - 建立檔案 `index.html`，貼入本專案的完整 HTML 程式碼並 Commit。
3. **開啟 GitHub Pages**：
   - 到儲存庫的 **Settings $\rightarrow$ Pages**。
   - Source 選擇 `Deploy from a branch`，Branch 選擇 `main` / `/(root)` 儲存。
   - 稍等 1 分鐘即可取得專屬 Web App 網址：`https://<你的GitHub帳號>.github.io/ordine/`。
4. **安裝到手機主畫面**：
   - 在 iPhone Safari 開啟該網址，點擊「**分享**」$\rightarrow$「**加入主畫面**」。

---

### 🗄️ Supabase 資料庫建表 SQL

前往 Supabase 的 **SQL Editor** 執行以下腳本：

```sql
CREATE TABLE IF NOT EXISTS public.transactions (
    id TEXT PRIMARY KEY,
    amount NUMERIC NOT NULL,
    category TEXT NOT NULL,
    note TEXT,
    date DATE NOT NULL DEFAULT CURRENT_DATE,
    time TEXT,
    payment_method TEXT DEFAULT '現金',
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

ALTER TABLE public.transactions ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Allow public read" ON public.transactions FOR SELECT USING (true);
CREATE POLICY "Allow public insert" ON public.transactions FOR INSERT WITH CHECK (true);
CREATE POLICY "Allow public update" ON public.transactions FOR UPDATE USING (true);
CREATE POLICY "Allow public delete" ON public.transactions FOR DELETE USING (true);
```

---

## 🇺🇸 English Description

### ✨ Key Features
- 📱 **Mobile-First Experience**: Designed specifically for smartphones. Install to Home Screen (PWA) for a clean, full-screen native app experience without browser bars.
- 🌐 **Instant Bilingual Support**: Switch between **Traditional Chinese** and **English** with one click.
- 🎙️ **Smart NLP & Voice Input**:
  - Built-in Web Speech API for hands-free voice expense logging.
  - Smart parsing: Type or speak `Lunch McDonald 150 Card` or `Starbucks 160` to automatically fill category, amount, and store details.
- 📊 **Real-time Dashboard & Doughnut Chart**:
  - Monthly total spend, dynamic budget progress bar, over-budget alerts, and remaining month countdown.
  - Dynamic Chart.js breakdown across 6 main categories (*Dining, Transport, Shopping, Entertainment, Living, Other*).
- ☁️ **Supabase Cloud Sync & Offline Local Mode**:
  - Pure offline mode (localStorage) by default.
  - Switch to instant cloud database sync upon adding your Supabase credentials.
- ⚡ **iOS Shortcuts Automation**: Compatible with iOS Shortcuts and Siri for instant one-tap or SMS-triggered expense logging via REST API.
- 📥 **CSV Data Export**: Download your full transaction history into a standard CSV spreadsheet anytime.

---

### 🚀 Quick Start with GitHub Pages (Zero Local Footprint)

1. **Create Repository**:
   - Create a new public repository named `ordine` on GitHub.
2. **Add Code**:
   - Create a new file named `index.html`, paste the complete code from this project, and click **Commit changes**.
3. **Enable GitHub Pages**:
   - Navigate to **Settings $\rightarrow$ Pages**.
   - Under Source, select `Deploy from a branch` $\rightarrow$ Branch: `main` / `/(root)` $\rightarrow$ Save.
   - Your Web App will be live at: `https://<your-username>.github.io/ordine/`
4. **Add to Home Screen**:
   - Open the URL in iPhone Safari $\rightarrow$ Tap **Share** $\rightarrow$ Tap **Add to Home Screen**.

---

### 📲 iOS Shortcuts Integration (REST API Webhook)

- **URL**: `https://<YOUR_SUPABASE_ID>.supabase.co/rest/v1/transactions`
- **Method**: `POST`
- **Headers**:
  - `apikey`: `<YOUR_ANON_KEY>`
  - `Authorization`: `Bearer <YOUR_ANON_KEY>`
  - `Content-Type`: `application/json`
- **Request Body (JSON)**:
  ```json
  {
    "amount": 150,
    "category": "餐飲",
    "note": "午餐麥當勞",
    "payment_method": "信用卡",
    "date": "2026-08-24",
    "time": "12:30"
  }
  ```

---

### 🛠️ Tech Stack
- **Frontend**: Vanilla HTML5, JavaScript (ES6+), Tailwind CSS (CDN), Lucide Icons
- **Charts**: Chart.js
- **Backend / Database**: Supabase (PostgreSQL REST API)
- **Deployment**: GitHub Pages / Netlify / Vercel

---
<p align="center">Made with ❤️ for mindful financial tracking with <b>歸序 Ordine</b>.</p>
