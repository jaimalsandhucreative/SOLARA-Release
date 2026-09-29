# SOLARA

**A futuristic desktop AI assistant.**

SOLARA is a premium AI desktop application that connects to OpenRouter, offering streaming conversations, web search, file attachments, persistent memory, and a carefully crafted aurora-inspired interface.

![SOLARA](https://img.shields.io/badge/SOLARA-0.2.0-7c5cff)

---

## Features

- **Streaming AI conversations** — Real-time token streaming with stop, regenerate, and edit support
- **Web search** — Live search through OpenRouter with real source citations
- **File attachments** — TXT, MD, JSON, CSV, PDF, DOCX, and code files with drag-and-drop
- **THINK mode** — Extra reasoning effort for complex questions
- **Persistent memory** — Local memory that survives restarts, with full editing controls
- **Chat management** — Rename, duplicate, delete, and search conversations
- **Secure API storage** — Windows Credential Manager integration (keyring)
- **Polished settings** — Model selection, themes, font size, UI scale, personality
- **Aurora interface** — Dark, atmospheric, glassmorphism design with purple/blue accents

---

## Downloading & Installing SOLARA (End Users)

**You do NOT need VS Code, a code editor, Node.js, Rust, or any development tools.** SOLARA comes as a standalone Windows installer.

### Step 1: Download

Download the latest `solara_0.2.0_x64-setup.exe` from the [Releases](https://github.com/yourusername/solara/releases) page (or from wherever the developer shared it with you).

### Step 2: Install

1. **Double-click** `solara_0.2.0_x64-setup.exe`
2. If Windows shows a "Windows protected your PC" warning, click **"More info"** → **"Run anyway"**
3. Follow the installer prompts (choose install location if asked)
4. Wait for installation to complete

### Step 3: Launch

- Open SOLARA from the **Start menu** or **Desktop shortcut**
- No command line, no terminal, no setup

### Step 4: Add Your OpenRouter API Key

1. On first launch, click **Settings** (gear icon in the sidebar)
2. Go to the **API** tab
3. Paste your OpenRouter API key
4. Click **"Save key"** — it is stored securely in Windows Credential Manager
5. Click **"Test connection"** to verify

### Step 5: Start Using SOLARA

- Type a message and press **Enter** to chat
- Click **New chat** to start a fresh conversation
- Use the **Search** toggle for live web search
- Use the **Think** toggle for extra reasoning effort
- Attach files with the **paperclip** button or drag-and-drop

### System Requirements

| Requirement | Minimum |
|-------------|---------|
| OS | Windows 10 (64-bit) or Windows 11 |
| RAM | 4 GB |
| Disk | ~50 MB free space |
| Internet | Required (for AI responses) |

### Troubleshooting

| Problem | Solution |
|---------|----------|
| "Windows protected your PC" | Click "More info" → "Run anyway" |
| "Missing DLL" error | Install [WebView2 Runtime](https://developer.microsoft.com/microsoft-edge/webview2/) |
| App won't start | Try reinstalling, or run as administrator |
| API key not working | Verify key at [OpenRouter Keys](https://openrouter.ai/keys) |

---

## Installation (Developers)

### Prerequisites

- [Node.js](https://nodejs.org/) 18+
- [Rust](https://www.rust-lang.org/tools/install) (latest stable)
- [Tauri CLI](https://v2.tauri.app/start/prerequisites/)

### Setup

```bash
# Clone the repository
git clone <repository-url>
cd solara

# Install dependencies
npm install

# Copy environment template
cp .env.example .env
# Edit .env and add your OpenRouter API key

# Start development server
npm run tauri dev
```

---

## Configuration

### OpenRouter API Key

SOLARA requires an OpenRouter API key. You have two options:

**Option 1: Environment variable (development)**

Create a `.env` file in the project root:

```env
OPENROUTER_API_KEY=sk-or-v1-your-key-here
```

**Option 2: Windows Credential Manager (production)**

Use the Settings → API panel to save your key securely. The key is stored in the Windows Credential Manager and never exposed to the frontend.

### Model Configuration

SOLARA supports configurable OpenRouter models. The default is `openai/gpt-4o-mini`. Change it in Settings → AI.

Available models:
- GPT-4o mini (default)
- GPT-4o
- Claude 3.5 Sonnet
- Gemini 2.0 Flash
- Llama 3.3 70B
- DeepSeek Chat
- Custom model ID

---

## Development

```bash
# Start Tauri development server
npm run tauri dev

# Run frontend tests
npm test

# Run Rust tests
npm run test:rust

# Build for production
npm run tauri build
```

---

## Architecture

```
solara/
├── src/                    # TypeScript frontend
│   ├── main.ts             # Entry point
│   ├── styles.css          # Global styles
│   ├── types.ts            # Type definitions
│   ├── store.ts            # State management
│   ├── storage.ts          # Persistence layer
│   ├── markdown.ts         # Markdown rendering
│   ├── icons.ts            # SVG icon system
│   ├── files.ts            # File handling
│   ├── ai/
│   │   ├── provider.ts     # Tauri command wrapper
│   │   └── prompts.ts      # System prompt builder
│   ├── ui/
│   │   ├── helpers.ts      # Shared utilities
│   │   ├── sidebar.ts      # Chat list & menu
│   │   ├── messages.ts     # Message rendering
│   │   ├── composer.ts     # Input & send
│   │   └── settings.ts     # Settings modal
│   └── __tests__/          # Frontend tests
├── src-tauri/              # Rust backend
│   ├── src/
│   │   ├── main.rs         # Binary entry
│   │   ├── lib.rs          # Command registration
│   │   ├── openrouter.rs   # OpenRouter streaming
│   │   ├── credentials.rs  # API key management
│   │   ├── files.rs        # File extraction
│   │   ├── errors.rs       # Error mapping
│   │   └── persist.rs      # State persistence
│   ├── Cargo.toml
│   └── tauri.conf.json
└── index.html
```

---

## Building

### Development build

```bash
npm run tauri dev
```

### Production build

```bash
npm run tauri build
```

The installer will be generated in `src-tauri/target/release/bundle/`.

---

## Privacy & Security

- **API keys** are stored in Windows Credential Manager, never in frontend code
- **Conversations** are stored locally on your device
- **Memory** is stored locally and never transmitted except as part of the system prompt
- **No telemetry** — SOLARA does not collect usage data

### Safety

SOLARA is an AI assistant and can make mistakes. It is **not**:
- A doctor or medical device
- A replacement for professional judgment
- A source of authoritative information

**Do not enter:**
- Passwords or API secrets
- Identifiable patient information
- Confidential institutional data
- Private credentials

Search results are supplemental. THINK mode increases reasoning effort but does not guarantee correctness.

---

## License

MIT
