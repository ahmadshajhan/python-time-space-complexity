# mailbox Module

The `mailbox` module provides classes for reading, writing, and manipulating various mailbox formats (mbox, Maildir, MMDF, etc.).

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Open mailbox | O(n) | O(n) | n = messages |
| Add message | O(1) amortized | O(1) | Append operation |
| Iterate messages | O(n) | O(1) | Sequential access |

## Working with Mailboxes

### Reading Mailbox

```python
import mailbox

# Open mbox - O(n)
mbox = mailbox.mbox('mail.mbox')

# Iterate - O(n)
for key, message in mbox.items():
    print(message['Subject'])
    print(message.get_payload())

mbox.close()
```

### Adding Messages

```python
import mailbox
from email.message import EmailMessage

# Open - O(n)
mbox = mailbox.mbox('mail.mbox')

# Create message - O(1)
msg = EmailMessage()
msg['Subject'] = 'Test'
msg.set_content('Hello')

# Add - O(1)
key = mbox.add(msg)

# Flush to disk - O(n)
mbox.flush()
mbox.close()
```

## Related Documentation

- [email Module](email.md)
- [smtplib Module](smtplib.md)
