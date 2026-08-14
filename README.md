# 🧠 Annu AI Brain

**Annu** ek advanced, voice + text dono se control hone waali Windows/Mac/Linux desktop AI assistant hai — Python aur Google Gemini par based. Ye apps kholna/band karna, YouTube pe gaana bajana, web research karna, professional Excel reports banana, reminders set karna, images se text nikaalna (OCR), WhatsApp messages bhejna, aur roz subah 10 baje automatic daily briefing taiyar karna — ye sab ek hi jagah se karti hai.

> Made by [Rohit Raj](https://github.com/rohitraj345) — DataPro Services

---

## ✨ Features

### 🗣️ Conversation
- Text ya voice (Hindi, `hi-IN`) dono se baat kar sakte ho — microphone background mein continuously sunti rehti hai
- Google Gemini (`gemini-flash-latest` alias — hamesha current stable model, kabhi deprecated nahi hoga) se natural Hindi replies
- **Female voice** — `edge-tts` (natural neural Hindi voice `hi-IN-SwaraNeural`) primary, na ho to `pyttsx3` fallback jo automatically female-named voice detect karke use karta hai
- Multiple Gemini API keys rakh sakte ho — ek ki quota khatam ho to automatically dusri pe switch (`GEMINI_API_KEY_1` ... `_4`)
- 503 (server busy) errors pe automatic retry with exponential backoff

### 🧠 Memory
- **SQLite** mein har conversation ka raw log (`annu_memory.db`)
- **Semantic memory** (ChromaDB) — purani relevant baatein context ke roop mein automatically yaad rakhti/use karti hai, chat restart hone ke baad bhi

### 🖥️ System Control
- Apps kholna/band karna — "chrome kholo", "notepad kholo", "band karo" (Windows/Mac/Linux teeno par sahi command)
- Websites seedha browser mein kholna — YouTube, Gmail, Google, Instagram, Facebook, WhatsApp Web, Amazon, Flipkart, Netflix, LinkedIn, Maps
- **Screen dekhna** — screenshot lekar Gemini vision se analyze karwana ("screen dekho")
- **System info** — battery, CPU/RAM, date-time ("system info", "battery kitni hai")
- **Clipboard** read/copy voice se

### 🎵 Media
- "gana chalao <naam>" → Spotify search
- "youtube pe <naam> chalao" → seedha YouTube video **play** ho jaata hai (extra click nahi)

### 🌐 Research & Shopping
- DuckDuckGo se real-time web search — news, weather, kisi bhi topic ki research
- **Amazon/Flipkart** par product search seedha khol deti hai — jaan-boojh kar **auto-checkout/payment nahi karti** (safety ke liye, final order tumhara confirm karna hoga)

### 📋 Productivity
- **Reminders/Tasks** — "10 minute baad yaad dilana ki chai peeni hai" — background thread har 20s check karta hai
- **OCR** 📷 — koi bhi image (invoice, form, scanned doc) se text nikaal ke Desktop par save — data-entry business ke liye directly useful
- **Professional Excel reports** — bordered, banded rows, auto column-width, wrapped text, frozen header
- **Roz subah 10 AM** — automatic daily briefing (top news headlines + tumhare pending tasks) Excel mein save
- File search — sirf Desktop/Documents/Downloads mein safe search (path-traversal se protected)

### 💬 WhatsApp
- "whatsapp 9876543210 kal milte hain" → WhatsApp Web ke through message bhej deti hai (koi unofficial API key nahi, tumhari khud ki login session use hoti hai)
- Sirf ek-ek message ke liye — bulk/spam automated messaging ke liye nahi banayi gayi

### 🔒 Security
- Koi bhi user/voice input seedha shell mein nahi jaata — command injection se protected
- Har destructive action (taskkill, file access) whitelisted/sanitized inputs par hi chalta hai

---

## 🛠️ Requirements

- Python **3.9+**
- Windows / macOS / Linux (sab par test-friendly)
- Microphone (voice feature ke liye)
- Free **Google Gemini API key**

---

## 🚀 Installation

```bash
# 1. Clone the repo
git clone https://github.com/rohitraj345/annu-ai-brain.git
cd annu-ai-brain

# 2. (Recommended) Virtual environment banao
python -m venv venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # macOS/Linux

# 3. Dependencies install karo
pip install -r requirements.txt
```

### API Key setup

1. [Google AI Studio](https://aistudio.google.com/apikey) se free Gemini API key generate karo
2. Project folder mein `.env` naam ki file banao (`.env.example` ko copy kar ke rename kar sakte ho):

```env
GEMINI_API_KEY=your_key_here
```

Agar multiple keys rakhne hain (quota-rotation ke liye):

```env
GEMINI_API_KEY_1=key_one
GEMINI_API_KEY_2=key_two
```

### Optional features setup

| Feature | Extra step |
|---|---|
| OCR (image se text) | [Tesseract-OCR](https://github.com/UB-Mannheim/tesseract/wiki) binary install karo (Windows) — `pytesseract` sirf wrapper hai |
| WhatsApp messages | Browser mein [web.whatsapp.com](https://web.whatsapp.com) login rakho |
| Behtar voice | `edge-tts` already `requirements.txt` mein hai — extra setup nahi chahiye |
| Screen vision | `pyautogui` already included |
| Linux par GUI | `sudo apt install python3-tk` (tkinter stdlib ke saath nahi aata Linux par) |

### Run

```bash
python annu_brain.py
```

---

## 💬 Voice/Text Commands

| Kaam | Bolo |
|---|---|
| App kholna | "chrome kholo", "notepad kholo" |
| Website kholna | "youtube kholo", "gmail kholo" |
| Gaana (Spotify) | "gana chalao arijit singh" |
| Gaana (YouTube, direct play) | "youtube pe kesariya chalao" |
| App band karna | "chrome band karo" |
| Web research | "batao aaj ka news kya hai" |
| Shopping search | "amazon par running shoes khojo" |
| Excel report | "excel report banao" |
| Note save | "ye save karo" |
| Reminder | "10 minute baad yaad dilana ki chai peeni hai" |
| Tasks dekhna | "tasks dikhao" |
| File dhundna | "file dhundo invoice" |
| System info | "system info", "battery kitni hai" |
| Clipboard | "clipboard mein copy karo ..." |
| Screen dekhna | "screen dekho" |
| WhatsApp | "whatsapp 9876543210 kal milte hain" |
| Band karna | "exit" / "shut down app" |

---

## 📁 Project Structure

```
annu-ai-brain/
├── annu_brain.py        # Main application (single-file)
├── requirements.txt      # Dependencies
├── .env                  # API keys (git-ignored — khud banao)
├── .env.example           # Template for .env
├── annu_memory.db         # Auto-created: conversation log (git-ignored)
├── annu_tasks.db           # Auto-created: reminders/tasks (git-ignored)
└── annu_storage/            # Auto-created: semantic memory + embeddings (git-ignored)
```

---

## ⚠️ Known Limitations

- `notepad`/`excel` jaise app names Windows-specific hain; Mac/Linux par equivalent commands automatically try hoti hain lekin exact app installed hona zaroori hai
- OCR ke liye Tesseract binary alag se install karni padti hai
- WhatsApp automation `pywhatkit` par depend karta hai, jo browser tab khol ke kaam karta hai — background/headless nahi chalta
- Reminders app band hone par trigger nahi hote (background thread hai, standalone service nahi)

---

## 📄 License

Apni pasand ka license yahan add karo (MIT recommended for open-source personal projects).

---

## 🙋 Author

**Rohit Raj** — Freelance Data Entry Expert & App Developer
[DataPro Services](https://rohitraj345.github.io) · [GitHub](https://github.com/rohitraj345)
