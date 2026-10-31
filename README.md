---
title: Talk to LFM3-Omni — a full voice agent in your browser
emoji: 🎙️
colorFrom: indigo
colorTo: purple
sdk: static
app_file: index.html
pinned: false
short_description: Hands-free voice agent on LFM3-Omni-2B, all in-browser
models:
- LiquidAI/LFM3-Omni-2B-ONNX
---

# LFM3 Omni Voice Agent

**▶ Try it live:** https://iamdgarcia-lfm3-omni-voice-agent.static.hf.space

**What you'll learn here:** a 2-billion-parameter speech-to-speech omni model runs
entirely inside your browser tab. Your mic audio goes in, a synthesized voice comes
out, and nothing is sent to any server. Each turn card shows the measured latency
chain: end-of-speech detection, time to the model's first word, and time to its
first voice sample. That chain is where a voice agent lives or dies.

**What to do:** click **Load model** (one-time, ~2.4 GB of weights, cached by the
browser), then just talk. Hands-free mode is on by default: Silero VAD decides when
you finished speaking, the model answers out loud, and you can interrupt it by
talking over it (barge-in). Use headphones to avoid echo false-triggers. The
walkie-talkie button still works if you prefer push-to-talk.

## What this adds over the upstream demo

The reference demo (LiquidAI's WebGPU space) is a model demo: push-to-talk, no
VAD, no barge-in while the assistant speaks. This Space adds the agent loop:

- **Hands-free turn-taking** with Silero VAD (onnx-community/silero-vad via
  transformers.js), threshold + min-speech + hangover FSM.
- **Barge-in**: speak while the assistant is talking and it stops and listens.
- **Latency instrument per turn**: end-of-speech delay, first word, first voice,
  measured with `performance.now()` in the same tab that renders the audio.

## Attribution & licenses

- Model + ONNX weights: [LiquidAI/LFM3-Omni-2B-ONNX](https://huggingface.co/LiquidAI/LFM3-Omni-2B-ONNX),
  LiquidAI `lfm1.0` license. The `Lfm3OmniForConditionalGeneration.js` class is
  LiquidAI's, copied unmodified from their WebGPU demo Space.
- Silero VAD: [onnx-community/silero-vad](https://huggingface.co/onnx-community/silero-vad), MIT.
- Voice-agent loop, barge-in and latency instrumentation: [iamdgarcia](https://github.com/iamdgarcia).

Related research: trace2trajectory / trace2grammar (turn-level trajectory evaluation)
— the latency chain and the barge-in traces feed that line.
