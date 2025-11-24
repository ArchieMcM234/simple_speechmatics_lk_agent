

# Speechmatics LiveKit Agent

A simple **LiveKit** AI voice agent using **Speechmatics** for STT and TTS.

## Getting up and running

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
curl -sSL https://get.livekit.io/cli | bash
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

(If running in console you can skip)

```bash
lk cloud auth
```

This will open a browser window allowing you to sign in or sign up to **LiveKit Cloud** and allowing your browser to connect to the agent we will create.





### 4. Intitialise a project

```bash
uv init livekit-voice-agent --bare
cd livekit-voice-agent
```

### 5. Install packages

```bash
uv add \
  "livekit-agents[silero,turn-detector]~=1.2" \
  "livekit-plugins-noise-cancellation~=0.2" \
  "livekit-plugins-speechmatics"
  "python-dotenv"
```


### 6. Get your API keys

```bash
lk app env -w
```
This will create a .env.local file using the api keys and urls linked to your LiveKit cloud account.

To this file we will now add api keys for Speechmatics and OpenAI.

Go to the [Speechmatics website](https://docs.speechmatics.com) and signup and get an api key.

Add these lines to your .env.local file.

```
OPENAI_API_KEY = "<Your API Key>"
SPEECHMATICS_API_KEY="<Your API Key>"
```


### 7. Create speechmatics_agent.py

Download, clone, or copy and paste the python code in speechmatics_agent.py into a python file in your project.

### 8. Download model files
Run the command:
```
uv run agent.py download-files
```
This downloads the models for voice activity detection and turn detection.

### 9. Try your agent

You can now run your agent in the command line:
```
uv run speechmatics_agent.py console
```

Or for a freindlier UI connect it to [LiveKit playground](https://docs.livekit.io/agents/start/playground/):
```
uv run agent.py dev
```


