# YouTube Video Downloader for Termux

A simple bash script to download YouTube videos in your preferred format directly to your Android device using Termux.

## Prerequisites

Before starting, ensure you have Termux installed on your Android device.

## Installation

### Step 1: Setup Storage Access
```bash
termux-setup-storage
```
Grant storage permission when prompted to allow downloads to your device's storage.

### Step 2: Update Packages
```bash
pkg update && pkg upgrade
```

### Step 3: Install Required Packages
```bash
pkg install python ffmpeg termux-api
```

### Step 4: Install yt-dlp
```bash
python3 -m pip install -U yt-dlp
```

## Setup

### Create the Download Script
```bash
nano yt_download.sh
```

Copy and paste the following code:

```bash
#!/bin/bash

# Prompt for YouTube URL input
read -p "Enter YouTube URL: " URL

echo "Fetching available formats for the video..."
yt-dlp -F "$URL"

echo ""
# Prompt for format code to download
read -p "Enter format code number to download (e.g., 18 for mp4): " FORMAT_CODE

echo "Downloading to ~/storage/downloads ..."
yt-dlp -f "$FORMAT_CODE" -o '~/storage/downloads/%(title)s.%(ext)s' "$URL"

echo "Download complete! Check your Downloads folder."
```

Save the file by pressing `Ctrl+X`, then `Y`, then `Enter`.

### Make the Script Executable
```bash
chmod +x yt_download.sh
```

## Usage

Run the script:
```bash
./yt_download.sh
```

The script will:
1. Ask for the YouTube URL
2. Display all available formats
3. Ask you to choose a format code
4. Download the video to your Downloads folder

## Notes

- Downloaded videos are saved to `~/storage/downloads/`
- Format codes (like 18 for mp4) vary by video
- Higher format codes typically mean better quality

## Troubleshooting

### Permission Denied Error
If you get a permission error when running the script:
```bash
chmod +x yt_download.sh
```

### Storage Not Accessible
If downloads fail due to storage access:
```bash
termux-setup-storage
```
Then restart Termux and grant the permission again.

### yt-dlp Update
Keep yt-dlp updated for best compatibility:
```bash
python3 -m pip install -U yt-dlp
```

## License

Free to use and modify.
