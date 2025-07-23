Sematic Video Retriever
===
**Problem Statement**
The goal is to search through stored video data using natural language commands, either in spoken or written form. These commands are expressed in plain English and aim to retrieve video segments that semantically match the query.

**Project Objective**<br>
**1.Voice-to-Text Interpretation**<br>
Convert voice commands into text using automatic speech recognition (ASR).<br>
**2. Semantic Video Search**<br>
Use the interpreted or typed sentence to search across a large collection of pre-processed video files and identify relevant scenes.<br>
**3. Clip Retrieval**<br>
Extract and return short video clips that match the semantics of the input sentence.

Steps Involved
===
1. Collect the video data
2. Preprocess the videos
3. Extract visual features with CLIP
4. Store embeddings and metadata
5. Accept user query (Text or Voice)
6. LangChain agent orchestration
7. Search videos using CLIP
8. Return matching video scenes

**1. Collect the video data**
* Relevant video footage is collected to support the use case of traffic surveillance and monitoring. Videos may be sourced from:
    1. Public repositories and free stock footage platforms (e.g., Vecteezy, Pixabay, Pexels)
    2. Open datasets related to smart city or transportation research
    3. Synthetic or recorded surveillance streams
* The collected videos are placed in the video_data/raw_videos/ directory.
* Multiple formats such as .mp4, .mov, and .avi are accepted.

**2. Preprocessing of Videos**<br>
To prepare the videos for semantic indexing and retrieval, the following preprocessing steps are applied:
1.  **Format Standardization**
All videos are converted to the .mp4 format using FFmpeg, so that a consistent codec is ensured for downstream processing.
2. **Scene-Level Splitting**
Each video is divided into fixed-length clips (e.g., 5 seconds per clip) using OpenCV. These shorter segments are treated as the searchable units.
3.  **Output Organization**
The converted .mp4 files are stored in video_data/converted_videos/. The scene clips are stored in video_data/scenes/. The time taken to process each video is logged to monitor performance and efficiency.

**3. Extraction of CLIP Embeddings**<br>
To semantically index each scene clip for later search:<br>
1. **Middle Frame Extraction**
The center frame of each 5-second clip is extracted using OpenCV to represent the scene visually. <br>
2. **Embedding Generation**
The frame is passed through OpenAI’s CLIP model (clip-vit-base-patch32) to produce a 512-dimensional embedding.<br>
3. **Output Organization**
Embeddings are saved as .npy files in the embeddings/ directory, with filenames matching the input clip.