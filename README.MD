# FFMPEG Media Plugin for Unreal Engine

A media player plugin using the FFMPEG library, supporting more formats and alpha videos.

## Features

- Cross-platform: Windows, Linux, Mac
- Hardware accelerated codec support
- Alpha video support
- Internet radio streaming (HTTP/HTTPS)
- Wide format support (MP3, MP4, MKV, AVI, FLAC, OGG, etc.)

## Compatibility

- **Unreal Engine 5.4+** (tested on 5.6)
- Platforms: Win64, Linux, Mac

## Installation

1. Clone or copy this repository to `<YourProject>/Plugins/`
    - Alternatively, copy to `Engine/Plugins/` to make available to all projects
2. Regenerate project files:
    - Right-click `.uproject` → "Generate Visual Studio project files"
    - Or run: `<UE>/Engine/Build/BatchFiles/Build.bat TargetProject Editor Win64 Development <ProjectPath>`
3. Open project, enable plugin in **Edit → Plugins → Media Players**

## Configuration

Add to `Config/DefaultEngine.ini`:

```ini
[/Script/FFMPEGMediaFactory.FFMPEGMediaSettings]
UseInfiniteBuffer=False
AllowFrameDrop=True
UseHardwareAcceleratedCodecs=True
DisableAudio=False
ZeroLatencyStreaming=False
RtspTransport=Default
SpeedUpTricks=False
AudioThreads=1
VideoThreads=1
SyncType=AudioMaster
```

**Important**: `DisableAudio=False` is required for audio-only streaming (radio).

## Usage

### Basic Video Playback

1. Create **Media Source** asset or use URL
2. Create **Media Player** component
3. In Media Player details, set **Player** to `FFMPEGMedia`
4. Use **Media Sound** component for audio
5. Play via Blueprint or C++

### Radio Streaming

```cpp
// C++ Example
UJTZ_RadioComponent* Radio = ...;

// Set desired player
Radio->DesiredPlayerName = TEXT("FFMPEGMedia");

// Play stream
Radio->PlayStream(TEXT("http://radio-server.com/stream.mp3"));
```

### Blueprint

1. Add **Media Player** component to actor
2. Set **Player → Desired Player Name** to `FFMPEGMedia`
3. Use **Open URL** node with stream URL
4. Add **Media Sound** component for audio output

## Supported Formats

- **Audio**: MP3, AAC, FLAC, OGG, WAV, Opus, AC3, DTS
- **Video**: MP4 (H.264/HEVC), MKV, AVI, MOV, WebM, FLV
- **Protocols**: HTTP, HTTPS, HLS (m3u8), RTSP
- **Streaming**: Shoutcast, Icecast, progressive download

## Known Issues

- Audio-only streams require `DisableAudio=False` in config
- Very old FFMPEG builds may not support all codecs
- Hardware acceleration depends on GPU drivers

## License

Original plugin by Giovany Gutiérrez. Modified for UE 5.6 compatibility.

## Links

- [UE Media Framework Docs](https://docs.unrealengine.com/en-US/Engine/MediaFramework/)
- [FFMPEG Documentation](https://ffmpeg.org/documentation.html)
