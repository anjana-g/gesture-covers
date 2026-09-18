# gesture-covers

A collection of browser-based, camera-driven instruments — one per song cover.
Left hand controls chords, right hand controls the bassline, both driven by hand-tracking
via the webcam. See each song folder's own notes below for what's specific to it.

## Structure

```
gesture-covers/
  vendor/              <- shared libraries (MediaPipe Hands + Tone.js), used by every song
  tere-paas-mein/       <- one song = one folder = one index.html
  _template/            <- starter copy for the next song
  ...
```

## Adding a new song

1. Copy `_template/` to a new folder named after the song (e.g. `nee-paartha-paarvai/`)
2. Open its `index.html` and edit:
   - the `<title>` and the `TERE PAAS HOON MAIN`-style heading near the top of the page
   - the default chord progression (`progInput` value) and bass notes (`bassInput` value)
3. Run it (see below) and tweak instrument/tone choices per song from the on-screen panels —
   no need to touch the code for that part.

Every song folder references the **same** `../vendor/` — don't duplicate those files per song.

## Running any song

From inside that song's folder:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000/` and click **"enable camera & start."**

## How each instrument works

- **Left hand** — finger count (1–5) selects a chord from the editable progression
- **Right hand** — finger count (1–5) selects a bass note from the editable list
- Fist on either hand = mute
- Per-hand instrument type (Basic/AM/FM/Mono, plus Pluck/Membrane for bass), waveform, and
  volume are all adjustable live from the on-screen panels
- Optional **MIDI output** to Logic Pro / GarageBand via Web MIDI (chords → channel 1, bass →
  channel 2) so you can play real instrument patches instead of the built-in synths — see each
  song's on-screen MIDI panel; one-time Mac setup is enabling the IAC Driver in Audio MIDI Setup

## Browser support

Camera + Web Audio: any modern browser.
MIDI out: Chrome/Edge only.
