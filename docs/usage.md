<!-- docs/usage.md -->

# Usage & Setup

> Quick reference for getting Neon up and running, and customizing it.

### 1. Prerequisites
- Python 3.8+
- A LiveKit deployment (Cloud or self-hosted)
- OpenAI & Deepgram API keys

### 2. Environment
> Copy and customize environment variables:
> ```bash
> cp .env.example .env.local
> ```
> Fill in:
> ```text
> LIVEKIT_URL=your_livekit_url
> LIVEKIT_API_KEY=your_key
> LIVEKIT_API_SECRET=your_secret
> OPENAI_API_KEY=your_openai_key
> DEEPGRAM_API_KEY=your_deepgram_key
> ```

### 3. Install Dependencies
> Create a virtual environment and install:
> ```bash
> python3 -m venv venv
> source venv/bin/activate
> pip install -r requirements.txt
> ```

### 4. Running Neon
> Launch the agent session:
> ```bash
> python3 main.py dev
> ```
> Options:
- `dev`: local mode
- `prod`: production mode (if configured)
- Run `python3 main.py --help` for full CLI usage.

### 5. Frontend Client
> Neon requires a real-time frontend (e.g. web, CLI) to connect:
- Example web client: https://github.com/livekit-examples/js-sdk
- Quickstarts: https://docs.livekit.io/realtime/quickstarts/
- LiveKit Sandbox: https://cloud.livekit.io/projects/p_/sandbox

### 6. Customizing Agents
- Edit system prompts: see `docs/system-prompt.md` and `main.py` (`instructions=`).
- Add new agents: subclass `Agent`, implement `on_enter` and `@function_tool` methods.
- Adjust LLM/STT/TTS models in `entrypoint` setup:
> ```python
> session = AgentSession[NeonData](
>     llm=openai.LLM(model="gpt-4o-mini"),
>     stt=deepgram.STT(model="nova-3"),
>     tts=openai.TTS(voice="ash"),
>     ...
> )
> ```

### 7. Metrics & Scaling
- Usage metrics are logged via `metrics.UsageCollector()`.
- Extend prewarm functions for custom model loading (see `prewarm` in `main.py`).

### 8. Feedback & Contributions
- PRs and issues welcome!
- LiveKit Agents GitHub: https://github.com/livekit/agents
- LiveKit Core GitHub: https://github.com/livekit/livekit-server