---
title: "AirChirp"
slug: "Acoustic Data Transfer"
client: "Acoustic Data Transfer"
category: "Project"
services: "Data Transfer via Audio"
year: "2026"
featuredImage: "./images/cloudsync-suite/1.jpg"
imageTwo: "./images/cloudsync-suite/whatsup.jpeg"
imageThree: "./images/cloudsync-suite/wow.jpeg"
liveSite: "https://github.com/metrobraj/acoustic-data-transmission-devjams26"
description: "An experimental, Web Audio API and WebAssembly-powered acoustic modem designed to transfer encrypted binary payloads across air-gapped devices using sound waves."
isFeatured: true
isDraft: false
---


AirChirp was created during the Google Developer Groups DevJams'26 hackathon at VIT Vellore to bridge isolated devices without Wi-Fi, Bluetooth, or physical cables. The goal was to convert binary files into structured sound streams and decode them cleanly across high-reverberation room environments.

This program follows Goertzel Algorithm. Rather than running complete Fast Fourier Transforms (FFT) across unnecessary frequency bands which introduced latency and byte mismatches, the core receiver pipeline was refactored around the Goertzel Algorithm.

Targeted Detection: Evaluates discrete target frequencies (e.g., 8 kHz – 12.5 kHz DTMF lanes) with lower computational overhead than an 
O(N log N) FFT.
Phase/Magnitude Extraction: Allowed per-sample energy extraction for precise tone-pair detection directly out of PCM buffers.

To eliminate the "phantom zero-bit" problem (where silence is confused for a zero byte), a 4-lane parallel frequency mapper was built using Dual-Tone Multi-Frequency (DTMF) pairs across the 8 kHz – 12.5 kHz band(subject to change).

To counter reverberation time (RT60) and noise, 3 guardrails were implemented:

Preamble Lock: Detects a start marker tone.
Echo Clearance: Forces a silent drain window to allow hall reflections to dissipate.
Pilot Sync: Aligns the sample clock to middle-of-symbol timing windows.

Frontend & User Interface
HTML5 / CSS3: Glass-morphed UI design.
Vanilla JavaScript (ES6+): Pure browser execution without framework dependencies.
Digital Signal Processing (DSP) & Audio
Web Audio API: Hardware-level audio routing, raw PCM buffer capture, AudioContext creation, and OscillatorNode synthesis.
Goertzel Algorithm: Single-tone frequency analysis for low-overhead, targeted magnitude extraction across discrete audio lanes.
WebAssembly (WASM): C++ compiled audio processing integration using ggwave bindings for high-speed PCM encoding/decoding(Indeterminate).
Data & Payload Compression
fflate: Real-time DEFLATE/INFLATE compression and decompression pipeline to minimize byte payload size before transmission.
TypedArrays: Native Uint8Array and Int8Array memory buffers for fast binary-to-nibble bitwise operations.
