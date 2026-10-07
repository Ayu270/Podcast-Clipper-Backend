# AI Podcast Clipper

An NLP-based AI podcast clip generation system that automatically
converts long-form podcast videos into short, engaging vertical clips.

The project uses **WhisperX** for speech transcription and word-level
timestamps, and **Google Gemini** through an API call to identify
meaningful moments such as questions, answers, and stories that can be
converted into short-form clips.

## Project Overview

The system follows this pipeline:

``` text
Podcast Video
      ↓
Audio Extraction
      ↓
WhisperX Transcription
      ↓
Word-level Timestamps
      ↓
Gemini LLM
      ↓
Identify Meaningful Moments
      ↓
Clip Extraction
      ↓
Speaker-aware Vertical Video
      ↓
Automatic Subtitles
      ↓
Upload Generated Clip to AWS S3
```

## NLP / LLM Component

The main NLP functionality is the semantic identification of useful
podcast moments.

WhisperX converts the podcast speech into a timestamped transcript. The
transcript is then provided to the Gemini LLM. Gemini analyzes the
transcript and identifies suitable sections for short-form clips.

The LLM is instructed to:

-   Find stories or questions with corresponding answers.
-   Generate clips between 30 and 60 seconds.
-   Prefer longer clips between 40 and 60 seconds.
-   Avoid greetings, thanking, and goodbye sections.
-   Avoid overlapping clips.
-   Use only timestamps provided by the transcript.
-   Return the selected clip timestamps as JSON.

The complete prompt used by the application is available in
[`prompt.txt`](prompt.txt).

## Technologies Used

-   **Python**
-   **Google Gemini API**
-   **WhisperX**
-   **Modal**
-   **AWS S3**
-   **FFmpeg**
-   **OpenCV**
-   **PyTorch**
-   **NumPy**
-   **FastAPI**
-   **pysubs2**
-   **ffmpegcv**

## Main Components

### `main.py`

Contains the main application logic, including:

-   Modal GPU environment configuration
-   WhisperX model loading
-   Audio extraction
-   Podcast transcription
-   Word-level timestamp alignment
-   Gemini API integration
-   Semantic clip identification
-   Video clip extraction
-   Vertical video generation
-   Speaker/face-aware cropping
-   Subtitle generation
-   AWS S3 upload
-   FastAPI endpoint

### `prompt.txt`

Contains the prompt used by the Gemini LLM to identify meaningful
podcast moments.

### `config.json`

Contains the project's configuration and processing settings, including:

-   Video resolution
-   Frame rate
-   Clip duration
-   WhisperX configuration
-   Gemini model
-   Subtitle settings
-   Modal GPU settings
-   AWS S3 information

### `requirements.txt`

Contains the Python dependencies required by the project.

### `asd/`

Contains the supporting speaker/face-processing code used during video
processing.

## LLM Workflow

1.  A podcast video is received through the backend API.
2.  The video is downloaded from AWS S3.
3.  Audio is extracted from the video.
4.  WhisperX transcribes the audio and generates word-level timestamps.
5.  The timestamped transcript is passed to Gemini.
6.  Gemini identifies suitable stories or question-answer sections.
7.  The returned JSON contains the start and end timestamps of the
    selected moments.
8.  The system extracts the corresponding video segment.
9.  Speaker/face information is used to create a vertical 1080 × 1920
    video.
10. Automatically generated subtitles are added.
11. The final clip is uploaded back to AWS S3.

## Configuration

The project uses environment variables / Modal Secrets for sensitive
credentials.

Required secrets include:

``` text
GEMINI_API_KEY
AUTH_TOKEN
```

AWS credentials should also be provided through the deployment
environment rather than hardcoded into the source code.

**Do not commit `.env` files, API keys, access keys, secret keys, or
other credentials to GitHub.**

## Running the Project

The backend is designed to run using **Modal** with GPU support.

Install the Python dependencies:

``` bash
pip install -r requirements.txt
```

Configure the required Modal secrets and deployment environment.

Then deploy the application using the Modal CLI:

``` bash
modal deploy main.py
```

The deployed application exposes a POST endpoint for processing videos.

### API Request

The endpoint accepts a request containing an S3 key:

``` json
{
  "s3_key": "path/to/input-video.mp4"
}
```

The endpoint uses Bearer Token authentication.

## Output

The generated clips are:

-   Vertical format: **1080 × 1920**
-   Video format: **MP4**
-   Automatically subtitled
-   Speaker-aware where face tracking is available
-   Stored in AWS S3

## Project Requirements

This project was developed as an NLP project demonstrating meaningful
integration of an LLM through an API.

The project includes:

-   Source code
-   LLM prompt file
-   Configuration file
-   Dependency file
-   Supporting processing code

## Repository Structure

``` text
Podcast-Clipper-Backend/
│
├── asd/
│   └── supporting processing code
│
├── config.json
├── main.py
├── prompt.txt
├── requirements.txt
├── README.md
└── .gitignore
```

## Security

Sensitive credentials are not stored directly in the source code. Gemini
authentication and API authorization values are obtained from
environment variables / Modal Secrets.

Large model weights and generated media files should not be committed
directly to the repository unless appropriate storage such as Git LFS is
configured.

## Author

**Ayush Kumar**

B.Tech --- Manipal University Jaipur
