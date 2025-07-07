# Forcing Python to send logs directly to stdout using PYTHONUNBUFFERED
## tl;dr
Set PYTHONUNBUFFERED=1 so Python prints logs immediately instead of buffering them.

## Description
Today I needed my Python script’s logs to appear instantly in my container logs while running in Docker. By default, Python buffers output to stdout and stderr, so print statements or logging output may not show up right away. This can make debugging in containers or CI pipelines tricky, because you can’t see logs in real time.

The fix is super simple: set the environment variable PYTHONUNBUFFERED to 1.

```sh
PYTHONUNBUFFERED=1
python my_script.py
```
Alternatively, you can use the -u flag:
```sh
python -u my_script.py
```
Now all logs are flushed directly to stdout as they happen — no more waiting for buffers to flush!

Just set PYTHONUNBUFFERED=1 and you’re done. 😊
