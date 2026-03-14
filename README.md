# 🚀 TeleCloud-CDN: Unlimited Media Hosting Engine

[![Portfolio](https://img.shields.io/badge/View-Portfolio-blue?style=for-the-badge)](https://asif-jamali-portfolio.vercel.app/)
[![License](https://img.shields.io/badge/License-Proprietary-red?style=for-the-badge)](https://choosealicense.com/no-permission/)

A high-performance, cost-optimized image and video hosting solution engineered to eliminate storage bottlenecks for **low-spec VPS environments (500MB RAM)** and bypass **regional CDN restrictions**.

---

## 💡 The Problem
In modern web development, hosting media assets on a budget is a major hurdle:
* **Hardware Constraints:** 500MB RAM VPS instances crash during heavy image processing.
* **Storage Limits:** Local SSD storage fills up instantly with high-resolution work history photos.
* **Regional Blocks:** Many free CDNs (like ImgBB or Telegram's direct links) are throttled or blocked in regions like **Pakistan**, leading to broken UI/UX.

## ✅ The Solution: Triple-Tier Architecture
I engineered a system that treats **Telegram** as an infinite "Hard Drive" and **Hugging Face** as a globally accessible "CDN Bridge."

1. **Infinite Storage:** Leverages the Telegram API to store unlimited assets at zero cost.
2. **FastAPI Middleware:** A secure proxy deployed on Hugging Face manages authentication and file retrieval.
3. **Smart Byte-Streaming:** Instead of providing direct links (which expire and are easily blocked), the server **streams image bytes** directly to the user. This ensures assets load 100% of the time without requiring a VPN.

---

## 🌟 Key Features

### 🛠 Architecture & Performance
* **Zero-Footprint Storage:** Assets are stored remotely; your local VPS database only holds tiny metadata strings.
* **RAM-Efficient Streaming:** Uses **Chunked Streaming Responses (8KB chunks)** to handle high-resolution 4K images and videos without spiking server memory.
* **Asynchronous Concurrency:** Built with `FastAPI` to handle hundreds of concurrent admin views simultaneously.

### 🔐 Security & Privacy
* **Source Obfuscation:** Your `BOT_TOKEN` and `CHANNEL_ID` are strictly server-side. The end-user only sees your custom API URL.
* **Hotlink Protection:** Since URLs are proxied through your API, you have full control over who can view your assets.

### 🌍 Accessibility
* **Bypass Regional Firewalls:** Works perfectly in Pakistan and other restricted regions by routing traffic through Hugging Face’s global network.
* **No VPN Required:** Delivers a seamless experience for the end-user.

### 🔄 Full Asset Management (CRUD)
* **Authenticated Uploads:** Securely push images/videos from any local VPS.
* **Bulk Deletion:** Clean up Telegram storage and your local DB in a single sync call.
* **Caption & Media Editing:** Update work history details directly via API without re-uploading.

---

## 🛠️ Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Backend** | Python, FastAPI, Uvicorn |
| **Infrastructure** | Docker, Hugging Face Spaces |
| **Storage API** | Telegram Bot API |
| **Frontend** | React, Vercel |

---

## 🏗️ System Design

```mermaid
graph LR
A[React Frontend] -- API Request --> B[Hugging Face Proxy]
B -- Get Path --> C[Telegram API]
C -- Return File Bytes --> B
B -- Streamed Bytes --> A
