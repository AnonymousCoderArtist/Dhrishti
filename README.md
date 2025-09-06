# Drishti – AI Assistant for the Blind

HackOdisha 5.0 Submission | Assistive AI that sees, understands, and acts for you

Drishti (meaning “vision” in Hindi) is an accessible AI assistant designed to empower blind and visually impaired users. It enables hands-free interaction with a PC via voice, describes the world and the screen in real-time using multimodal AI, and helps communicate through email and WhatsApp.

---

## Highlights
- Built for HackOdisha 5.0 with a strong focus on accessibility and independence
- End-to-end workflow: Voice in → Intelligent actions → Voice out
- Multimodal Gemini integration: understands both text and images (screen and webcam)
- Privacy-first defaults: secrets and tokens are git-ignored

---

## Full Feature Set
- Voice Interaction
  - Speech-to-Text via a lightweight web recognizer (automated with Selenium/Chrome)
  - Robust handling of pauses and silence, simple language selection (default en-US)
- Natural Voice Output
  - Edge TTS (en-US-JennyNeural) with offline audio playback using Pygame
  - Automatic MP3 cleanup after playback
- Describe What’s Around You
  - Webcam capture with OpenCV → short, focused descriptions from Gemini
- Describe What’s On Your Screen
  - Full-screen capture with mss → concise screen summaries from Gemini
- Gmail Integration
  - Read latest emails (sender + subject)
  - Send emails to known contacts via Gmail API (OAuth flow handled)
- WhatsApp Support
  - Send messages instantly to known contacts (pywhatkit)
  - Initiate voice/video calls via UI automation (pyautogui)
- Web Search
  - Google search with top results summarized (title, snippet, URL)
- Conversation Memory
  - Persistent conversation_log.txt with automatic summarization when large
- Safety & Confirmation
  - Sensitive actions can be gated behind explicit confirmation
- Configurable
  - .env for secrets, contact maps in code, adjustable limits and timeouts

---

## Tech Stack
- Python, Selenium (Chrome), OpenCV, mss, Pillow
- Google Gemini (google-generativeai / google-genai)
- Edge TTS + Pygame
- Gmail API (google-api-python-client + auth libs)
- pywhatkit, pyautogui, googlesearch-python

---

## Requirements
- OS: Windows 10/11 strongly recommended (Edge TTS, Windows key automation)
- Software: Google Chrome, Microsoft Edge, WhatsApp Desktop
- Hardware: Microphone and webcam
- Accounts/Keys: Google Gemini API key; Google Cloud project with Gmail API enabled

---

## Setup

### 1) Get the code
- Clone or download this repository.

### 2) Install dependencies
You can install system-wide OR use a virtual environment (optional). Both are shown below.

- Option A: System-wide install (quick)
  - pip install --upgrade pip
  - pip install -r requirements.txt

- Option B: Virtual environment (optional but clean)
  - python -m venv .venv
  - .venv\Scripts\activate
  - pip install --upgrade pip
  - pip install -r requirements.txt

### 3) Environment variables
Create a file named .env in the project root:
- GOOGLE_API_KEY=your_gemini_api_key

### 4) Gmail API (optional, for email features)
1. In Google Cloud Console, enable the Gmail API.
2. Create OAuth 2.0 Desktop Client credentials and download credentials.json.
3. Place credentials.json in the project root. On first run, a browser will prompt for consent and token.json will be created automatically.
Note: credentials.json and token.json are already git-ignored.

---

## Run
- Ensure .env is configured
- Launch the app:
  - python main.py

If Selenium uses a headless Chrome, ensure Chrome is installed. WhatsApp automations open the desktop app; keep the machine unlocked.

---

## Usage Examples
- “What’s on my screen?” → Drishti captures the display and describes key elements
- “What’s in front of me?” → Drishti uses the webcam to describe surroundings
- “Send a WhatsApp to Papa: I reached safely” → Sends a message to a mapped contact
- “Call Mom on WhatsApp, voice” → Initiates a WhatsApp voice call via UI automation
- “Read my latest emails” → Summarizes recent inbox subjects
- “Email Papa about my schedule for tomorrow” → Sends an email with inferred subject/body
- “Search for best screen readers for Windows” → Returns a concise set of results

---

## How It Works (High-Level)
1. Listens for user input (currently via terminal input; Selenium web STT included and ready)
2. Decides whether to answer directly or invoke tools (vision, email, search, etc.)
3. Uses Gemini to summarize tool outputs and respond
4. Speaks the result back using Edge TTS
5. Logs the conversation and auto-summarizes when large

---


## Troubleshooting
- Chrome/Driver: Ensure Google Chrome is installed; webdriver-manager will fetch the driver.
- Edge TTS voice: Requires Microsoft Edge installed; network connectivity may be needed for voices.
- WhatsApp UI automation: Coordinates may need calibration per display. Ensure WhatsApp Desktop is openable and you are logged in.
- Gmail OAuth: If auth fails, delete token.json and retry, or recheck credentials.json.
- Webcam/Screen capture: Close apps using the camera; allow permissions.

---

## License
MIT (or update as per your team’s preference)

## Attribution
Built for HackOdisha 5.0 as an assistive technology prototype to enhance digital accessibility for blind and visually impaired users.