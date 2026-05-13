# CSRF Vulnerability Analysis

> Automatically extracted on 2026-01-23 18:57
> Sample count: 3


> Total case count: 3

## High-Frequency Parameters
```
  url: 1 occurrence
  desc: 1 occurrence
  callback: 1 occurrence
  get_recent_photos: 1 occurrence
  _: 1 occurrence
```


## Representative Case Titles

- Multiple CSRF issues on Gewara Lifestyle Network can inflate followers and post movie reviews and replies
  Vulnerability type: CSRF
- CSRF in a certain album service saves images
  Vulnerability type: CSRF
- CSRF on Jiapin.com allows login as arbitrary users
  Vulnerability type: CSRF

## High-Frequency Payload Patterns
```
orm action="https://example.com/[redacted]
```
