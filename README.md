# PortableScribe
A local-first Windows 10/11 portable Electron + React transcription app using OpenAI **gpt-transcribe**.

## User experience
Download the Windows EXE from a successful GitHub Actions workflow artifact, place it in its own folder, and double-click it. On first run enter your OpenAI API key and an encryption password (8+ characters). On later launches enter the same password to unlock the saved key. Choose a recording, optionally enter context, and click Transcribe. Files appear in `Transcriptions/<job-id>/transcript.txt` and `metadata.json` alongside the EXE. No database or web server. The original recording is not copied. The app sends audio chunks to OpenAI for transcription and deletes temporary chunks.

## Development
Requires Node.js 20+ and Windows FFmpeg binaries at `vendor/ffmpeg/ffmpeg.exe` and `vendor/ffmpeg/ffprobe.exe`.
Run `npm install`, `npm run dev`, `npm run check`, `npm run dist`.
Development data is stored in `portable-data/`; packaged data is stored beside the EXE. The app folder must be writable. No API keys belong in Git.

## Windows release
GitHub Actions builds an unsigned portable Windows EXE and uploads it as a workflow artifact. FFmpeg binaries are fetched from gyan.dev for packaging. Check FFmpeg licensing, attribution, and distribution obligations before public release. Windows SmartScreen may warn about unsigned software. Portable Electron executables can extract internal runtime resources temporarily.

## Security
The key is encrypted with AES-256-GCM and a password-derived scrypt key in `AppData/credentials.json`. The password is not stored, and must be entered after each launch. The key is only used in the Electron main process. No telemetry or hosted backend. Audio **does leave the computer** for OpenAI. Anyone who knows the password and has the credentials file can use the API key.

## MVP limitations
Audio is converted locally to mono 16 kHz MP3, split into 8-minute chunks and sent sequentially. The API's 25 MB per-file limit is checked. Progress is per chunk; speaker labels, timestamps, retries across restarts, and transcript editing are not implemented yet. Test the packaged EXE on a clean Windows 10/11 PC before distribution.


## Portable family use (updated)
The Windows GitHub Actions workflow builds a **clean PortableApp folder** containing a no-install PortableScribe.exe and a start guide. The downloadable artifact is named `PortableApp-Windows`. The repository's `PortableApp/` folder contains instructions only until a built executable is added separately. Windows build and runtime still need verification.

The app now **remembers the API key automatically** in `AppData/credentials.json` next to the portable EXE. **The key is stored as plaintext**, not encrypted. Do not commit or share `AppData/`; distribute a clean app folder and let each family member enter their own key. Transcripts are stored in `Transcriptions/` beside the EXE. See `AGENTS.md` and `docs/ARCHITECTURE.md`.
