# Audio Logo Toolkit

This folder holds everything tied to the World of Tethys audio logo so it stays synced with the website intro animation.

## Files

| File | Purpose |
| --- | --- |
| `wot-audio-logo-template.rpp` | Reaper session pre-loaded with four tracks (impact/sub, riser, ambient texture, vocal tag) plus timing markers so you can drop in assets and export a master under 3 seconds. |

## Workflow

1. Drop your assets into the corresponding tracks in the Reaper template.
2. Print the master to `renders/wot-audio-logo.wav` (48k/24-bit).
3. Convert/trim a `public/audio/wot-logo.mp3` (0.8–1.5 MB) — the website intro animation auto-loads this exact file name.
4. Keep a short `README` note with any loudness tweaks so future versions match.

## Getty Sounds Shortlist

I can’t hit Getty’s API from this offline environment, so I can’t add the official asset IDs for you right now. The template is labeled with the four layers you need; once you log into Getty Images | Sound, grab the IDs that fit these categories and drop them in here for the team:

| Layer | Target vibe | Getty metadata to capture |
| --- | --- | --- |
| Impact/Sub | Deep tectonic hit + sub tail (~0.6s) | ID, title, length, licensing tier |
| Riser/Energy | Granular reverse swell that peaks around marker “Riser Crest” | ID, title, BPM |
| Texture/Field | Volcanic steam, ocean spray, or electro-organic beds | ID, title, loop/single-shot note |
| Vocal Tag/Whisper | Breath or whisper that can be time-stretched to ~0.7s | ID, performer credit |

> Once you have the IDs, update this table so the design + audio teams pull the same cues. Example entry format: `ID 131234567 – “Cinematic Sub Impact Boom” (Getty Creative / SFX Premium)`.

## Web Hook

- The intro animation now looks for `public/audio/wot-logo.mp3`.
- The overlay plays once per session and respects `prefers-reduced-motion`.
- If you rename the file or change folders, update the path in `index.html`.

Drop any exported MP3/WAV assets inside `public/audio/` so Netlify or any static host picks them up automatically.

## ACX QC Snapshot

Use this table when you prep final assets for ACX so every render clears their gate before you upload. The “Requirement” column mirrors the official ACX spec, and the “Measurement” column is where you drop your latest QC readouts (values below are placeholders pulled from the screenshot you shared).

| Check | Requirement | Measurement | Status/Notes |
| --- | --- | --- | --- |
| Peak amplitude | ≤ -3 dBFS | — | Run `JS: Loudness Meter` (Reaper) or `Youlean` and confirm peaks hit between -3 and -6 dBFS. |
| RMS integrated | Between -23 and -18 dBFS | — | Bounce a full mix pass and note the integrated LUFS/LKFS value; adjust limiter threshold as needed. |
| Noise floor | ≤ -60 dBFS | **-41.2 dBFS** | Needs more cleanup — print longer room tone, notch hums, and add gentle broadband NR to push the floor below -60 dBFS. |
| Sample rate | 44.1 kHz WAV master → 44.1 kHz MP3 | 48 kHz session (OK) | Render masters at 44.1 kHz when you make the ACX upload, or dither/downsample during export. |
| MP3 encoding | Constant bit rate ≥ 192 kbps, joint stereo | **128 kbps** | Re-export at 192 kbps CBR (ACX standard) once the loudness issues are fixed. |
| Head/tail room tone | ≥0.5 s lead-in, ≥1 s tail | — | Confirm each deliverable includes printed room tone per ACX spec. |

Update the “Measurement” column each time you run QC so whoever exports next instantly sees what still needs attention.
