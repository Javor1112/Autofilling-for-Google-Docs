# AutoTyper for Google Docs — Chrome Extension

Automatically types any text into Google Docs character by character, simulating real keystrokes. No manual typing required.

---

## Installation (Developer Mode)

1. Open Chrome and go to `chrome://extensions/`
2. Enable **Developer mode** (toggle in the top-right corner)
3. Click **Load unpacked**
4. Select the `autotyper-extension` folder
5. The AutoTyper icon will appear in your Chrome toolbar

---

## How to Use

1. Open a **Google Doc** in Chrome
2. Click the **AutoTyper** extension icon
3. Paste or type the text you want auto-typed
4. Adjust the **typing speed** (10–300 WPM)
5. Optionally enable **Typo mode** for realistic human-like typing
6. Click **▶ Start typing**
7. Switch back to your Google Doc — AutoTyper will begin typing immediately

You can **Pause** mid-session and **Resume** at any time. Click **Stop** to cancel.

---

## Features

| Feature | Description |
|---|---|
| Character-by-character typing | Fires real keyboard events — Google Docs registers each keystroke |
| Adjustable WPM | 10 to 300 words per minute with human jitter |
| Typo mode | Randomly introduces and self-corrects typos for realism |
| Paste from clipboard | One-click clipboard import |
| File import | Import `.txt`, `.md`, or `.html` files |
| Templates | Save and reuse text snippets |
| Session history | Last 20 sessions, click any to reload |
| Pause / Resume | Resume exactly where it left off |
| Progress bar | Live character count and percentage |

---

## Permissions Used

| Permission | Why |
|---|---|
| `activeTab` | To detect which tab is a Google Doc |
| `scripting` | To inject the content script into the Docs tab |
| `storage` | To save templates and history locally |
| `host_permissions: docs.google.com` | To run the typing script inside Google Docs |

No data leaves your browser. Everything is stored locally.

---

## Troubleshooting

**Text isn't appearing in the Doc**
- Make sure a Google Doc is open and focused in the active Chrome tab
- Try clicking inside the Doc first, then clicking Start in the extension
- Refresh the Doc page and try again

**"No Google Doc open" error**
- The active tab must be a `docs.google.com/document/...` URL
- Open your document in the same window as the extension popup

**Typing stops mid-way**
- This can happen if focus shifts away from the Doc
- Keep the Doc tab active while typing is in progress

---

## File Structure

```
autotyper-extension/
├── manifest.json       # Extension config & permissions
├── popup.html          # Extension popup UI
├── popup.js            # Popup logic (UI, storage, messaging)
├── content.js          # Injected into Google Docs — handles typing
├── icons/
│   ├── icon16.png
│   ├── icon48.png
│   └── icon128.png
└── README.md
```

---

## Technical Notes

Google Docs uses a custom canvas-based editor that intercepts keyboard events at the `iframe` level. AutoTyper fires `KeyboardEvent` + `InputEvent` (`insertText`) pairs directly into the Docs text event target iframe, which is the same mechanism real keystrokes use. This is why it works where simple `innerHTML` injection does not.
