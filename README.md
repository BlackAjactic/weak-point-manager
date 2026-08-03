# weak-point-manager

# Physics Trainer ⚛️ · Smart Management System for Physics Competition Weak Points

> A physics competition review tool built on the SM-2 spaced repetition algorithm. Record weak knowledge points, get automatically scheduled reviews, compose and print practice papers, with safe local-only storage that works fully offline.

---

## 📖 About

**Physics Trainer** is a **pure frontend, zero-backend** review tool for physics competitions. It digitizes the weak points you keep getting wrong: each weak point can carry **question/answer images or PDF attachments** plus **text with LaTeX formulas**, while the built-in **SM-2 spaced repetition algorithm** (Ebbinghaus memory curve) automatically schedules your review so that the more you master a topic, the longer the intervals become — and the more you forget it, the more often it comes back.

It also ships with a **Print Designer** that lets you select weak points and typeset them into a "practice paper / answer booklet," with customizable cover pages, headers, and multi-item layouts — a practical companion for focused exam prep.

---

## ✨ Key Features

### 📚 Weak Point Library
- Add weak points: title, category, difficulty rating, and error analysis
- **LaTeX formula support** (`$...$` / `$$...$$`) with live preview + MathJax rendering
- Separate question and answer text fields, both accepting formulas
- Attachments: **images** (drag & drop, click to select, **Ctrl+V paste**, mobile camera capture) and **PDFs** (selective page import, adjustable render resolution)
- Attachments can be reordered by drag, rotated, renamed, and deleted
- Search, category filter, status filter, and multi-axis sorting

### 🗓️ SM-2 Spaced Repetition
- Classic **SuperMemo-2 algorithm**: ease factor (EF), dynamic intervals, consecutive success count
- Four self-assessment levels: **Forgot / Hard / Good / Easy**, adaptively adjusting next review time
- Overview of today's tasks, overdue items, and next 7 days at a glance
- Per-card memory state: New / Learning / Mastered, with a mastery progress bar
- **Study heatmap** (last 6 months / last year), consecutive-day streaks, category & interval distribution charts

### 🖨️ Print Designer
- Select multiple cards and **compose a print job**, freely drag to reorder
- Content options: questions, answers, cover page
- Layout modes: **interleaved** or **appendix answer booklet** (with divider page)
- Grid layouts: 1 item/page, 2 items/page, 4 items/page
- Adjustable paper size / orientation / margins (A4 / A5 / Letter, portrait / landscape)
- Customizable header info (difficulty / mastery / interval / description / print date / page number)
- **Grayscale (ink-saving)** mode
- Text flows from the **top-left corner** with fine-tuned font sizes; long text auto-paginates without clipping; images align to the top and center
- Live print preview (rendered first, then opens the system print dialog)

### 💾 Data Safety
- **IndexedDB primary storage with localStorage fallback** — capacity ranges from ~5 MB up to hundreds of MB / a few GB
- Request browser **persistent storage** to reduce the risk of automatic clearing
- Export **full backup** (with attachments) or **light backup** (text & progress only) as JSON
- Import with **per-item preview and checkbox selection**, supporting **merge / replace** modes
- Destructive operations (delete, clear all) require multiple confirmations

### 🌗 Appearance & Modes
- Light / Dark theme, one-click toggle with persistence
- **Study Mode / Browse Mode**: Browse mode disables review/memory features, focusing on library management and printing/export

---

## 🚀 Getting Started

The project is a **single HTML file** — no installation, no build step, no backend.

1. Download `index.html` (in the repository root)
2. Open it in a browser (recommended: **Chrome / Edge / Firefox**)
3. Optional internet: MathJax (formula rendering) and pdf.js (PDF import) are pulled from a CDN on first load. Even **offline**, all features work except LaTeX typesetting and PDF import.

> 💡 For regular use, export a backup regularly via "💾 Data → Export" (especially before updating the app or clearing browser cache).

---

## 🖥️ Tech Stack

| Module | Description |
|--------|-------------|
| **Plain HTML / CSS / Vanilla JS** | No framework dependency, self-contained single file |
| **IndexedDB** | Primary storage (kv store + attachment blob store) |
| **localStorage** | Legacy data compatibility + fallback storage |
| **SM-2 Algorithm** | Custom implementation for spaced-repetition scheduling |
| **MathJax 3** | LaTeX math typesetting |
| **pdf.js** | PDF parsing and page rendering for import |

---

## 📁 Project Structure

```
physics-trainer-weakpoint-manager/
└── index.html      # Single-file app (HTML + CSS + JS all inline)
```

---

## 🎯 Suggested Workflow

1. **Add a weak point**: Click "＋ Add Weak Point" in the top-right. Fill in title, category, and difficulty; optionally paste question/answer text (with formulas) or upload screenshots / PDFs
2. **First study**: New cards automatically enter today's tasks. Click "✓ Complete Review" and **self-assess honestly** (Forgot / Hard / Good / Easy)
3. **Daily review**: Follow "Today's Tasks" on the dashboard and the "Review Plan". The more you master a card, the longer the intervals — less effort needed
4. **Pre-exam sprint**: In the Library, check high-frequency weak points → "🖨️ Compose Print" to generate a practice paper / answer booklet and print it
5. **Regular backup**: "💾 Data → Export Full Backup", and store the JSON file somewhere safe

---

## 💡 Tips

- **Paste screenshots**: With the editor open, press `Ctrl+V` to drop clipboard images into the currently selected "Questions" or "Answers" section (toggle the target with "📋 Paste here")
- **Multi-image layouts**: In printing, "2 items/page" suits medium-length content; "4 items/page" is great for a quick overview
- **Answer self-test**: In the detail view, answers are blurred by default — tap "Test yourself first, click to reveal" to check after attempting
- **Selective PDF import**: When importing a PDF you can specify a page range (e.g., `1-3,5,8-9`) to avoid importing an entire book and wasting space
- **Offline use**: After the first online load caches the CDN scripts, the single file can run locally offline

---

## 🔧 FAQ

**Q: Will I lose data if I switch computers or browsers?**
A: Data is stored only in the local browser of the current device. To move, export a **full backup** in "💾 Data" first, then import it on the new device.

**Q: Why do I get a "storage full" message?**
A: Image/PDF attachments are stored as compressed base64 in the browser. If space runs out, lower the resolution/quality in "Upload & Compression Settings" or delete unneeded attachments.

**Q: LaTeX formulas aren't showing?**
A: MathJax requires an internet connection to load from CDN. Offline, formulas appear as raw text; all other features still work.

**Q: What's the difference between Browse Mode and Study Mode?**
A: Browse Mode disables review/memory features (review plan, self-assessment, heatmap) and focuses on library CRUD, printing, and export. Study Mode restores the full review functionality.

---

## 🛡️ Privacy

- All data (including attachments) is stored **only in your local browser** and is **never uploaded to any server** — no accounts, no cloud sync, no tracking
- External requests are limited to CDN static assets (MathJax, pdf.js)

---

## 🧩 Accessibility & Compatibility

- Modals include `role="dialog"` / `aria-label` semantics; ESC closes dialogs; arrow keys navigate the image lightbox
- Focus capture/restore and a Tab focus trap keep keyboard navigation within open dialogs
- Responsive on mobile: collapsible top nav, single-column forms, camera capture support
- Recommended: a fairly recent version of Chrome / Edge / Firefox / Safari

---

## 📜 License

A personal learning tool, provided for personal and educational use.

---

**Happy studying, and all the best on the physics competition! 🏆⚛️**
