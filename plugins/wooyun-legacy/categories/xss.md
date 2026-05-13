# XSS Vulnerability Analysis

> Automatically extracted on 2026-01-23 18:57
> Sample count: 9


> Total case count: 9

## High-Frequency Parameters
```
  photourl: 1 occurrence
  w: 1 occurrence
  kwd: 1 occurrence
  sohuurl: 1 occurrence
```


## Representative Case Titles

- Anhui Wanjia Hotline vulnerability bundle
  Vulnerability type: XSS cross-site scripting attack
- Sogou stored XSS plus CSRF
  Vulnerability type: XSS cross-site scripting attack
- Cross-site scripting vulnerability on a subsite of a certain portal
  Vulnerability type: XSS cross-site scripting attack
- Stored XSS on the main site of a certain classified-information website; yes, the main site
  Vulnerability type: XSS cross-site scripting attack
- Stored cross-site scripting issue in ITPUB blog posting can phish many cookies and has reached the official admin
  Vulnerability type: XSS cross-site scripting attack
- Another stored XSS at Moxian Technology
  Vulnerability type: XSS cross-site scripting attack
- XSS in article comments on CCW.com
  Vulnerability type: XSS cross-site scripting attack
- Fantong.com XSS successfully hijacks an administrator and can enter the backend
  Vulnerability type: XSS cross-site scripting attack
- XSS cross-site attack on Jiuxian.com's official site can obtain more than 1.6 million order records online and get the backend address
  Vulnerability type: XSS cross-site scripting attack

## High-Frequency Payload Patterns
```
<script>alert(/xss/);</script>photourl filtering is too loose, allowing direct insertion of cross-site scripting code
```
