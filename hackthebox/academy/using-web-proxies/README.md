# 🌐 Using Web Proxies

> Personal notes and practical reference for the **Hack The Box Academy — Using Web Proxies** module.

[![HTB Academy](https://img.shields.io/badge/Hack%20The%20Box-Academy-green)](https://academy.hackthebox.com/)

## 📋 Module Overview

**Difficulty:** Easy
**Tier:** 2
**Estimated Time:** 8 hours
**Sections:** 15
**Interactive Exercises:** 8
**Assessment:** 1

### 🎯 Objective

Build practical knowledge of web proxy frameworks, primarily **Burp Suite** and **OWASP ZAP**, and learn how to intercept, inspect, modify, repeat, fuzz, and scan web traffic.

This repository contains my own notes, procedures, commands, configurations, and lessons learned while completing the module.

## 🗂️ Contents

### 1. Getting Started

* [Intro to Web Proxies](./getting-started/intro-to-web-proxies.md)
* [Setting Up](./getting-started/setting-up.md)

### 2. Web Proxy

* [Proxy Setup](./web-proxy/proxy-setup.md)
* [Intercepting Web Requests](./web-proxy/intercepting-web-requests.md)
* [Intercepting Responses](./web-proxy/intercepting-responses.md)
* [Automatic Modification](./web-proxy/automatic-modification.md)
* [Repeating Requests](./web-proxy/repeating-requests.md)
* [Encoding & Decoding](./web-proxy/encoding-decoding.md)
* [Proxying Tools](./web-proxy/proxying-tools.md)

### 3. Web Fuzzer

* [Burp Intruder](./web-fuzzer/burp-intruder.md)
* [ZAP Fuzzer](./web-fuzzer/zap-fuzzer.md)

### 4. Web Scanner

* [Burp Scanner](./web-scanner/burp-scanner.md)
* [ZAP Scanner](./web-scanner/zap-scanner.md)
* [Extensions](./web-scanner/extensions.md)

### 5. Skills Assessment

* [Assessment Notes](./skills-assessment/README.md)

---

## 🧠 Quick Reference

### Burp Suite

| Task               | Tool                    |
| ------------------ | ----------------------- |
| Intercept requests | Proxy                   |
| Modify requests    | Proxy / Match & Replace |
| Repeat requests    | Repeater                |
| Fuzz parameters    | Intruder                |
| Scan applications  | Scanner                 |
| Encode/decode data | Decoder                 |
| Analyze requests   | HTTP history            |

### OWASP ZAP

| Task               | Tool           |
| ------------------ | -------------- |
| Intercept requests | Breakpoints    |
| Repeat requests    | Request Editor |
| Fuzz parameters    | Fuzzer         |
| Scan applications  | Active Scanner |
| Analyze traffic    | History        |

## 🔗 Resources

* [Hack The Box Academy](https://academy.hackthebox.com/)
* [Burp Suite Documentation](https://portswigger.net/burp/documentation)
* [OWASP ZAP Documentation](https://www.zaproxy.org/docs/)

## 🏆 Completion

**Status:** Completed

**Badge:** [Dive into requests](https://academy.hackthebox.com/achievement/badge/c6b43d4e-b93d-11f1-9524-0affe7dfeb45)

**Completed:** 26 September 2026
