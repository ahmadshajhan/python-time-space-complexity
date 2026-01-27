# ftplib Module

The `ftplib` module implements FTP client functionality for transferring files to and from FTP servers.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `connect()` | O(1) | O(1) | TCP connection |
| List files | O(n) | O(n) | n = files |
| Transfer | O(n) | O(n) | n = file size |
| `FTP()` | O(1) | O(1) | Create client (optional connect) |
| `FTP_TLS()` | O(1) | O(1) | Create FTPS client |
| `parse227()` | O(1) | O(1) | Parse PASV reply |
| `parse229()` | O(1) | O(1) | Parse EPSV reply |
| `parse257()` | O(n) | O(1) | Parse PWD reply |

## Connecting and Transferring Files

### Basic FTP Operations

```python
from ftplib import FTP

# Connect - O(1)
ftp = FTP('ftp.example.com')
ftp.login('user', 'password')

# List files - O(n)
files = ftp.nlst()
print(files)

# Download file - O(n)
with open('local.txt', 'wb') as f:
    ftp.retrbinary('RETR remote.txt', f.write)

# Upload file - O(n)
with open('local.txt', 'rb') as f:
    ftp.storbinary('STOR remote.txt', f)

# Disconnect - O(1)
ftp.quit()
```

## Related Documentation

- [socket Module](socket.md)
- [smtplib Module](smtplib.md)
