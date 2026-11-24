# Ses Bölücü

Split an audio or video file in the browser, name the parts and download them separately. The file never leaves your device. The interface is in Turkish.

**Use it:** https://deniztanisman.github.io/media-splitter/

![Ses Bölücü (media splitter)](screenshot.png)

## What it does

- **Load:** MP3, WAV, M4A, OGG, FLAC, or MP4 / WEBM / MOV video. For video, a preview appears above the waveform.
- **Select a part:** press and drag on the waveform, or type the start / end (`1.23` = 1 min 23 s; `1:23.5` works too).
- **Adjust:** while dragging an edge you see the current frame (video) or hear the audio; on release it plays the first 5 s from the start, or the last 5 s before the end.
- **Listen:** "Çal" (play) stops at the end of the part you are in and asks whether to continue. If you continue, the part's end extends along with playback and ends where you stop.
- **Exclude:** take a section out of use; it shows grey on the waveform and is skipped during playback. "Kesilmiş hâlini indir" (download the cut version) gives the whole file without those sections.
- **Join:** merge parts into a single file in any order.
- **Undo:** every change (Cmd/Ctrl+Z).
- **Download:** MP3 (192 kbps), WAV or video (WebM). Each part comes with its own name inside a `.zip`.
- **Text:** if you also choose the written version when downloading (picked file by file in a bulk download), the Mac helper transcribes the speech and adds a `.txt` with the same name.

Video parts are recorded by playing them in the browser: it takes as long as the part lasts, so keep the tab in front until recording finishes. Safari / iPhone can't cut video (you can still get its audio as MP3); use Chrome or Edge.

## Mac helper (optional)

Unpacks Ses Bölücü zips that land in Downloads and deletes the zip; for the requested files it produces `.txt` text with Whisper (on this Mac, offline). It recognises many languages, Turkish included.

```sh
cd helper && ./install.sh
```

Requirements: Apple Silicon Mac, `ffmpeg` (`brew install ffmpeg`), Python 3 (preferably `uv`). The Whisper model downloads once on first use (~1.5 GB).

- `helper/ses-bolucu-unzip.sh` — unzip + text. Only touches zips whose comment says `ses-bolucu`.
- `helper/folder-action.applescript` — Downloads folder action.
- `helper/install.sh` — installs all three.

To remove it: Finder › Downloads › right-click › Quick Actions › Folder Actions Setup › untick `ses-bolucu-unzip.scpt`.

## Technical

A single file: `index.html` (no install). [lamejs](https://github.com/zhuker/lamejs) for MP3, [JSZip](https://stuk.github.io/jszip/) for zip and [fix-webm-duration](https://github.com/yusitnikov/fix-webm-duration) for WebM duration are loaded from a CDN.
