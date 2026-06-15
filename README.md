# The DOM-Scraper — Guide

A browser-based **drone & granular synthesis instrument** that turns the structure of a webpage (or any source file) into an evolving soundscape. It reads code top-to-bottom and translates colors, text, nesting, and punctuation into a sustained chord bed, a shimmering grain cloud, and soft noise swells. Everything runs client-side with the Web Audio API — no backend, no plugins.

---

## The core idea

A "scrubber" walks through the parsed source one cell at a time. Each cell's features steer the sound:

- **Color → harmony.** The running color of the page is snapped to a musical scale and held as a sustained chord. When the color drifts far enough, the instrument *crossfades* to a new chord. It never slides pitch — that's what keeps it a drone and not a siren.
- **Text → texture.** Text density drives a cloud of tiny windowed grains, pitched to the current chord tones and scattered across the stereo field.
- **Structure → space.** DOM nesting (or code indentation) controls reverb depth and, optionally, harmonic complexity.
- **Punctuation, `=` signs, digits, exact hex values, whitespace → micro-detail.** Dozens of tiny modulations add the codebase's "fingerprint," all governed by one **Detail** knob.

Signal flow: `sources → master filter → subsonic highpass → (dry + reverb + delay) → brick-wall limiter → output`. A meter (top-right of the visualizer) shows the post-limiter level.

---

## Quick start

1. **Open it.** A dense newsfeed page is pre-loaded. Press **▶ Listen** (or the **spacebar**).
2. **Try an Atmosphere.** Tap *Cathedral*, *Glass*, *Tape ruins*, *Tectonic*, or *Spectral* — each recalls a full setting.
3. **Feed it your own.** Paste HTML/CSS, or switch the dropdown to **Raw code** and paste any source file (JS, CSS, Python…) — or hit the **⌨ Code sample** chip.

Spacebar toggles play/stop anytime you're not typing in the source box.

---

## Two input modes

- **DOM mode** — walks the HTML element tree. "Nodes" = the number of actual tags. Long CSS/JS pasted here barely moves the node count, because only tags become nodes.
- **Raw code mode** — tokenizes **by line**, so a 500-line file makes ~500 cells regardless of tags. Indentation and bracket nesting become depth; a line's syntactic role becomes its pitch (declarations sit in a blue/low region, control-flow in amber, comments calm and green, everything else a stable hash-hue); blank lines are quiet rests.

---

## What each control does

**Transport & safety**
- *Scrape speed* — how fast the playhead reads through the source.
- *Grain density* — overall thickness of the grain cloud.
- *Filter (LP cutoff)* — global low-pass to tame brightness.
- *Master vol* — output level.

**Sanity ⟷ Chaos**
- *Guardrails* — at low values it clamps the filter and tightens everything; high opens it up and widens the scatter.

**Drone & harmony**
- *Voicing* — Open fifths (spacious), Stacked thirds (lush), Quartal (suspended), Cluster (dissonant), Overtone (spectral/microtonal).
- *Scale / mode* — pentatonic, the church modes, harmonic minor, whole-tone, two Japanese scales, or raw chromatic.
- *Voices* — how many tones in the chord (2–7).
- *Octave spread* — how far the chord fans across registers.
- *Drift · beating* — per-voice detune movement; the "living" shimmer of the drone.
- *Bed ⟷ Cloud* — balance between the sustained chord and the grain cloud.
- *Root pedal* — a constant tonic anchor underneath everything (tanpura-style).
- *Depth → complexity* — when on, deeper nesting adds voices and spread.

**Space & timbre**
- *Tonic / key* and *Register* — the root note and its octave.
- *Shimmer* — octave-up grains fed into the reverb tail (ambient glow).
- *Air · wind* — a constant filtered-noise bed.
- *Wash · swells* — the noise swells triggered by containers/images.
- *Space · reverb* — reverb and delay depth.
- *Stereo width* — how wide the chord spreads.
- *Detail · code micro-mods* — master amount for all the fine code-feature modulations.

**Temporal matrix** (decoupled smoothing)
- *Harmonic inertia* — how slowly chords crossfade.
- *Granular blur* — how gradually the cloud responds to text changes.
- *Transient bleed* — how long the swells sustain and overlap.

---

## How source features map to sound

| Source feature | What it controls |
|---|---|
| Hex hue | Pitch (scale degree) |
| Hex lightness / saturation | Register / brightness |
| Exact hex low-bits | Micro-detune signature |
| Text or line length | Grain density & size |
| DOM depth / code nesting | Reverb space (+ optional complexity) |
| Containers / block-opening lines | Noise-swell triggers |
| Images / string lines | Noise bursts |
| `=` density | Width of the drone's beating |
| Punctuation density | Grain grit |
| Digit density | Octave-up sparkle |
| Whitespace ratio | Spacing between grains |

---

## Tips & recipes

- **Make it a pure drone (no "ocean" whoosh):** set *Air* and *Wash* to 0 — you're left with just the tonal chord and grain cloud.
- **Dial the codebase fingerprint in or out:** *Detail* at 0 gives clean intervals; push it up to layer in the punctuation/hex/whitespace character.
- **Vast and slow:** high *Harmonic inertia*, *Space* ~80%, *Root pedal* on, slow *Scrape speed*.
- **Uneasy and tectonic:** *Cluster* voicing + *Whole tone* scale + high *Drift* + low *Register*.
- **Hear architecture:** turn on *Depth → complexity*, switch to Raw code, and scrub a deeply-nested source file — the nested sections audibly thicken.

---

## Notes & limits

- **No live URLs.** Scraping a remote site requires a backend proxy to clear browser CORS rules, which isn't available in this standalone file — so it works on pasted HTML/CSS or source code.
- **All client-side**, built on the Web Audio API: scheduled Hann-windowed grains, sustained oscillator voices, a convolution reverb, a feedback delay, and a `DynamicsCompressor` acting as a brick-wall limiter so dense pages can't clip.
- Best in a current desktop browser (Chrome/Edge/Safari/Firefox) with sound on.
