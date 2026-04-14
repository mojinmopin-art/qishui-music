# Qishui Music - 汽水音乐修复补丁

[![Official Site](https://img.shields.io/badge/Official_Site-qishui--app.org-brightgreen)](https://qishui-app.org)
[![Version](https://img.shields.io/badge/Version-2026.4-blue)]()

Compatibility patch for Qishui Music (汽水音乐) app. Fixes playback errors, resolves regional restrictions, and enhances audio quality parsing for overseas users.

## Known Issues & Fixes

### Playback Errors
| Error Code | Description | Status |
|-----------|-------------|--------|
| 403 | Access forbidden (regional restriction) | ✅ Fixed |
| 502 | Server gateway timeout during peak hours | ✅ Fixed |
| -1 | Audio stream decode failure | ✅ Fixed |
| 1001 | Login session expired loop | ✅ Fixed |

### Regional Playback Restrictions
Users outside mainland China often encounter "该歌曲暂不可播放" (This song is currently unavailable). This is caused by:
- **GeoIP-based content licensing** — music licenses are region-locked
- **CDN routing** — overseas requests route to nodes without cached content
- **API endpoint restrictions** — certain API calls check client IP against a whitelist

Our patch provides:
- Optimized CDN endpoint selection for overseas users
- Fallback audio stream sources
- Local cache for frequently played tracks

## Supported Platforms

| Platform | Version | Status |
|----------|---------|--------|
| Android | 8.0+ | ✅ Full support |
| iOS | 14+ | ✅ Full support |
| Windows | 10+ | ✅ Desktop client |
| macOS | 12+ | ⚠️ Via web player |
| Web Browser | Chrome 118+ | ✅ Web player |

## Installation

1. Visit [qishui-app.org](https://qishui-app.org) for environment detection
2. The diagnostic tool identifies your platform and network environment
3. Download the recommended patch version
4. Follow platform-specific installation guide

## Technical Details

### Audio Stream Architecture

```
User Request (play song)
    ↓
API: /music/play?id=xxx
    ↓
License Check (region + subscription)
    ↓
CDN Selection (nearest edge node)
    ↓
Audio Stream (HLS / DASH adaptive bitrate)
    ↓
Local Decoder (AAC / FLAC / MP3)
```

### Why Audio Quality Matters

Qishui Music supports multiple audio quality tiers:

| Quality | Bitrate | Format | File Size (3min) |
|---------|---------|--------|-----------------|
| Standard | 128 kbps | AAC | ~2.8 MB |
| High | 256 kbps | AAC | ~5.6 MB |
| Lossless | 900+ kbps | FLAC | ~20 MB |
| Hi-Res | 1400+ kbps | FLAC 24bit | ~32 MB |

The patch ensures overseas users can access High quality tier (normally restricted to Standard for non-CN IPs).

### Lyrics Support

This repository also maintains a lyrics database with LRC format files. Features:
- Time-synced lyrics (word-level for supported songs)
- Bilingual lyrics (Chinese + Romanized pinyin)
- LRC file download for offline players

Browse the lyrics collection at [qishui-app.org/lyrics/](https://qishui-app.org/lyrics/)

## Frequently Asked Questions

**Q: Is this safe to use?**
A: The patch only modifies CDN routing and audio stream endpoints. No personal data is collected or modified.

**Q: Will my playlists and favorites be affected?**
A: No. The patch does not touch user data. Your playlists, favorites, and listening history remain intact.

**Q: How often is the patch updated?**
A: We release updates whenever Qishui Music changes their API or CDN configuration. Check this repository or [qishui-app.org](https://qishui-app.org) for the latest version.

**Q: Can I request a specific song's lyrics?**
A: Yes! Open an [Issue](../../issues) with the song name and artist, and we'll add it to the lyrics database.

## Contributing

Bug reports, lyrics contributions, and pull requests are welcome.

---
*Downloads, lyrics database, and full documentation at [qishui-app.org](https://qishui-app.org)*
