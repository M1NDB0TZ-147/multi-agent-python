<a href="https://livekit.io/">
  <img src="./.github/assets/livekit-mark.png" alt="LiveKit logo" width="100" height="100">
</a>

# Neon: Rave Companion & Harm Reduction Bot 🎉✨

<p>
  <a href="https://cloud.livekit.io/projects/p_/sandbox"><strong>Deploy a sandbox app</strong></a>
  •
  <a href="https://docs.livekit.io/agents/overview/">LiveKit Agents Docs</a>
  •
  <a href="https://livekit.io/cloud">LiveKit Cloud</a>
  •
  <a href="https://blog.livekit.io/">Blog</a>
</p>

## Meet **Neon**, your PLUR‑loving rave companion 🦄: a multi‑agent bot that keeps the party safe and fun!
Neon pairs state‑of‑the‑art AI (STT, LLM, TTS) with LiveKit’s real‑time platform to:
- 💦 Remind you to hydrate and check on friends
- 💊 Offer uncensored harm‑reduction guidance
- 🎵 Share DJ mixing tips & production tricks
- 🌐 Spill underground culture & PLUR etiquette

## Dev Setup

Clone the repository and install dependencies to a virtual environment:

```console
cd multi-agent-python
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Set up the environment by copying `.env.example` to `.env.local` and filling in the required values:

- `LIVEKIT_URL`
- `LIVEKIT_API_KEY`
- `LIVEKIT_API_SECRET`
- `OPENAI_API_KEY`
- `DEEPGRAM_API_KEY`

You can also do this automatically using the LiveKit CLI:

```bash
lk app env
```

### 🚀 Run Neon

```console
python3 main.py dev
```

Or run `python3 main.py --help` to explore more options.

This agent requires a frontend application to communicate with. You can use one of our example frontends in [livekit-examples](https://github.com/livekit-examples/), create your own following one of our [client quickstarts](https://docs.livekit.io/realtime/quickstarts/), or test instantly against one of our hosted [Sandbox](https://cloud.livekit.io/projects/p_/sandbox) frontends.
