# LiveStar-Colab

A lightweight implementation of **LiveStar-style streaming video understanding** built in **Google Colab** using **OpenRouter** and multimodal LLMs.

This project demonstrates the core ideas from the LiveStar / LiveStarPro papers:

* Streaming video observation
* Event extraction from video frames
* Hierarchical memory construction
* Long-horizon video summarization
* Proactive assistant commentary
* Speak-or-silence decision making

Unlike the original research implementation, this version is designed to run on **free Google Colab** without training any models.

---

# Architecture

```text
Video
 ↓
Frame Sampling
 ↓
Vision LLM (Gemini 2.5 Flash)
 ↓
Event Stream
 ↓
Hierarchical Memory
 ↓
Video Summary
 ↓
Speak / Don't Speak Decision
 ↓
Live Commentary
```

---

# Features

## Streaming Event Detection

Frames are sampled from a video at fixed intervals.

Example:

```text
Person enters room.
Person sits at desk.
Person opens laptop.
```

---

## Hierarchical Memory

Events are grouped into memory nodes.

Example:

```text
Events
 ├─ Person enters room
 ├─ Person sits down
 └─ Person starts working

Memory Node:
"Person entered a room and began working."
```

This approximates the Tree-Structured Hierarchical Memory (TSHM) proposed in LiveStarPro.

---

## Video-Level Understanding

Memory nodes are merged into a final video summary.

Example:

```text
A person entered an office, worked on a laptop,
and later left the room.
```

---

## Proactive Commentary

The system decides whether an event is important enough to comment on.

Example:

```text
EVENT:
Person enters room.

ASSISTANT:
Someone has entered the room.
```

---

# Setup

## Clone Repository

```bash
git clone https://github.com/YOUR_USERNAME/LiveStar-Colab.git
cd LiveStar-Colab
```

---

## Install Dependencies

```bash
pip install openai
pip install opencv-python
pip install pillow
pip install tqdm
```

---

# OpenRouter Configuration

Create an API key from:

https://openrouter.ai

Then set:

```python
OPENROUTER_API_KEY = "YOUR_API_KEY"
```

---

# Supported Models

Vision:

* google/gemini-2.5-flash
* qwen/qwen2.5-vl-7b-instruct

Text:

* google/gemini-2.5-flash
* qwen/qwen3-8b
* qwen/qwen3-4b

---

# Running

1. Upload a video file.
2. Extract frames every few seconds.
3. Generate event descriptions.
4. Build memory nodes.
5. Generate video summary.
6. Produce live assistant commentary.

Outputs:

```text
events.json
livestar_results.json
```

---

# Example Output

```text
EVENT:
A person enters a kitchen.

ASSISTANT:
Someone has entered the kitchen.
```

```text
EVENT:
The person opens a refrigerator.

ASSISTANT:
The person appears to be looking for food.
```

---

# Project Structure

```text
.
├── LiveStar_Colab.ipynb
├── events.json
├── livestar_results.json
├── README.md
└── assets/
```

---

# Limitations

* Not the official LiveStar implementation.
* Uses API-based inference rather than local models.
* TSHM is approximated using memory summaries.
* SVeD is approximated using a lightweight decision prompt.

---

# Future Improvements

* Real-time webcam streaming
* FAISS memory retrieval
* Motion-based frame filtering
* Multi-agent reasoning
* Full LiveStarPro TSHM implementation
* Real-time audio commentary

---

# References

LiveStar

https://github.com/sotayang/LiveStar

LiveStarPro

https://arxiv.org/pdf/2606.17798

---

# License

MIT License
