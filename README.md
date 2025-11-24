# 🎙️ Speechmatics LiveKit Agent

A simple **LiveKit** AI voice agent using **Speechmatics** for STT (Speech-to-Text) and TTS (Text-to-Speech).

---

## ⚡ Getting Up and Running

### 1. Install `uv`

We use **uv** for fast and reliable package management. Follow the installation guide [here](https://docs.astral.sh/uv/getting-started/installation/).

You can verify your installation by running:
```bash
uv --version
```

### 2. Install LiveKit CLI

We will be using the LiveKit command line interface to quickly get up and running.

<details>
<summary><b>🍎 macOS </b></summary>

```bash
curl -sSL [https://get.livekit.io/cli](https://get.livekit.io/cli) | bash
```
</details>

<details>
<summary><b>🐧 Linux</b></summary>

```bash
brew install livekit-cli
```
</details>

<details>
<summary><b>🪟 Windows</b></summary>

```powershell
winget install LiveKit.LiveKitCLI
```
</details>


### 3. Link your LiveKit Cloud project to the CLI

*(If running in console you can skip this step)*

```bash
lk cloud auth
```

This will open a browser window allowing you to sign in or sign up to **LiveKit Cloud** and allowing your browser to connect to the agent we will create.

### 4. Initialise a project

```bash
uv init livekit-voice-agent --bare
cd livekit-voice-agent
```

### 5. Install packages

```bash
uv add \
  "livekit-agents[silero,turn-detector]~=1.2" \
  "livekit-plugins-noise-cancellation~=0.2" \
  "livekit-plugins-speechmatics" \
  "python-dotenv"
```

### 6. Get your API keys

Generate your local environment file:
```bash
lk app env -w
```
This will create a `.env.local` file using the API keys and URLs linked to your LiveKit cloud account.

To this file, we will now add API keys for Speechmatics and OpenAI.

> **Note:** Go to the [Speechmatics website](https://docs.speechmatics.com) to sign up and get an API key.

Add these lines to your `.env.local` file:

```env
SPEECHMATICS_API_KEY="<Your Speechmatics Key>"
OPENAI_API_KEY="<Your OpenAI Key>"
```

### 7. Create `speechmatics_agent.py`

Download, clone, or copy and paste the Python code into a file named `speechmatics_agent.py` in your project directory.

### 8. Download model files

Run the command to download models for voice activity detection and turn detection:
```bash
uv run speechmatics_agent.py download-files
```

### 9. Try your agent

**Option A: Run in command line**
```bash
uv run speechmatics_agent.py console
```

**Option B: LiveKit Playground (UI)**
For a friendlier UI, connect it to the [LiveKit Playground](https://docs.livekit.io/agents/start/playground/):
```bash
uv run speechmatics_agent.py dev
```