# 🎤 Local Voice Agent for OpenClaw

**Complete offline voice-to-voice AI assistant (Whisper.cpp STT + Pocket-TTS)**

✅ 100% Local Processing | ✅ No Cloud APIs | ✅ No Costs | ✅ Custom Voice Cloning

---

## 🌟 Features

- ✅ **Voice Input** - Whisper.cpp speech-to-text (100+ languages)
- ✅ **Voice Output** - Pocket-TTS text-to-speech (custom voice cloning)
- ✅ **AI Processing** - OpenClaw integration for intelligent responses
- ✅ **Hands-Free** - Full voice conversation mode
- ✅ **Multi-Language** - English, Nepali, Hindi, and 97+ more
- ✅ **Custom Voices** - Use your own cloned voice

---

## 🏗️ Architecture

```
┌─────────────┐     ┌──────────────┐     ┌──────────┐     ┌─────────────┐
│ User Voice  │ ──→ │ Whisper STT  │ ──→ │ OpenClaw │ ──→ │ Pocket-TTS  │ ──→ │ Voice Response │
│ (Audio)     │     │ (Speech→Text)│     │   AI     │     │ (Text→Speech)│     │ (Audio)        │
└─────────────┘     └──────────────┘     └──────────┘     └─────────────┘
```

---

## 🚀 Quick Start

### 1. Install Dependencies

```bash
# Whisper.cpp (Speech-to-Text)
git clone https://github.com/ggerganov/whisper.cpp ~/.local/whisper.cpp
cd ~/.local/whisper.cpp
make -j4
bash ./models/download-ggml-model.sh tiny

# Pocket-TTS (Text-to-Speech) - See Pocket-TTS setup guide
export POCKET_TTS_URL="http://localhost:5000"

# FFmpeg (Audio Conversion)
sudo apt-get install -y ffmpeg
```

### 2. Install Skill

```bash
# Copy skill to OpenClaw skills directory
cp -r voice-agent ~/.openclaw/workspace/skills/

# Make scripts executable
chmod +x ~/.openclaw/workspace/skills/voice-agent/bin/*

# Add to PATH (optional)
export PATH="$HOME/.openclaw/workspace/skills/voice-agent/bin:$PATH"
```

### 3. Test It

```bash
# Basic voice command
voice-agent "What's the weather today?"

# Interactive conversation mode
voice-agent --interactive

# Process audio file
voice-agent --file recording.wav

# Text-only mode
voice-agent "Hello!" --no-voice
```

---

## 📖 Usage

### Voice Commands

```bash
# Ask a question
voice-agent "What time is it?"

# Get morning briefing
voice-agent "Give me my morning briefing"

# Set a reminder
voice-agent "Remind me to call Peter at 3 PM"

# Check system status
voice-agent "Is the TTS server running?"
```

### Interactive Mode

```bash
# Start conversation
voice-agent --interactive

# Example session:
# You: What's the weather?
# AI: The weather in Kathmandu is partly cloudy, 22 degrees.
# You: Thanks!
# AI: You're welcome! Anything else?
# You: quit
```

### Audio File Processing

```bash
# Transcribe voice note
voice-to-text voice-note.wav

# Transcribe video audio
voice-to-text meeting.mp4

# Transcribe OGG file
voice-to-text recording.ogg
```

### Generate Speech

```bash
# Basic TTS
text-to-voice "Hello world!"

# Custom voice
text-to-voice "Namaste!" greeting.wav "peter voice"

# Different output format
text-to-voice "Hello!" output.mp3
```

---

## ⚙️ Configuration

Edit `config/voices.yaml`:

```yaml
# Change STT model (tiny → small → medium)
stt:
  model: small  # Better accuracy, slower

# Change default TTS voice
tts:
  voice: voice 2  # Use female voice

# Change language
stt:
  language: ne  # Nepali
```

---

## 🔧 Troubleshooting

### "Whisper CLI not found"

```bash
# Install Whisper.cpp
git clone https://github.com/ggerganov/whisper.cpp ~/.local/whisper.cpp
cd ~/.local/whisper.cpp && make -j4
bash ./models/download-ggml-model.sh tiny
```

### "Cannot connect to TTS server"

```bash
# Start Pocket-TTS server
cd /path/to/pockettts
source venv/bin/activate
python3 -m app.main --host 0.0.0.0 --port 5000
```

### "ffmpeg required"

```bash
# Install ffmpeg
sudo apt-get install -y ffmpeg
```

### Slow Transcription

- Use `tiny` model instead of `small` or `medium`
- Reduce audio sample rate: `ffmpeg -i input.wav -ar 16000 output.wav`

---

## 📊 Performance

| Component | Model | RAM | Speed | Accuracy |
|-----------|-------|-----|-------|----------|
| **STT** | tiny | 500MB | 3x realtime | 90% |
| **STT** | small | 1GB | 1x realtime | 95% |
| **STT** | medium | 2GB | 0.5x realtime | 98% |
| **TTS** | Pocket-TTS | 200MB | Instant | High |

---

## 🎯 Use Cases

### 1. Daily Briefings

```bash
# Voice-activated morning briefing
voice-agent "Good morning! Give me my briefing"
```

### 2. Hands-Free Coding

```bash
# Check git status while coding
voice-agent "What's the git status?"
```

### 3. Accessibility

Perfect for users with mobility constraints or visual impairments.

### 4. Multilingual Support

```bash
# Nepali voice commands
voice-agent "मौसम कस्तो छ?"  # What's the weather?
```

### 5. Voice Notes

```bash
# Quick voice memos
voice-agent "Note: Call Peter about the project tomorrow"
```

---

## 📁 Project Structure

```
voice-agent/
├── SKILL.md              # OpenClaw skill definition
├── README.md             # This file
├── bin/
│   ├── voice-to-text     # STT script
│   ├── text-to-voice     # TTS script
│   └── voice-agent       # Main pipeline
├── lib/
│   ├── stt.py            # Python STT wrapper
│   └── tts.py            # Python TTS wrapper
├── config/
│   └── voices.yaml       # Configuration
└── examples/
    ├── morning-briefing.sh
    └── conversation-mode.sh
```

---

## 🤝 Contributing

1. Fork the repository
2. Create feature branch
3. Make changes
4. Submit pull request

---

## 📄 License

MIT License - See LICENSE file

---

## 🙏 Credits

- **Whisper.cpp** - [ggerganov/whisper.cpp](https://github.com/ggerganov/whisper.cpp)
- **Pocket-TTS** - [kyutai-labs/pocket-tts](https://github.com/kyutai-labs/pocket-tts)
- **OpenClaw** - [openclaw/openclaw](https://github.com/openclaw/openclaw)

---

## 💬 Support

- **GitHub Issues:** [Your Repo Link]
- **OpenClaw Discord:** https://discord.com/invite/clawd
- **Documentation:** [Your Docs Link]

---

**Built with ❤️ by Peter Karki & Pinobot**
