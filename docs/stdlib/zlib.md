# zlib Module Complexity

The `zlib` module provides low-level compression and decompression functions using the DEFLATE algorithm (same as gzip but without headers).

## Functions & Methods

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `zlib.compress(data)` | O(n log n) | O(n) | Compress bytes, n = input size |
| `zlib.decompress(data)` | O(m) | O(m) | Decompress bytes, m = uncompressed size |
| `zlib.compressobj()` | O(1) | O(1) | Create compressor object |
| `Compress.compress(data)` | O(n) | O(k) | Add data to compress, k = buffer |
| `Compress.flush()` | O(k) | O(k) | Finalize compression |
| `Decompress.decompress(data)` | O(m) | O(k) | Decompress data |

## Compression Functions

### compress() - One-shot Compression

```python
import zlib

# Compress entire data: O(n log n) time, O(n) space
data = b'Large data...' * 10000
compressed = zlib.compress(data)  # O(n log n)

# Space: creates entire compressed result
# O(n) for output (typically 30-50% of input)

# With compression level
compressed = zlib.compress(data, level=6)  # O(n log n)
compressed = zlib.compress(data, level=9)  # O(n log^2 n)
```

### decompress() - One-shot Decompression

```python
import zlib

# Decompress entire data: O(m) time, O(m) space
# m = uncompressed size
compressed = b'x\x9c...'  # DEFLATE data
data = zlib.decompress(compressed)  # O(m)

# Space: creates entire decompressed result
# O(m) for output
```

## Streaming Compression

### Compressobj - Streaming Compression

```python
import zlib

# Create compressor: O(1)
compressor = zlib.compressobj()  # O(1)

# Add data to compress: O(n) total for all data
result = b''
for chunk in data_chunks:  # O(n) iterations
    result += compressor.compress(chunk)  # O(n log n) total

# Finalize: O(k)
result += compressor.flush()  # O(k) for remaining

# Total: O(n log n) time, O(k) memory
```

### Space Complexity: O(k)

```python
import zlib

# Streaming with small buffer
compressor = zlib.compressobj()

result = b''
for chunk in huge_data_chunks:
    # compress() returns partial output
    result += compressor.compress(chunk)  # O(k) memory, not O(n)
    
    # Optional: flush periodically for incremental output
    result += compressor.flush(zlib.Z_SYNC_FLUSH)  # Incremental flush

result += compressor.flush()  # Final flush
```

## Streaming Decompression

### Decompressobj - Streaming Decompression

```python
import zlib

# Create decompressor: O(1)
decompressor = zlib.decompressobj()  # O(1)

# Add compressed data: O(m) total
result = b''
for chunk in compressed_chunks:
    result += decompressor.decompress(chunk)  # O(m) total

# Total: O(m) time, O(k) memory
```

### Space Complexity: O(k)

```python
import zlib

# Streaming with small buffer
decompressor = zlib.decompressobj()

result = b''
for chunk in compressed_chunks:
    # decompress() returns partial output
    result += decompressor.decompress(chunk)  # O(k) memory

# Total: O(m) time, O(k) memory (k = buffer size)
```

## Compression Levels

### Effect on Performance

```python
import zlib

data = b'x' * 1000000

# Level 0: No compression (STORED)
# Time: O(n), fastest
compressed = zlib.compress(data, level=0)  # Fastest, largest

# Level 1-3: Fast compression
# Time: O(n log n)
compressed = zlib.compress(data, level=1)  # Fast

# Level 6: Default, balanced
# Time: O(n log n)
compressed = zlib.compress(data, level=6)  # Balanced

# Level 9: Maximum compression
# Time: O(n log^2 n), slowest
compressed = zlib.compress(data, level=9)  # Slowest, smallest
```

### Trade-offs

```python
import zlib

data = large_data

# Speed critical: level 1
compressed = zlib.compress(data, level=1)  # Fastest

# Balanced: level 6 (default)
compressed = zlib.compress(data)  # Default balance

# Storage critical: level 9
compressed = zlib.compress(data, level=9)  # Best ratio
```

## Common Patterns

### Basic Compression/Decompression

```python
import zlib

# Compress: O(n log n)
data = b'Hello, World!' * 1000
compressed = zlib.compress(data)  # O(n log n)

# Decompress: O(m)
decompressed = zlib.decompress(compressed)  # O(m)

# Verify
assert data == decompressed
```

### Streaming Large File Compression

```python
import zlib

def compress_file(input_path, output_path):
    """Compress file with streaming."""
    compressor = zlib.compressobj()
    
    with open(input_path, 'rb') as f_in:
        with open(output_path, 'wb') as f_out:
            while True:
                chunk = f_in.read(65536)  # 64KB chunks
                if not chunk:
                    break
                
                # Compress: O(n log n) total
                compressed = compressor.compress(chunk)
                if compressed:
                    f_out.write(compressed)
            
            # Final flush: O(k)
            f_out.write(compressor.flush())
    
    # Total: O(n log n) time, O(k) memory
```

### Streaming Large File Decompression

```python
import zlib

def decompress_file(input_path, output_path):
    """Decompress file with streaming."""
    decompressor = zlib.decompressobj()
    
    with open(input_path, 'rb') as f_in:
        with open(output_path, 'wb') as f_out:
            while True:
                chunk = f_in.read(65536)  # 64KB chunks
                if not chunk:
                    break
                
                # Decompress: O(m) total
                decompressed = decompressor.decompress(chunk)
                if decompressed:
                    f_out.write(decompressed)
    
    # Total: O(m) time, O(k) memory
```

### Incremental Compression

```python
import zlib

# Create compressor
compressor = zlib.compressobj(level=6)

# Add data incrementally
compressed_parts = []

data1 = b'Part 1' * 10000
compressed_parts.append(compressor.compress(data1))

data2 = b'Part 2' * 10000
compressed_parts.append(compressor.compress(data2))

# Finalize
compressed_parts.append(compressor.flush())

# Combine results
final_compressed = b''.join(compressed_parts)

# Time: O(n log n) total
# Space: O(k) during processing
```

## Advanced Options

### Compression Parameters

```python
import zlib

# Method parameter (usually not changed)
compressor = zlib.compressobj(
    level=6,  # Compression level 0-9
    method=zlib.DEFLATED,  # Compression method
    wbits=15,  # Window size (15 = 32KB window)
    memLevel=8  # Memory level for compression
)

# wbits affects compression ratio and memory:
# 15 (default): 32KB window, good compression
# 9: 512 byte window, less compression, less memory
```

### Incremental Flushing

```python
import zlib

compressor = zlib.compressobj()

# Z_NO_FLUSH: Default, maximum compression
# Wait until buffer full to output
result = compressor.compress(data)  # May return empty

# Z_SYNC_FLUSH: Output partial result
# Allows decompressor to decode up to this point
result += compressor.flush(zlib.Z_SYNC_FLUSH)  # Incremental

# Z_FULL_FLUSH: Maximum sync point
result += compressor.flush(zlib.Z_FULL_FLUSH)

# Z_FINISH: Final flush
result += compressor.flush(zlib.Z_FINISH)
```

## Decompression Limits

### Preventing Decompression Bombs

```python
import zlib

# Malicious data can expand massively during decompression
# Example: highly compressible data can expand 1000x+

# Safe decompression with size limit
def safe_decompress(compressed, max_size=10*1024*1024):
    """Decompress with size limit to prevent DoS."""
    decompressor = zlib.decompressobj()
    
    try:
        result = b''
        while True:
            # Decompress in chunks
            decompressed = decompressor.decompress(
                compressed[len(result):],
                max_size - len(result)  # Limit output
            )
            result += decompressed
            
            if len(result) > max_size:
                raise ValueError(f"Decompressed size exceeds {max_size}")
            
            if not decompressed:
                break
        
        return result
    except zlib.error as e:
        raise ValueError(f"Decompression error: {e}")
```

## Performance Characteristics

### Best Practices

```python
import zlib

# Good: Use streaming for large data
compressor = zlib.compressobj()
for chunk in data_chunks:
    compressed += compressor.compress(chunk)  # O(k) memory
compressed += compressor.flush()

# Avoid: Compress entire large data at once
compressed = zlib.compress(huge_data)  # O(n) memory

# Good: Use appropriate compression level
# Default (6) is usually best balance
compressed = zlib.compress(data)

# Avoid: Using level 9 for real-time compression
# 9 is much slower and rarely worth it
compressed = zlib.compress(data, level=9)  # Very slow

# Good: Check decompressed size before processing
decompressor = zlib.decompressobj()
result = b''
for chunk in chunks:
    result += decompressor.decompress(chunk)
    if len(result) > MAX_SIZE:
        raise ValueError("Data too large")
```

### Compression Level Selection

```python
import zlib

data = sample_data

# Real-time/streaming: level 1-3
# Fast compression, reasonable ratio
compressed = zlib.compress(data, level=3)

# Default/balanced: level 6 (default)
# Good balance of speed and compression
compressed = zlib.compress(data)

# Archival/storage: level 9
# Best compression, slow, rarely needed
# Usually not worth the slowness for zlib
compressed = zlib.compress(data, level=9)
```

## Version Notes

- **Python 2.0+**: Basic zlib support
- **Python 3.0+**: Enhanced API
- **Python 3.3+**: Better compression control
- **Python 3.10+**: Improved performance

## Differences from gzip

```python
import zlib
import gzip

# DEFLATE (zlib):
# - Raw DEFLATE data
# - No headers/metadata
# - Slightly smaller than gzip

# GZIP:
# - DEFLATE with headers
# - Includes filename, timestamp, etc.
# - Adds 10-18 bytes overhead
# - More portable

# Both use same compression algorithm
# zlib is more low-level and efficient
# gzip is better for files and interoperability
```

## Related Documentation

- [gzip Module](gzip.md) - GZIP compression (higher level)
- [bz2 Module](bz2.md) - BZIP2 compression
- [lzma Module](lzma.md) - XZ compression (better ratio)
- [zipfile Module](zipfile.md) - ZIP archive handling (uses zlib)
- [io Module](io.md) - I/O operations
