# 🎬 OpenClaw Skill: cutmv Video Tool

A video processing skill for OpenClaw that leverages FFmpeg to perform video/audio cutting, format conversion, and compression.

## Features

- ✂️ **Video Cutting** - Split video/audio by time range
- 🔄 **Format Conversion** - Convert between video/audio formats
- 🗜️ **Video Compression** - Compress videos with quality control
- 🖼️ **Frame Extraction** - Extract frames from videos
- 🎵 **Audio Extraction** - Extract audio from video
- 🔊 **Audio Replacement** - Replace or mix audio tracks
- 📝 **Text Watermark** - Add text watermark to video (requires freetype)
- 💬 **Subtitle** - Add subtitle files (.srt, .ass)

## Requirements

- FFmpeg installed on your system
- Python 3.7+

## Installation

### 1. Install FFmpeg

**macOS:**
```bash
brew install ffmpeg
```

**Ubuntu/Debian:**
```bash
sudo apt install ffmpeg
```

**Windows:**
Download from [ffmpeg.org](https://ffmpeg.org/download.html) or use Winget:
```bash
winget install ffmpeg
```

### 2. Install the Skill

This skill can be loaded directly from the workspace. Place the skill files in your OpenClaw workspace:

```
~/openclaw-workspace/skills/cutmv-video-tool/
├── SKILL.md
├── skill.py
└── README.md
```

## Usage

### Video Cutting

```python
from skill import VideoTool

tool = VideoTool()
# Cut video from 0 to 480 seconds
tool.cut(input_file="input.mp4", output_file="output.mp4", start_time=0, end_time=480)
```

### Format Conversion

```python
# Convert video format
tool.convert(input_file="input.mp4", output_file="output.avi", output_format="avi")

# Convert audio format  
tool.convert(input_file="input.mp4", output_file="output.mp3", output_format="mp3")
```

### Video Compression

```python
# Compress video with target bitrate
tool.compress(input_file="input.mp4", output_file="compressed.mp4", bitrate="1000k")
```

### Frame Extraction

```python
# Extract a single frame at specific time
tool.extract_frame(input_file="input.mp4", output_file="frame.jpg", timestamp="00:01:30")

# Extract multiple frames (one per second)
tool.extract_frames(input_file="input.mp4", output_dir="./frames/")
```

## API Reference

### VideoTool Class

#### `cut(input_file, output_file, start_time, end_time)`
Cut a video/audio file by time range.

**Parameters:**
- `input_file` (str): Input file path
- `output_file` (str): Output file path
- `start_time` (int/float): Start time in seconds
- `end_time` (int/float): End time in seconds

#### `convert(input_file, output_file, output_format)`
Convert video/audio to different format.

**Parameters:**
- `input_file` (str): Input file path
- `output_file` (str): Output file path
- `output_format` (str): Target format (mp4, avi, mp3, wav, etc.)

#### `compress(input_file, output_file, bitrate)`
Compress video with specified bitrate.

**Parameters:**
- `input_file` (str): Input file path
- `output_file` (str): Output file path
- `bitrate` (str): Target bitrate (e.g., "1000k", "1M")

#### `extract_frame(input_file, output_file, timestamp)`
Extract a single frame from video.

**Parameters:**
- `input_file` (str): Input video path
- `output_file` (str): Output image path
- `timestamp` (str): Time position (HH:MM:SS)

#### `extract_frames(input_file, output_dir, interval=1)`
Extract multiple frames from video.

**Parameters:**
- `input_file` (str): Input video path
- `output_dir` (str): Output directory for frames
- `interval` (int): Interval between frames in seconds

## Integration with OpenClaw

This skill can be used in OpenClaw workflows:

```python
# In your OpenClaw skill
from skill import VideoTool

def process_video(video_path):
    tool = VideoTool()
    # Compress for sending via messaging apps
    tool.compress(video_path, "compressed.mp4", "1000k")
    return "compressed.mp4"
```

## Examples

### Example 1: Compress Video for WeChat/Lark

```python
from skill import VideoTool

def compress_for_messaging(input_path):
    tool = VideoTool()
    # Compress to 15MB for compatibility
    tool.compress(input_path, "output.mp4", "1000k")
    return "output.mp4"
```

### Example 2: Extract Screenshots

```python
from skill import VideoTool

def create_video_grid(video_path):
    tool = VideoTool()
    # Extract frames every 10 seconds
    tool.extract_frames(video_path, "./frames/", interval=10)
    return "./frames/"
```

## Troubleshooting

### "ffmpeg not found"

Make sure FFmpeg is installed and available in your system PATH.

```bash
# Verify installation
ffmpeg -version
```

### "Permission denied"

Ensure you have read/write permissions for input/output directories.

## License

MIT License - See [LICENSE](LICENSE) for details.

## Author

- **Isaac** - [GitHub](https://github.com/QiaoTuCodes)

## Acknowledgments

- Thanks to the [OpenClaw](https://github.com/openclaw/openclaw) team for the amazing platform
- FFmpeg team for the powerful media processing tools

---

*This skill is part of the OpenClaw Skills Collection.*
