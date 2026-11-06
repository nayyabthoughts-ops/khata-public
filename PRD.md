# Khata — PRD (Product Requirements Document)

Date: 2026-11-05 · Status: v1 built (code in this folder)

## 1. Goal
A private, voice-first expense diary ("khata") for one person, installed on an Android phone with its own icon. Open the app → it listens → the person says what she spent → it saves automatically in the right category and answers by voice. No typing, no buttons in normal use.

## 2. User
- One user (the owner). Lives in Spain. Currency: euro (€).
- Speaks Urdu/Hindi mixed with English and some Spanish shop names (Mercadona, Lidl, Consum).
- New to technology: every screen text is simple Roman Urdu.

## 3. Features (v1)
### F1. Hands-free voice input
- App starts listening automatically when opened or brought back to the screen (Web Speech API, `webkitSpeechRecognition`).
- Default language `hi-IN` (understands mixed Urdu/Hindi best). Options: `ur-PK`, `en-IN`, `es-ES`.
- After answering, it listens again. Stops after ~3 silent tries, or when she says "bas, shukriya". Tapping the big red mic restarts.
- A small text box is a fallback.

### F2. Understanding the sentence (on the phone, no AI server)
- Finds the amount: digits, "20 euro", "€20", Devanagari/Urdu digits, common number words (das, bees, pachas, सौ…).
- Finds the category by keywords: Grocery, Ghar/Kiraya, Bills, Safar, Sehat/Dawai, Mobile, Kaghazat/Fees, Ghar bheje, Bahar khana, Kapre/Shopping, Tohfa/Ghoomna, Digar.
- Each category is marked **Zaroorat** (need) or **Extra**.
- Several items in one sentence: "metro 10 aur kebab 8 euro" → two entries.
- Commands: "kitna bacha hai", "is hafte kitna kharcha hua", "is mahine ka hisaab", "budget 250", "aakhri wala mita do", "bas, shukriya".

### F3. Budget and alert
- Monthly budget (default €200) and alert level (default €20 left), set in Settings.
- Alert banner + spoken warning when money left ≤ alert level; red banner when over budget.

### F4. Reports
- Khata tab: this month's entries by day; category can be changed by tapping it; entries can be deleted (✕ then "Pakka?").
- Is hafta: total since Monday, need vs extra, by category, compared with last week.
- Is mahina: total, need vs extra, by category, compared with last month; lists what went up.
- On the first open of a new week/month, shows last week's/month's total.

### F5. Voice replies
- Uses the phone's built-in voice (`speechSynthesis`), preferring Urdu, then Hindi, then English.

## 4. Privacy and security
- **All data stays on the phone** (`localStorage`). No server, no account, no analytics, no AI API, no keys.
- The code is public on GitHub Pages; the spending data is never in the code or on GitHub.
- Backup: "Hisaab copy karo" copies the data as text so she can send it to herself.
- No external scripts. Only Google Fonts (with system-font fallback).

## 5. Phone-friendly / install
- PWA: `manifest.webmanifest`, icons (192, 512, maskable), service worker `sw.js` for offline use.
- Installed from Chrome on Android: ⋮ → "Install app" / "Add to Home screen".
- One column layout, big touch targets, light and dark mode.

## 6. Out of scope (v1)
- Push notifications for weekly/monthly reports (needs a server).
- Syncing between devices.
- Listening while the app is closed.

## 7. Known limits (to test)
- Whether Chrome starts the mic with no tap at all after permission is given (depends on phone).
- Which voice the phone uses for replies.
- Keyword categories may miss some words; she can fix them by tapping the category.

## 8. Files
- `index.html` — the whole app
- `manifest.webmanifest` — app name, icon, colors
- `sw.js` — offline support
- `icons/` — app icons
