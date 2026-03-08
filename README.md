# 📵 Anti-Distraction — WhatsApp Smart Filter

Automatically scans your unread WhatsApp chats and surfaces only the messages that actually matter — work, meetings, deadlines, and urgent requests — so you can ignore the rest without missing anything important.

Built with Python, Selenium, and Google Gemini AI.

---

## How It Works

1. Opens WhatsApp Web in a Chrome browser
2. Detects all chats with unread messages
3. Enters each chat and takes a screenshot
4. Sends the screenshot to Gemini AI, which reads and classifies the messages
5. Filters out already-seen messages to avoid duplicates
6. Prints a clean summary of only the important ones

---

## Features

- 🤖 **AI-powered classification** — Gemini 2.0 Flash reads full message context, not just previews
- 🔔 **Unread chat detection** — multiple selector strategies to handle WhatsApp Web's changing HTML
- 📋 **Deduplication** — tracks previously seen messages so you never get the same alert twice
- 🧹 **Auto cleanup** — screenshots are deleted after analysis
- 💼 **Focuses on what matters** — ignores casual greetings, flags work, deadlines, and appointments

---

## Requirements

- Python 3.8+
- Google Chrome
- A [Google Gemini API key](https://aistudio.google.com/app/apikey)

---

## Installation

**1. Clone the repo**
```bash
git clone https://github.com/Starky292005/anti-distraction.git
cd anti-distraction
```

**2. Install dependencies**
```bash
pip install -r requirements.txt
```

**3. Set your Gemini API key**

Create a `.env` file in the project root:
```
GEMINI_API_KEY=your_api_key_here
```

Or export it directly in your terminal:
```bash
export GEMINI_API_KEY=your_api_key_here   # macOS / Linux
set GEMINI_API_KEY=your_api_key_here      # Windows
```

---

## Usage

```bash
python main.py
```

On first run, a Chrome window will open with a WhatsApp Web QR code. Scan it with your phone. The script will wait up to 60 seconds for you to log in, then automatically begin scanning your unread chats.

**Example output:**
```
🚀 ENHANCED WhatsApp Filter
🔍 Scanning for unread chats...
🔔 Found unread chat: Work Group
🤖 Analyzing chat: chat_Work_Group.png

🚨 IMPORTANT MESSAGES FOUND: 1
============================================================
1. 📨 From: Manager
   💬 Message: Team standup moved to 3pm today, please confirm attendance
   📋 Reason: Meeting schedule change requiring response
============================================================
✅ Scan complete!
```

---

## Project Structure

```
anti-distraction/
├── main.py                  # Entry point — orchestrates the full scan
├── whatsapp_scraper.py      # Selenium automation for WhatsApp Web
├── message_analyzer.py      # Gemini AI integration for message classification
├── message_tracker.py       # Deduplication using a local JSON history file
├── config.py                # Configuration (API key, intervals)
├── requirements.txt
└── message_history.json     # Auto-generated — tracks seen messages
```

---

## Configuration

| Variable | Description | Default |
|---|---|---|
| `GEMINI_API_KEY` | Your Google Gemini API key | *(required)* |
| `SCREENSHOT_INTERVAL` | Seconds between scans (if running in loop mode) | `60` |

---

## Dependencies

| Package | Purpose |
|---|---|
| `selenium` | Browser automation for WhatsApp Web |
| `webdriver-manager` | Auto-installs the correct ChromeDriver |
| `google-generativeai` | Gemini AI API client |
| `Pillow` | Image loading for AI analysis |

---

## Limitations

- Requires WhatsApp Web to remain open and logged in
- Gemini AI classification may occasionally miss or misclassify messages
- WhatsApp Web's HTML structure can change with updates, which may break selectors
- Currently scans once per run — loop/scheduling support is planned

---

## Privacy

- Screenshots are taken locally on your machine and sent to the Gemini API for analysis
- Screenshots are deleted immediately after analysis
- Message hashes (not content) are stored locally in `message_history.json` for deduplication
- No data is sent anywhere except the Gemini API

---

## Contributing

Pull requests are welcome! If a WhatsApp Web update breaks the selectors in `whatsapp_scraper.py`, opening an issue with the new HTML structure is especially helpful.

---

## License

MIT
