# Architecture

`src/` is the React interface. `electron/main.ts` handles audio files, FFmpeg conversion, OpenAI requests, and transcript storage. `electron/preload.ts` exposes a restricted IPC bridge. Windows builds bundle FFmpeg and produce a portable EXE. On packaged builds `PORTABLE_EXECUTABLE_DIR` locates the actual portable executable directory so `AppData/` and `Transcriptions/` persist beside the EXE.

The user chose automatically remembered API keys. `AppData/credentials.json` stores the key in plaintext, without a password; protect that folder. Transcripts are text and metadata JSON in `Transcriptions/`. Never commit private data. The GitHub Actions artifact is a clean distribution, not a copy of anyone's personal data.

Build with `npm install`, `npm run check`, `npm run dist` on Windows with FFmpeg binaries in `vendor/ffmpeg/`. Verify the Windows build and run it before describing it as finished.
