# AN OFFLINE Live Caption Translator

A simple web app that listens to speech, shows live captions, and translates them into another language in real time.

---

## What This App Does

1. **Listens** to you speak through your microphone
2. **Shows live captions** of what you said
3. **Translates** those captions into a language you choose
4. **Displays both** the original text and the translation on screen

You can also **type or paste text** to translate without using a microphone.

---

## How to Use It

1. Open the HTML file in a browser (Chrome works best)
2. Choose your **speaking language** (e.g. Cantonese, Mandarin, English)
3. Choose your **target language** (e.g. English, Spanish, Japanese)
4. Pick a **translation engine**:
   - **MyMemory** — free, no API key needed
   - **Google Cloud Translate** — requires your own API key
5. Press **Start** and begin speaking
6. Captions and translations appear live on screen
7. Press **Stop** when done, or **Clear** to wipe the screen

---

## Features

- Live speech recognition (Web Speech API)
- Real-time translation (MyMemory or Google Translate)
- Works on desktop and mobile
- Light/dark mode support
- Manual text translation box (works even without a mic)
- Safe-area padding for notched phones

---

## Supported Languages

**Speaking:**

| Language | Code |
|----------|------|
| Cantonese | zh-HK |
| Mandarin | zh-CN |
| English | en-US |
| Japanese | ja-JP |
| Korean | ko-KR |
| Spanish | es-ES |
| French | fr-FR |
| Vietnamese | vi-VN |
| Thai | th-TH |

**Translating to:**

| Language | Code |
|----------|------|
| English | en |
| Traditional Chinese | zh-TW |
| Simplified Chinese | zh-CN |
| Spanish | es |
| French | fr |
| Japanese | ja |
| Korean | ko |
| Vietnamese | vi |
| Tagalog | tl |

---

## Tech Stack

- Pure **HTML + CSS + JavaScript** — no frameworks, no build step
- **Web Speech API** for speech recognition
- **MyMemory API** (free) or **Google Cloud Translation API** for translation

---

## Project Structure

```
live-caption-translator/
│
├── index.html          # The entire app (HTML, CSS, and JS in one file)
└── README.md           # This file
```

---

## How to Run

### Option 1: Open directly

Just double-click `index.html` in your file explorer.

### Option 2: Serve locally (recommended for microphone access)

```bash
# Python 3
python3 -m http.server 8000
```

Then open:

```
http://localhost:8000
```

### Option 3: Use a live server (VS Code)

Install the **Live Server** extension, right-click `index.html`, and choose **Open with Live Server**.

---

## Code Overview

### Speech Recognition

```javascript
const SR = window.SpeechRecognition || window.webkitSpeechRecognition;
const recognition = new SR();
recognition.continuous = true;
recognition.interimResults = true;
recognition.lang = 'zh-HK';
recognition.start();
```

### Translation (MyMemory — free)

```javascript
const url = `https://api.mymemory.translated.net/get?q=${encodeURIComponent(text)}&langpair=${sourceIso}|${targetIso}`;
const resp = await fetch(url);
const data = await resp.json();
console.log(data.responseData.translatedText);
```

### Translation (Google Cloud — needs API key)

```javascript
const resp = await fetch(`https://translation.googleapis.com/language/translate/v2?key=${key}`, {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    q: text,
    source: sourceIso,
    target: targetIso,
    format: 'text'
  })
});
const data = await resp.json();
console.log(data.data.translations[0].translatedText);
```

---

## Limitations

- Speech recognition only works in browsers that support the Web Speech API (mainly Chrome)
- Microphone access requires **HTTPS** or **localhost**
- MyMemory has daily usage limits
- Google Translate requires a paid API key
- Safari and Firefox have limited or no speech recognition support

---

## Browser Support

| Browser | Speech Recognition | Translation |
|---------|-------------------|-------------|
| Chrome (desktop) | ✅ | ✅ |
| Chrome (Android) | ✅ | ✅ |
| Edge | ✅ | ✅ |
| Safari |  Limited | ✅ |
| Firefox | ❌ | ✅ |

---

## What I'm Doing in This Repo

I'm building a **browser-based live caption and translation tool**. The goal is to help people understand speech in real time across languages — useful for meetings, lectures, travel, or accessibility.

The whole app lives in a single HTML file for simplicity, so anyone can open it and start using it immediately.

---

## Future Ideas

- [ ] Save transcript history
- [ ] Export captions as `.txt` or `.srt`
- [ ] Add more languages
- [ ] Offline translation support
- [ ] Multi-speaker detection
- [ ] Dark/light theme toggle button

---

## License

MIT — free to use, modify, and share.
