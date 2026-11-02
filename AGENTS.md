# Codex guide

This repository contains a portable Windows transcription app.

Keep the application portable, with no installer or backend. Store transcripts locally and do not commit user data or API keys. Use the OpenAI transcription API and bundled FFmpeg. Run TypeScript checks and a Windows build before declaring a release ready.

The user selected convenience mode: API keys are saved automatically as plaintext in AppData/credentials.json. Keep them out of GitHub and family distribution folders. electron-builder portable builds must use PORTABLE_EXECUTABLE_DIR for persistent data, not the temporary process.execPath. GitHub Actions produces the downloadable PortableApp-Windows artifact; do not claim the repo itself includes a built EXE. Review docs/ARCHITECTURE.md.
