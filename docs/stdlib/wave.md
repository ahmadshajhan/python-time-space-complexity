# wave Module

The `wave` module reads and writes WAV (RIFF) audio files, supporting various sample rates and bit depths.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `open()` | O(1) | O(1) | Open file |
| Read/write | O(n) | O(n) | n = frame count |

## Working with WAV Files

### Reading WAV File

```python
import wave

# Open - O(1)
with wave.open('audio.wav', 'rb') as wav:
    # Get properties
    n_channels = wav.getnchannels()
    sample_width = wav.getsampwidth()
    framerate = wav.getframerate()
    n_frames = wav.getnframes()
    
    # Read frames - O(n)
    frames = wav.readframes(n_frames)
```

### Writing WAV File

```python
import wave

# Create - O(1)
with wave.open('output.wav', 'wb') as wav:
    # Set parameters
    wav.setnchannels(2)      # Stereo
    wav.setsampwidth(2)      # 16-bit
    wav.setframerate(44100)  # 44.1 kHz
    
    # Write frames - O(n)
    wav.writeframes(audio_data)
```

## Related Documentation

- [aifc Module](aifc.md)
- [sunau Module](sunau.md)
