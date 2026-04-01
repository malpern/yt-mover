# yt-mover

A macOS app for migrating your YouTube Watch Later playlist into organized playlists. Built with SwiftUI.

## What it does

YouTube's Watch Later playlist has a 5,000 video limit and no built-in way to bulk-move videos. This app automates the process:

1. **Scan** your Watch Later playlist
2. **Copy** videos to a target playlist (e.g., "Old Watch")
3. **Delete** copied videos from Watch Later
4. **Clean up** unavailable (private/deleted) video placeholders

All operations happen in chunks of 50 with automatic pacing to avoid YouTube rate limits. If the session is interrupted, it resumes exactly where it left off.

## Features

- Resume detection — interrupted transfers persist across app restarts
- Live progress with copy/move phase tracking
- Cooldown and throttle feedback in the UI
- Inventory scanning with live video count
- Chrome Canary integration via CDP

## Requirements

- macOS 14+
- [yt-cli](https://github.com/malpern/yt-cli) installed in a sibling directory
- Google Chrome or Chrome Canary with remote debugging enabled

## Build

```bash
swift build
```

Or use the bundled app:
```bash
open "You Watch Later.app"
```

## Architecture

The app is a SwiftUI frontend that invokes `yt-cli` as a child process, streaming JSON progress events from stdout. All browser automation happens in the CLI — the app handles UI, state persistence, and user interaction.

## Related

- [yt-cli](https://github.com/malpern/yt-cli) — The TypeScript CLI engine this app depends on
- [be-kind-rewind](https://github.com/malpern/be-kind-rewind) — Video library organizer

## License

MIT
