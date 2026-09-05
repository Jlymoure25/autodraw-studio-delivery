# Music subsystem (deterministic)

This document describes the deterministic audio pipeline used by AutoDraw Studio. No ML/AI is used.

Overview
- Input: MIDI file (user-uploaded or generated from UI/text commands) + soundfont (SF2) + preset mapping
- Output: Rendered WAV (or MP3) produced deterministically using a software synth (fluidsynth) and deterministic FX chain

Components
- midi_mappings.json: maps preset names and text-commands to instrument program numbers, sample sets, and FX chains.
- audio_worker: a Dockerized worker that reads jobs from Redis `audio_jobs`, renders via fluidsynth (or sample concatenation), applies deterministic FX (ffmpeg), and uploads output to storage.

Presets
- ambient-pad
- lo-fi-beats
- piano-ballad
- string-ensemble

Deterministic rules
- Given the same MIDI, soundfont, and preset, the render output is byte-for-byte identical (fluidsynth + fixed rendering parameters). Randomness is disabled.
- FX are applied with fixed parameters recorded in the job params; these are saved in the audit entry.

Sample workflow
1. User selects "Create audio" -> picks preset or uploads MIDI.
2. User confirms any sample licenses.
3. Backend enqueues job to Redis with job_id, midi_path, preset, soundfont.
4. audio_worker renders using fluidsynth -> outputs /storage/{job_id}.wav and POSTs completion to backend.

Notes
- For high-quality commercial use, include a licensed SF2 in the project and record its license in the audit entry.
- If a user provides a MIDI that references third-party content, the system blocks export until rights are confirmed.
