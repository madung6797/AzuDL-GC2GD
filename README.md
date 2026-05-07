# AzuDl - GC2GD

<p align="center">
  <a href="AzuDl-GC2GD-v1.2.0-README.fa.md">فارسی</a> · <strong>English</strong>
</p>

<p align="center">
  <strong>Azizi Universal Downloader - Google Colab to Google Drive</strong>
</p>

<p align="center">
  A powerful Google Colab downloader and file utility toolkit that saves downloads directly to Google Drive.
</p>

<p align="center">
  <code>Google Colab</code> · <code>Google Drive</code> · <code>aria2</code> · <code>yt-dlp</code> · <code>FFmpeg</code> · <code>Python</code>
</p>

---

## Overview

**AzuDl - GC2GD** stands for:

> **Azizi Universal Downloader - Google Colab to Google Drive**

It is a Google Colab-based downloader that saves supported downloads directly into Google Drive.

Version **1.2.0** improves the original downloader with better torrent handling, `.torrent` file support, direct-link headers, YouTube metadata options, storage reports, SHA256 hashing, ZIP tools, and aria2 management utilities.

---

## For Regular Users

AzuDl is useful when you want to download supported files without keeping your personal computer running.

You open Google Colab, run the code, connect Google Drive, paste a supported link, and the final file is saved into your Drive.

You can use it for:

- Direct file links
- YouTube videos
- YouTube playlists
- YouTube audio extraction as MP3
- Magnet torrents
- `.torrent` files
- Batch downloads
- ZIP creation
- File integrity checking with SHA256

---

## For Developers

The project is built around one Python class:

```python
class AzuDlGC2GD:
```

It manages:

- Google Drive mounting
- Project folder creation
- aria2 RPC startup
- JSON-RPC communication with aria2
- Magnet metadata detection
- Real torrent GID resolution after metadata
- `.torrent` loading through `aria2.addTorrent`
- Direct URL downloads through aria2
- YouTube downloads through `yt-dlp`
- Progress bars through `tqdm.notebook`
- Download history
- Storage reports
- SHA256 hashing
- ZIP archive creation
- aria2 task management

---

## Features

### Download Features

- Magnet torrent downloads
- Real torrent progress after metadata fetching
- `.torrent` file download from URL or local path
- Direct link downloads
- Optional HTTP headers for direct links
- YouTube video downloads
- YouTube playlist downloads
- YouTube audio-only MP3 extraction
- YouTube quality selection
- Custom YouTube format ID support
- Optional YouTube metadata and thumbnail saving
- Batch download mode
- Speed limit support for aria2 downloads
- Resume support

### File Utility Features

- List downloaded files
- Show latest downloaded file
- Google Drive storage report
- Project folder size report
- SHA256 hash for latest file
- SHA256 hash for selected file
- ZIP any folder
- ZIP latest downloaded folder
- Download history log

### aria2 Management Features

- Show active, waiting, and stopped aria2 tasks
- Remove aria2 GID
- Clear stopped aria2 results
- Better torrent status display
- Better progress details with speed, percentage, connections, and seeders

---

## Menu

```text
1. Auto detect link
2. Torrent magnet
3. Torrent file
4. YouTube video or playlist
5. Direct link
6. Batch download
7. Download history
8. List downloaded files
9. Storage report
10. SHA256 latest file
11. SHA256 selected file
12. ZIP folder
13. ZIP latest folder
14. aria2 status
15. Remove aria2 GID
16. Clear stopped aria2 results
17. Latest file
18. Developer
19. Help
20. Exit
```

---

## Storage Structure

AzuDl creates this directory:

```text
/content/drive/MyDrive/AzuDl-GC2GD
```

Folder layout:

```text
AzuDl-GC2GD/
├── TorrentDownloads/
├── YouTubeDownloads/
├── DirectDownloads/
├── BatchDownloads/
├── Archives/
└── Logs/
    └── download_history.json
```

| Folder | Purpose |
|---|---|
| `TorrentDownloads` | Magnet and `.torrent` downloads |
| `YouTubeDownloads` | YouTube video, playlist, audio, metadata, and thumbnail outputs |
| `DirectDownloads` | Direct URL downloads |
| `BatchDownloads` | Grouped batch downloads |
| `Archives` | ZIP archives created by the tool |
| `Logs` | Download history and logs |

---

## Torrent Improvements in v1.2.0

Magnet links work in stages:

```text
Magnet link
  ↓
Metadata download
  ↓
Real torrent task
  ↓
Actual file download
```

Older versions could show only the metadata download, such as:

```text
Torrent: 100% 5.77k/5.77k
```

That was not the real file download. It was only the torrent metadata.

Version **1.2.0** detects the real torrent `GID` after metadata is fetched and monitors the actual file download.

Expected output:

```text
Magnet added
Metadata GID: ...
Fetching metadata: 100%
Metadata completed
Real torrent GID: ...
Starting torrent download monitor
Torrent Download: ...
```

---

## Torrent Magnet Usage

Choose:

```text
2. Torrent magnet
```

Then paste:

```text
magnet:?xt=urn:btih:EXAMPLE_HASH
```

Optional speed limit examples:

```text
500K
2M
10M
```

---

## Torrent File Usage

Choose:

```text
3. Torrent file
```

You can enter a `.torrent` URL:

```text
https://example.com/file.torrent
```

or a local Colab/Drive path:

```text
/content/drive/MyDrive/file.torrent
```

---

## YouTube Usage

Choose:

```text
4. YouTube video or playlist
```

Supported examples:

```text
https://www.youtube.com/watch?v=VIDEO_ID
https://youtu.be/VIDEO_ID
https://www.youtube.com/playlist?list=PLAYLIST_ID
https://music.youtube.com/watch?v=VIDEO_ID
```

Quality presets:

```text
best
4320
2160
1440
1080
720
480
360
```

Custom format examples:

```text
137+140
248+251
22
18
best
```

Audio-only mode saves MP3 output. Metadata mode can save `.info.json` and thumbnails.

---

## Direct Link Usage

Choose:

```text
5. Direct link
```

Supported protocols:

```text
http://
https://
ftp://
```

Optional fields:

```text
Folder name
File name
Speed limit
Headers JSON
```

Header example:

```json
{"User-Agent":"Mozilla/5.0","Referer":"https://example.com"}
```

---

## Batch Download

Choose:

```text
6. Batch download
```

Paste links one by one. Submit an empty line to start.

Batch mode supports:

- Magnet links
- `.torrent` URLs
- YouTube links
- Direct links

---

## Storage Report

Choose:

```text
9. Storage report
```

It shows:

- Total mounted storage
- Used storage
- Free storage
- Size of each AzuDl project folder

---

## SHA256

Choose:

```text
10. SHA256 latest file
```

or:

```text
11. SHA256 selected file
```

SHA256 helps verify file integrity after download.

---

## ZIP Tools

Choose:

```text
12. ZIP folder
```

to zip a folder by path.

Choose:

```text
13. ZIP latest folder
```

to zip the most recently modified downloaded folder.

ZIP files are saved in:

```text
/content/drive/MyDrive/AzuDl-GC2GD/Archives
```

---

## aria2 Tools

Choose:

```text
14. aria2 status
```

to view active, waiting, and stopped aria2 tasks.

Choose:

```text
15. Remove aria2 GID
```

to remove a task by GID.

Choose:

```text
16. Clear stopped aria2 results
```

to clean old stopped results from aria2.

---

## Download History

History is saved at:

```text
/content/drive/MyDrive/AzuDl-GC2GD/Logs/download_history.json
```

Example:

```json
{
  "type": "youtube",
  "source": "https://www.youtube.com/watch?v=VIDEO_ID",
  "output": "/content/drive/MyDrive/AzuDl-GC2GD/YouTubeDownloads/Example",
  "format": "bv*+ba/best",
  "status": "completed",
  "time": "2026-05-06 18:30:00"
}
```

---

## Installation

Paste the full source code into a Google Colab cell and run it.

The code installs:

```text
aria2
ffmpeg
p7zip-full
tqdm
requests
yt-dlp
```

---

## Troubleshooting

### Google Drive mount failed

Try:

```text
Runtime > Restart session
```

or run:

```python
from google.colab import drive
drive.flush_and_unmount()
```

Then restart the runtime.

Other fixes:

- Use only one Google account in the browser
- Open Colab in Incognito mode
- Allow third-party cookies
- Reconnect Google Drive manually from the Colab file panel

### Torrent metadata downloads but real file does not start

Possible reasons:

- No seeders
- Weak torrent
- Metadata found but no peers available
- Network restrictions

Use:

```text
14. aria2 status
```

to inspect active, waiting, and stopped tasks.

### YouTube download fails

Try updating yt-dlp:

```python
!pip install -U yt-dlp
```

### Direct link fails

Possible reasons:

- Expired link
- Missing headers
- Server blocks Colab
- Authentication required
- Temporary token expired

Try using custom headers JSON.

---

## Responsible Use

AzuDl is a downloader and file utility tool. Use it only for files and content you have permission to download, store, or process.

Appropriate uses include:

- Your own files
- Open-source releases
- Public domain content
- Creative Commons content
- Backups of your own data
- Files shared with permission

Do not use this tool to violate copyright, bypass access controls, or download unauthorized content.

---

## Developer

**Project:** AzuDl - GC2GD  
**Full Name:** Azizi Universal Downloader - Google Colab to Google Drive  
**Developer:** The Azizi

### Links

- X: https://x.com/the_azzi
- GitHub: https://github.com/TheGreatAzizi
- Telegram: https://t.me/luluch_code
- Git: https://git.theazizi.ir/TheAzizi
- Website: https://theazizi.ir

---

## Version

```text
Current version: 1.2.0
```
