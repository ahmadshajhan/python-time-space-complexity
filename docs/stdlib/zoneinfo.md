# zoneinfo Module

The `zoneinfo` module provides IANA time zone support for accurate timezone handling, including daylight saving time.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `ZoneInfo()` | O(1) | O(n) | Load timezone data |
| Localize datetime | O(1) | O(1) | Apply timezone |

## Working with Time Zones

### Using Timezones

```python
from zoneinfo import ZoneInfo
from datetime import datetime

# Create timezone - O(1)
est = ZoneInfo("America/New_York")
pst = ZoneInfo("America/Los_Angeles")

# Create datetime with timezone - O(1)
dt = datetime(2024, 1, 15, 12, 0, tzinfo=est)
print(dt)  # 2024-01-15 12:00:00-05:00

# Convert timezone - O(1)
dt_pst = dt.astimezone(pst)
print(dt_pst)  # 2024-01-15 09:00:00-08:00

# Get timezone name - O(1)
print(dt.tzname())  # EST
```

## Related Documentation

- [datetime Module](datetime.md)
- [pytz Library](https://pypi.org/project/pytz/)
