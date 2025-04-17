<!-- docs/project-context.md -->

# Project Context: Neon Rave Companion AI

> Copy-paste this document into an AI chat to restore full project context and continue development seamlessly.

## Overview
- **Project**: Neon – a multi-agent AI rave companion focused on harm reduction, music tips, and underground culture.
- **Tech Stack**: Python, LiveKit Agents framework, Deepgram STT, OpenAI LLM/TTS, Silero VAD.
- **Agents**:
  - `NeonLeadAgent`: greets users, routes to specialists based on intent.
  - `NeonHarmReductionAgent`: provides uncensored substance safety, hydration & friend-check reminders.
  - `NeonMusicAgent`: offers DJ mixing tips, production advice, gear recommendations.
  - `NeonCultureAgent`: shares underground event info, fashion trends, PLUR etiquette.

## Key Files
- `main.py`: defines data models (`NeonData`), agents, `prewarm`, and `entrypoint`; starts the AgentSession.
- `requirements.txt`: Python dependencies (livekit, openai, deepgram, silero, etc.).
- `.env.example`: template for environment variables.
- `docs/`: documentation folder with usage guides and system prompts.

## Data Model
```python
@dataclass
class NeonData:
    hydration_reminders: int = 0
    topics_discussed: list[str] = field(default_factory=list)
```

## Environment Variables
```text
LIVEKIT_URL=your_livekit_url
LIVEKIT_API_KEY=your_key
LIVEKIT_API_SECRET=your_secret
OPENAI_API_KEY=your_openai_key
DEEPGRAM_API_KEY=your_deepgram_key
```

## Entry Point & Session
```python
# prewarm: load VAD
proc.userdata['vad'] = silero.VAD.load()

# entrypoint:
await ctx.connect()
session = AgentSession[NeonData](
    vad=ctx.proc.userdata['vad'],
    llm=openai.LLM(model='gpt-4o-mini'),
    stt=deepgram.STT(model='nova-3'),
    tts=openai.TTS(voice='ash'),
    userdata=NeonData(),
)
await session.start(
    agent=NeonLeadAgent(),
    room=ctx.room,
    room_input_options=RoomInputOptions(),
    room_output_options=RoomOutputOptions(transcription_enabled=True),
)
```

## System Prompts Reference
See `docs/system-prompt.md` for the exact `instructions` strings for each agent.

## Usage
1. **Install** dependencies: `pip install -r requirements.txt`
2. **Configure**: copy `.env.example` → `.env.local` and fill values.
3. **Run**: `python3 main.py dev`
4. **Frontend**: connect via LiveKit JS SDK or examples at https://github.com/livekit-examples/js-sdk

## Frontend Integration Snippet (JS)
```javascript
import { connect, LocalAudioTrack } from 'livekit-client';

async function joinRoom(url, token) {
  const room = await connect(url, token, { audio: true, video: false });
  const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
  const tracks = stream.getAudioTracks().map(t => new LocalAudioTrack(t));
  await room.localParticipant.publishTracks(tracks);
}
```

## Logging & Metrics
- Metrics are collected via `metrics.UsageCollector()` and logged on shutdown.
- Transcriptions and events are enabled in `RoomOutputOptions`.

## Next Steps
- Extend or customize agents by editing prompts in `main.py`.
- Build or adapt a frontend client to capture user media and render Neon’s TTS audio.
- Add new agents or tools via the `@function_tool` decorator.

---
*End of project context.*