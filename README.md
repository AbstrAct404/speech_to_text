# Mac Recording Script Generator

Small macOS project that records audio with the built-in QuickTime Player, sends the recording to OpenAI for transcription, and generates a cleaned Markdown script from the recording content.

## Requirements

- macOS
- Node.js 18.17 or newer
- An OpenAI API key
- Microphone permission for QuickTime Player on first recording

## Setup

```bash
cd /Users/studyhard/NYU/Coding/Translator
cp .env.example .env
```

Edit `.env` and set `OPENAI_API_KEY`.

Run a quick local check:

```bash
npm run check
```

## Record and Generate a Script

Record 60 seconds through QuickTime Player, transcribe it, and generate a Markdown script:

```bash
npm run record -- --seconds 60 --title "class-notes"
```

The app saves:

- `recordings/<timestamp>.m4a`
- `outputs/<timestamp>.transcript.txt`
- `outputs/<timestamp>.script.md`

## Use an Existing Recording

If you already recorded audio with Voice Memos, QuickTime Player, or another app, export the audio as `m4a`, `mp3`, `wav`, `mp4`, `mpeg`, `mpga`, or `webm`, then run:

```bash
npm run from-file -- ./path/to/recording.m4a --title "interview"
```

## Useful Options

```bash
--seconds 45                 Recording length for the record command
--title "my note"            Friendly filename label
--language en                Optional input language hint for transcription
--target-language English    Optional final script language
--style "podcast intro"      Optional style guidance for generated script
--no-script                  Only create the transcript
```

Examples:

```bash
npm run record -- --seconds 120 --language en --style "clear lecture script"
npm run from-file -- ./audio.m4a --target-language "Simplified Chinese"
```

## Notes

- QuickTime Player is used because it is built into macOS and can be automated with AppleScript.
- OpenAI file transcription uploads are currently limited to 25 MB. For longer recordings, split the audio first.
- Model names are configurable in `.env` so you can switch to another compatible OpenAI model without changing the code.
