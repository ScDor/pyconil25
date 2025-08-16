# Loguru

write logs to a file with minimal setup

<v-clicks>

````md magic-move
<!-- saved 29 chars, but it's not _that_ amazing -->
```python
import logging

logging.basicConfig(filename="app.log", level=logging.INFO)
logging.info("This is info")
logging.error("This is an error")
```

```python
from loguru import logger

logger.add("app.log")
logger.info("This is info")
logger.error("This is an error")
```
````

</v-clicks>

```
Outcome: Logs written to app.log
```

---

# Loguru: Advanced

multi-sink logs, rotation, and exceptions with minimal setup


<v-clicks>

````md magic-move

```python
import logging
from logging.handlers import TimedRotatingFileHandler

logger = logging.getLogger()
logger.setLevel(logging.INFO)

fmt = logging.Formatter("%(asctime)s | %(levelname)s | %(message)s")

sh = logging.StreamHandler()
sh.setFormatter(fmt)

fh = TimedRotatingFileHandler("app.log", when="midnight", backupCount=7)
fh.setFormatter(fmt)

logger.handlers = [sh, fh]

try:
    raise ValueError("Boom")
except Exception:
    logger.exception("Unhandled error")

logger.info("Hello %s", "world")
```

```python
from loguru import logger
import sys

logger.remove() # remove default stdout logger
logger.add(sys.stderr, level="INFO", format="{time} | {level} | {message}")
logger.add("app.log", rotation="00:00", retention="7 days", encoding="utf-8")

@logger.catch  # auto-captures and logs exceptions with traceback
def main():
    logger.bind(user="alice").info("Hello world")  # structured context
    raise ValueError("Boom")

main()
```
````

</v-clicks>
