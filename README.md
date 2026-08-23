# Known AI Artists Database

Curated, community-maintained database of artists/projects known to produce AI-generated music. Used by [ai-music-checker](https://github.com/holgerkampffmeyer2/ai-music-checker) for forensic detection.

## Data

- **File**: `known_ai_artists.json`
- **Schema**: `schema.json` (validated on every PR)
- **License**: CC0-1.0 (public domain dedication)

## Entry Format

```json
{
  "id": "clmx",
  "name": "CLMX",
  "aliases": ["Cli-Max", "@clmxmusic"],
  "type": "artist",
  "labels": ["Balearic Vibes Records"],
  "ai_confidence": "high",
  "evidence": [
    {
      "url": "https://pro.music-worx.com/release/freedom-balearic-vibes",
      "note": "Music Worx editorial: 'Likely AI-assisted based on label-level evaluation and release patterns'",
      "date": "2026-07"
    }
  ],
  "added": "2026-08-22",
  "verified": "2026-08-22"
}
```

### Fields

| Field | Description |
|-------|-------------|
| `id` | Unique kebab-case identifier |
| `name` | Primary artist/project name |
| `aliases` | Alternative names, handles, spellings |
| `type` | `artist` \| `project` \| `collective` |
| `labels` | Associated record labels |
| `ai_confidence` | `high` \| `medium` \| `low` |
| `evidence` | Array of source URLs + notes + dates |
| `added` / `verified` | ISO dates (YYYY-MM-DD) |

## Contributing

### Option 1: Issue-based (Recommended)

1. Click **New Issue** → Select **"Add AI Artist Entry"**
2. Fill in all required fields (ID, Name, Type, AI Confidence, Evidence)
3. Submit Issue
4. Maintainer reviews and sets **Accept** label
5. GitHub Action automatically creates PR with your entry
6. Maintainer merges after validation passes

### Option 2: Fork and PR

1. Fork this repo
2. Add entry to `known_ai_artists.json` (keep alphabetical by `id`)
3. Ensure at least **one evidence URL** with note and date
4. Run validation locally: `python -m jsonschema -i known_ai_artists.json schema.json`
5. Submit PR

### PR Requirements

- Entry follows schema exactly
- Evidence from credible source (editorial, investigation, creator admission, platform marketing)
- No duplicate `id`
- Dates in ISO format (YYYY-MM-DD for added/verified, YYYY-MM for evidence)

## Usage

Default fetch URL for ai-music-checker:
```
https://raw.githubusercontent.com/holgerkampffmeyer2/ai-artists-db/main/known_ai_artists.json
```

Tool caches with 24h TTL, falls back to bundled copy offline.

## Current Entries

See `known_ai_artists.json` for full list. Includes:
- **CLMX** (Balearic Vibes) — Music Worx editorial "likely AI-assisted"
- **The Velvet Sundown** — The Verge investigation (2024)
- **Anna Indiana** — Creator-admitted fully AI singer
- **AIVA, Soundraw, Boomy, Mubert** — Platforms explicitly marketing AI generation