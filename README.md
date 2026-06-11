# Shopee Video Downloader v2

Minimal Chrome Extension Manifest V3 for detecting and downloading Shopee MY/SG product videos.

## Scope

- Runs on `shopee.com.my`, subdomains of `shopee.com.my`, `shopee.sg`, and subdomains of `shopee.sg`.
- Detects video URLs from:
  - `video.currentSrc`
  - `video.src`
  - `source.src`
  - performance resource entries
  - fetch/XHR URLs observed after the content script loads
- Keeps accumulated detections across rescans for lazy-loaded videos.
- Uses exact normalized URL dedupe only.
- Removes only volatile query parameters: `t`, `timestamp`, `_`, `token`, `auth_key`, `expires`, `expiry`, `signature`, `sign`.

## Panel

The floating panel shows:

- detected video count
- minimum size filter, default `1 MB`
- Refresh
- Download All
- detected video list

`Download All` downloads all visible videos after the size filter, waiting 700 ms between downloads.

## Filename Rules

Filenames use:

1. Shopee product title when available
2. URL slug
3. `document.title` only when it is not generic

Format:

```text
product-title (1).mp4
product-title (2).mp4
```

Names are sanitized for Windows and capped at 180 characters before the numbered suffix.

## Install

1. Open Chrome Extensions: `chrome://extensions`
2. Enable Developer mode.
3. Click Load unpacked.
4. Select this folder.

## Project Structure

```text
shopee-video-downloader-v2/
  background.js
  CHANGELOG.md
  content.js
  icons/
    icon16.png
    icon48.png
    icon128.png
  manifest.json
  privacy-policy.md
  README.md
  screenshots/
  style.css
```

## Verify

```powershell
python3 -m json.tool manifest.json
node --check background.js
node --check content.js
```
