# ac-releases

Model bundles the ac app loads, published as release assets. The app never downloads from here:
the build machine's `scripts/speech-bundles fetch` does, and refuses any archive or file whose
SHA-256 differs from `dist/speech-catalog.json`, which pins each bundle by tag, commit and hash.

Each bundle's licence and use restrictions are in `cards/`, read at the pinned commit.

| release | bundles | card |
|---|---|---|
| `live-voice-v1` | `live-voice-shared/coreml` — ContentVec + RMVPE for live voice conversion | [cards/live-voice-shared.md](cards/live-voice-shared.md) |
| `live-voice-v1` | `live-voice-m1/coreml` — voice M1 (RVC v2 48 kHz generator + retrieval index) | [cards/live-voice-m1.md](cards/live-voice-m1.md) |
