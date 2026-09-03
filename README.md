# Web Audio Cutter

A lightweight, zero-dependency, client-side audio slicing tool running directly in the browser. 

Built entirely with modern Web Standards (HTML5, Vanilla JavaScript, and Web Audio API), it decodes, previews, and extracts specific time ranges from any browser-supported audio container without uploading a single byte to an external server.

---

## Features

- **100% Client-Side & Privacy-First:** All audio processing occurs in local browser memory via `AudioContext`. No backend, no data transmission, completely functional offline.
- **Zero Dependencies:** Pure Vanilla JS. No bloated third-party libraries, Node runtimes, or build steps required.
- **Precise Time Control:** Set start ($T_1$) and end ($T_2$) boundaries down to fractions of a second using an intuitive `HH : MM : SS.ss` input layout.
- **Real-Time Position Capture:** Sync playback positions directly into boundary inputs with a single click.
- **Instant Preview:** Audition selected segments on the fly before exporting.
- **Lossless PCM Export:** Encodes cut segments directly into valid 16-bit PCM `.wav` containers via low-level `ArrayBuffer` byte assembly.

---

## Technical Mechanism

1. **Decoding:** Uses `AudioContext.decodeAudioData()` to parse compressed or uncompressed audio files into raw PCM channels (`AudioBuffer`).
2. **Slicing:** Translates input timestamps ($T_1, T_2$) to discrete frame indices:
   $$\text{Offset} = \lfloor T \times \text{SampleRate} \rfloor$$
   Copies subarray channel slices into a newly instantiated target buffer.
3. **Container Assembly:** Dynamically writes the standard 44-byte canonical RIFF/WAVE header (specifying channel count, sampling rate, bit depth, and data block chunks) using `DataView`, quantizes 32-bit float samples to signed 16-bit linear PCM integers, and triggers browser downloads via Object URLs.

---

## Supported Input Formats

Supports any audio format natively decodable by your browser's underlying media engine:
- `.mp3`
- `.wav`
- `.m4a` / `.aac`
- `.ogg`
- `.flac`
- `.webm`

*Note: Export format is standardized to 16-bit PCM `.wav` for zero-dependency encoding stability.*

---

## Quick Start

### Local Usage
1. Clone the repository:
   ```bash
   git clone [https://github.com/](https://github.com/)<your-username>/web-audio-cutter.git
