# 🎙️ AI Podcast Clipper — NLP Project

An AI-powered podcast video processing system that uses **Automatic Speech Recognition (ASR), Natural Language Processing (NLP), and Large Language Models (LLMs)** to automatically identify meaningful moments from long-form podcast videos and convert them into short-form clips.

The system uses **WhisperX** for speech transcription and word-level timestamp alignment, and **Google Gemini** for semantic understanding and intelligent clip selection.

---

## 📌 Project Overview

Long-form podcasts contain valuable discussions, stories, questions, and insights, but manually finding the best short-form moments is time-consuming.

This project automates that process.

Given a podcast video, the system:

1. Extracts the audio.
2. Transcribes the speech using WhisperX.
3. Generates word-level timestamps.
4. Sends the timestamped transcript to an LLM.
5. Uses the LLM to identify meaningful questions, answers, stories, and insights.
6. Selects suitable 30–60 second segments.
7. Extracts the corresponding video clips.
8. Generates subtitles and processes the final short-form videos.

The final output can be used for platforms such as **YouTube Shorts, Instagram Reels, and TikTok**.

---

# 🎯 Objectives

The main objectives of this project are:

- Automate podcast highlight extraction.
- Apply NLP techniques to real-world spoken language.
- Use an LLM for semantic understanding of podcast conversations.
- Identify self-contained and engaging sections of long-form content.
- Preserve accurate temporal alignment between transcript and video.
- Generate short-form videos automatically.
- Reduce the amount of manual effort required for content creation.

---

# 🧠 NLP Pipeline

The project combines multiple NLP and AI components.

```text
                 Podcast Video
                       │
                       ▼
                Audio Extraction
                       │
                       ▼
                 WhisperX ASR
                       │
                       ▼
            Speech Transcription
                       │
                       ▼
          Word-Level Timestamping
                       │
                       ▼
            Timestamped Transcript
                       │
                       ▼
                Gemini LLM
                       │
             Semantic Analysis
                       │
        ┌──────────────┼──────────────┐
        ▼              ▼              ▼
     Questions       Stories       Insights
        │              │              │
        └──────────────┼──────────────┘
                       ▼
              Candidate Segments
                       │
                       ▼
             30–60 Second Clips
                       │
                       ▼
             Video Processing
                       │
                       ▼
              Subtitle Generation
                       │
                       ▼
              Final Short Videos
```

---

# 🔍 NLP Techniques Used

## 1. Automatic Speech Recognition

**WhisperX** is used to convert the podcast's audio into text.

Unlike basic transcription systems, WhisperX provides accurate **word-level timestamps**, which allow the system to map individual words back to their corresponding positions in the video.

Example:

```json
{
  "word": "podcast",
  "start": 125.42,
  "end": 125.91
}
```

These timestamps are essential for extracting the correct portion of the original video.

---

## 2. Transcript Processing

The generated transcript is converted into a structured representation containing:

- Speaker information
- Words
- Start timestamps
- End timestamps

This structured transcript is provided to the LLM for semantic analysis.

---

## 3. LLM-Based Semantic Understanding

Google Gemini is used to understand the meaning and context of the podcast conversation.

The LLM identifies segments containing:

- Meaningful questions and answers
- Complete stories
- Interesting explanations
- Strong opinions
- Surprising insights
- Informative discussions

This allows the system to select clips based on **semantic relevance rather than simply selecting random timestamps**.

---

## 4. Semantic Clip Selection

The LLM is instructed to select clips satisfying specific constraints:

- Minimum duration: **30 seconds**
- Maximum duration: **60 seconds**
- Prefer approximately **40–60 seconds**
- Avoid greetings and introductions
- Avoid advertisements
- Avoid incomplete conversations
- Prefer self-contained discussions
- Avoid overlapping clips

The LLM returns the selected timestamps in structured JSON format.

Example:

```json
[
  {
    "start": 125.4,
    "end": 174.8
  }
]
```

These timestamps are then used to extract the corresponding section of the original video.

---

# 🤖 LLM Integration

The project uses the **Google Gemini API** for semantic analysis.

### LLM

```text
Provider: Google Gemini
Model: gemini-3-flash-preview
```

The LLM receives the timestamped transcript and identifies the most valuable sections of the podcast.

The LLM is not used simply for text generation. It performs a specific NLP task:

> **Semantic identification and temporal localization of meaningful podcast segments.**

This makes the LLM an integral component of the NLP pipeline.

---

# 📝 Prompt Engineering

The LLM prompt is stored separately in:

```text
prompt.txt
```

The prompt defines:

### Content requirements

The model is instructed to prioritize:

- Questions followed by meaningful answers
- Complete stories
- Informative explanations
- Strong insights
- Engaging discussions

### Temporal requirements

```text
Minimum duration: 30 seconds
Maximum duration: 60 seconds
Preferred duration: 40–60 seconds
```

### Exclusion criteria

The model should avoid:

- Greetings
- Introductions
- Advertisements
- Thank-you messages
- Incomplete conversations
- Segments requiring substantial missing context

### Output format

The model is instructed to return structured JSON containing the start and end timestamps.

This makes the LLM output easier to process programmatically.

---

# 🏗️ System Architecture

```text
Client
  │
  │ Upload Podcast
  ▼
Backend API
  │
  ├── Download / Store Video
  │
  ├── Extract Audio
  │
  ▼
WhisperX
  │
  ├── Speech Recognition
  ├── Word Alignment
  └── Speaker Information
  │
  ▼
Structured Transcript
  │
  ▼
Gemini API
  │
  ├── Semantic Understanding
  ├── Moment Identification
  └── Timestamp Selection
  │
  ▼
Clip Processing
  │
  ├── Video Cutting
  ├── Subtitle Generation
  └── Formatting
  │
  ▼
Final Short-Form Video
```

---

# 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Python | Backend and NLP processing |
| WhisperX | Speech recognition and word-level alignment |
| Google Gemini | LLM-based semantic analysis |
| FFmpeg | Audio/video processing |
| MoviePy | Video manipulation |
| JSON | Structured LLM output |
| AWS S3 | File storage |
| Flask / API layer | Backend API |
| NumPy / supporting libraries | Data processing |

---

# 📁 Project Structure

```text
Podcast-Clipper-Backend/
│
├── main.py
├── prompt.txt
├── config.json
├── requirements.txt
├── .gitignore
├── LICENSE
└── README.md
```

### `main.py`

Contains the main backend pipeline, including:

- Audio extraction
- WhisperX transcription
- Transcript processing
- Gemini API integration
- Clip identification
- Video processing

### `prompt.txt`

Contains the prompt used by the LLM for podcast moment identification.

### `config.json`

Contains configurable project parameters such as:

- Clip duration
- Whisper configuration
- Video settings
- LLM configuration
- Processing settings

### `requirements.txt`

Contains the Python dependencies required to run the project.

---

# ⚙️ Installation

## 1. Clone the repository

```bash
git clone https://github.com/Ayu270/Podcast-Clipper-Backend.git
```

```bash
cd Podcast-Clipper-Backend
```

---

## 2. Create a virtual environment

### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

### Linux / macOS

```bash
python3 -m venv venv
source venv/bin/activate
```

---

## 3. Install dependencies

```bash
pip install -r requirements.txt
```

---

# 🔑 Configuration

Create a `.env` file in the project root.

Example:

```env
GEMINI_API_KEY=your_gemini_api_key
AUTH_TOKEN=your_auth_token

AWS_ACCESS_KEY_ID=your_aws_access_key
AWS_SECRET_ACCESS_KEY=your_aws_secret_key
AWS_DEFAULT_REGION=your_aws_region
```

> Never commit your actual API keys or credentials to GitHub.

---

# ⚙️ Configuration File

Project-level settings are stored in:

```text
config.json
```

Important parameters include:

```json
{
  "min_clip_duration": 30,
  "max_clip_duration": 60
}
```

These values ensure that generated clips are appropriate for short-form content.

---

# ▶️ Running the Project

After configuring the required environment variables:

```bash
python main.py
```

The backend can then receive a podcast/video input and process it through the complete NLP pipeline.

---

# 🔄 Processing Workflow

## Step 1 — Input

The system receives a long-form podcast video.

```text
podcast.mp4
```

---

## Step 2 — Audio Extraction

The audio track is extracted from the video.

```text
podcast.mp4
      ↓
podcast.wav
```

---

## Step 3 — Speech Recognition

WhisperX converts the audio into text.

```text
Audio
  ↓
WhisperX
  ↓
Transcript
```

---

## Step 4 — Word-Level Alignment

Each word is associated with its timestamp.

```text
"I"
12.10 – 12.20

"started"
12.21 – 12.60

"coding"
12.61 – 13.10
```

This allows the system to accurately locate content in the original video.

---

## Step 5 — LLM Analysis

The timestamped transcript is sent to Gemini.

The model identifies meaningful sections based on:

- Semantic relevance
- Completeness
- Narrative structure
- Informational value
- Audience engagement

---

## Step 6 — Clip Selection

The LLM returns timestamps.

Example:

```json
[
  {
    "start": 120,
    "end": 168
  }
]
```

---

## Step 7 — Video Processing

The selected timestamp range is extracted from the original video.

```text
Original Podcast
      │
      ├── 00:00–02:00
      ├── 02:00–02:48  ← Selected
      ├── 02:48–05:00
      │
      ▼
Short Clip
```

---

## Step 8 — Subtitle Generation

The transcript timestamps are used to generate subtitles for the selected section.

The final video can therefore contain synchronized captions.

---

# 📊 Evaluation

The project can be evaluated using both quantitative and qualitative metrics.

## Quantitative Metrics

| Metric | Description |
|---|---|
| Clip validity | Percentage of generated clips satisfying duration constraints |
| Timestamp accuracy | Whether selected timestamps correctly map to the intended content |
| JSON validity | Percentage of successful structured LLM responses |
| Non-overlapping clips | Percentage of clips without temporal overlap |
| Processing time | Total time required to process a podcast |
| LLM response time | Time required for semantic analysis |

---

## Qualitative Metrics

Human evaluation can be performed based on:

1. **Content relevance**
2. **Context completeness**
3. **Story/narrative coherence**
4. **Engagement potential**
5. **Accuracy of selected timestamps**
6. **Overall clip quality**

Example evaluation:

| Sample | Relevant | Complete Context | Engaging | Correct Timestamp |
|---|---|---|---|---|
| Podcast 1 | ✓ | ✓ | ✓ | ✓ |
| Podcast 2 | ✓ | ✓ | ✓ | ✓ |
| Podcast 3 | ✓ | ✗ | ✓ | ✓ |
| Podcast 4 | ✓ | ✓ | ✓ | ✓ |

---

# ⚡ Efficiency Considerations

The system is designed to reduce unnecessary processing by:

- Processing the audio before performing semantic analysis.
- Using word-level timestamps rather than manually searching the video.
- Sending structured transcript information to the LLM.
- Restricting the LLM to a specific output format.
- Applying fixed duration constraints.
- Performing automated video extraction after semantic selection.

The LLM is used specifically for the task that requires semantic understanding rather than for conventional video-processing operations.

---

# 🧪 Example

### Input

```text
Long-form podcast episode
Duration: 60 minutes
```

### Processing

```text
60-minute video
      ↓
Audio extraction
      ↓
WhisperX
      ↓
Timestamped transcript
      ↓
Gemini
      ↓
Meaningful moments
      ↓
30–60 sec clips
```

### Example LLM output

```json
[
  {
    "start": 842.4,
    "end": 891.7
  },
  {
    "start": 1432.1,
    "end": 1484.2
  }
]
```

### Output

```text
clip_1.mp4
clip_2.mp4
```

Each clip corresponds to a semantically meaningful section of the original podcast.

---

# 🔐 Security

Sensitive credentials should be stored in environment variables.

Do not commit:

```text
.env
API keys
AWS credentials
Authentication tokens
```

to the repository.

The `.gitignore` file should exclude sensitive configuration files.

---

# ⚠️ Limitations

The current system has several limitations:

- LLM-based selection may occasionally choose a segment that requires additional context.
- Transcription quality depends on audio quality.
- Background noise can affect speech recognition.
- LLM responses may occasionally require validation.
- Processing long podcasts can require significant computational resources.
- GPU availability can affect WhisperX processing speed.
- LLM API usage is subject to provider limits and costs.

---

# 🚀 Future Improvements

Possible improvements include:

### 1. Better Clip Ranking

Instead of returning only candidate clips, assign each clip a score based on:

```text
Relevance
+ Engagement
+ Completeness
+ Narrative quality
```

---

### 2. Multi-Stage LLM Pipeline

Use separate stages for:

```text
Transcript Analysis
        ↓
Candidate Detection
        ↓
Candidate Ranking
        ↓
Final Selection
```

---

### 3. Automated Clip Validation

Automatically verify:

- Duration
- Timestamp validity
- Transcript completeness
- Clip overlap
- JSON schema

before video processing.

---

### 4. Multiple LLM Support

The architecture can be extended to support other LLM providers such as:

- OpenAI
- Anthropic
- Google Gemini
- Local open-source models

---

### 5. Improved Content Ranking

A future version could combine LLM semantic scores with:

- Sentiment analysis
- Topic relevance
- Keyword importance
- Speech intensity
- Audience engagement predictions

---

# 📚 Conclusion

This project demonstrates how **NLP and LLM technologies can be applied to a real-world multimedia problem**.

The system combines:

```text
Speech Recognition
        +
Word-Level Alignment
        +
Natural Language Processing
        +
Large Language Models
        +
Temporal Video Processing
```

to automatically transform long-form podcast conversations into short-form, semantically meaningful video clips.

The key NLP component is the use of a Large Language Model to understand the semantic structure of a conversation and identify the most valuable segments while maintaining their temporal relationship with the original video.

---
## Repositories

-   [Frontend](https://github.com/Ayu270/podcast-clipper-frontend)
-   [Backend](https://github.com/Ayu270/Podcast-Clipper-Backend)

# 👨‍💻 Author

**Kumar Ayush**


---
