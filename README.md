# n8n-workflows
this workflow automatically downloads and uploads videos on a yt channel without doing any work

# ⚙️ Project Description: Automatic YouTube Uploader Workflow
This repository most likely contains the configuration for an n8n workflow designed to automatically download videos, prepare them for upload, and track their status on YouTube using Google Sheets for management.

Core Functionality
The workflow operates on a scheduled interval (every 6 hours) and performs a complete cycle of content management:

Video Selection: It connects to a Google Sheet ("1Lx1wAb1Wn-wgnQYOyAaBukKzs86JG0ev6wJo4T-a1V0") to read rows that have not yet been processed (status is not yet updated).

Metadata Generation: It generates a unique random file name for the video and defines a target folder ("footer").

Video Download: It uses the yt-dlp command-line tool to download the source video URL fetched from the Google Sheet, saving it to a local path (./footer/generated_name.mp4).

Status Update (Preparation): It updates the Google Sheet row to mark the video as "Success" and records the internal file path.

YouTube Upload:

It initiates the YouTube resumable upload process to create a new video link with predefined metadata (title, description, tags, privacy status).

It reads the local video file from the disk.

It executes an HTTP PUT request to the link provided by YouTube to upload the actual video file.

Status Update (Completion) & Cleanup:

It updates the Google Sheet row to mark the video as "Uploaded: Yes".

It runs a shell command (rm) to delete the local video file after the successful upload, ensuring no unnecessary storage is used.
