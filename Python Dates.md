# Python Dates

Working with dates and times in Python.

## datetime Module

```python
import datetime

# Current date and time
now = datetime.datetime.now()
print(now)  # 2026-01-06 12:30:45.123456

# Current date
today = datetime.date.today()
print(today)  # 2026-01-06

# Create specific date
date = datetime.date(2026, 1, 6)
time = datetime.time(14, 30, 0)
dt = datetime.datetime(2026, 1, 6, 14, 30, 0)
```

## Format Dates

```python
import datetime

now = datetime.datetime.now()

# Format date
print(now.strftime("%Y-%m-%d"))  # 2026-01-06
print(now.strftime("%B %d, %Y"))  # January 06, 2026
print(now.strftime("%A"))  # Monday

# Common format codes:
# %Y - Year (4 digits)
# %m - Month (01-12)
# %d - Day (01-31)
# %H - Hour (00-23)
# %M - Minute (00-59)
# %S - Second (00-59)
# %A - Weekday full name
# %B - Month full name
```

## Parse Dates

```python
from datetime import datetime

date_string = "2026-01-06"
date = datetime.strptime(date_string, "%Y-%m-%d")
```

## Date Arithmetic

```python
from datetime import datetime, timedelta

now = datetime.now()

# Add days
future = now + timedelta(days=7)

# Subtract days
past = now - timedelta(days=7)

# Difference between dates
diff = future - past
print(diff.days)  # 14
```

---

**Related:** [[Python]] | [[Python Strings]] | [[Python String Formatting]]
