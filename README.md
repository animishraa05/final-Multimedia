# Final Project: Consolidated Multimedia Analyzer

This is the final consolidated project that accepts any multimedia file (Image, Audio, Video), automatically identifies its type, analyzes it using the appropriate module, and generates a structured JSON report.

## Project Structure
- `main.py`: Entry point for the application.
- `file_utils.py`: Contains utilities for file validation, size extraction, and type identification.
- `image_analyzer.py`: Module for analyzing images.
- `audio_analyzer.py`: Module for analyzing audio files.
- `video_analyzer.py`: Module for analyzing video files.
- `report_generator.py`: Module for exporting the analysis results to a JSON report.
- `samples/`: Directory for sample media files.
- `reports/`: Output directory for generated reports.

## Usage
```bash
python main.py <path_to_media_file>
```

## Requirements
- Python 3
- Pillow (`pip install Pillow`)
- Mutagen (`pip install mutagen`)
- FFmpeg/ffprobe installed on the system

## System Architecture / Use Case
```mermaid
flowchart TD
    User([User])
    
    subgraph CMA [Consolidated Multimedia Analyzer System]
        Validate([Validate File & Size])
        Identify([Identify File Type])
        
        ImgAnalyzer([Image Analysis Module])
        AudAnalyzer([Audio Analysis Module])
        VidAnalyzer([Video Analysis Module])
        
        ReportGen([JSON Report Generator])
    end
    
    User -->|Input Media File| Validate
    Validate --> Identify
    
    Identify -->|If Image| ImgAnalyzer
    Identify -->|If Audio| AudAnalyzer
    Identify -->|If Video| VidAnalyzer
    
    ImgAnalyzer --> ReportGen
    AudAnalyzer --> ReportGen
    VidAnalyzer --> ReportGen
    
    ReportGen -->|Save report.json| User
```

## Sample Consolidated Report (JSON)
```json
{
    "File Type Identified": "VIDEO",
    "File Name": "proper_video.mp4",
    "File Size": "0.75 MB",
    "Container": "QuickTime / MOV",
    "Duration": "10.03 seconds",
    "Video": {
        "Resolution": "320x176",
        "Frame Rate": "25/1",
        "Bit Rate": "300 kbps",
        "Codec": "h264"
    },
    "Audio": {
        "Codec": "aac",
        "Channels": "2",
        "Sampling Rate": "48000 Hz",
        "Bit Rate": "160 kbps"
    },
    "Metadata": {
        "major_brand": "mp42",
        "minor_version": "0",
        "compatible_brands": "mp42isomavc1",
        "creation_time": "2012-03-13T08:58:06.000000Z",
        "encoder": "HandBrake 0.9.6 2012022800"
    }
}```
