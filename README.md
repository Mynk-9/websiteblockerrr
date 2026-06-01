# Custom Website Blocker Chrome Extension (MV3)

A premium, high-performance, and visually stunning Chrome Extension that enables regex-based website blocking using Google Chrome's native Manifest V3 APIs.

---

## 🚀 Key Features

*   **Regex Filtering**: Easily block websites matching complex regular expressions.
*   **Frugal Permissions**: Zero host permissions requested (no `<all_urls>` warnings), ensuring maximum privacy and instant trust.
*   **High Performance**: Leverages Chrome's native `declarativeNetRequest` (DNR) C++ engine for near-zero matching latency.
*   **Aesthetic UI**: A beautifully designed dark glassmorphic control dashboard (Popup) and a premium, glowing landing page for blocked requests.
*   **Reliable Redirection**: Seamlessly redirects matching requests to an internal warning landing page, passing the original URL for audit and context.

---

## 🛠️ Tech Stack & Architecture

*   **API Framework**: Chrome Extension Manifest V3
*   **Storage**: `chrome.storage.local` (persistent active rules list)
*   **Matching Engine**: `chrome.declarativeNetRequest` (Dynamic dynamic filters)
*   **UI Layers**: Vanilla HTML5, ES6+ Javascript, Pure CSS3 (custom HSL color palette, micro-animations, and glassmorphism)

---

## 📥 Local Installation Guide

Since the extension runs locally in Developer Mode, follow these steps to load it into Chrome once the implementation phase begins:

1.  Open Google Chrome and navigate to `chrome://extensions/`.
2.  Enable **Developer Mode** by toggling the switch in the top-right corner.
3.  Click the **Load unpacked** button in the top-left.
4.  Select the `src/` directory within this repository.
5.  Pin the extension from your toolbar and open the popup to begin managing blocked sites!

---

## 📖 Mandatory Documentation Rules

To ensure seamless coordination between humans and AI agents working on this project:

1.  **AI Instructions**: This repository uses standard instructions. All AI tools **MUST** read [LIVE_DOCUMENTATION.md](file:///Users/mayankmathur/projects/personal/websiteblockerrr/LIVE_DOCUMENTATION.md) at the beginning of each session.
2.  **Updating the Documentation**:
    *   Whenever you introduce changes to files, add features, or change configuration options, you **MUST** update [LIVE_DOCUMENTATION.md](file:///Users/mayankmathur/projects/personal/websiteblockerrr/LIVE_DOCUMENTATION.md) immediately.
    *   Ensure that the implementation status table and active directory tree in [LIVE_DOCUMENTATION.md](file:///Users/mayankmathur/projects/personal/websiteblockerrr/LIVE_DOCUMENTATION.md) match the absolute current state of the filesystem.
    *   Update this `README.md` if core installation steps, features, or architectural specifications change. Keep the documentation synchronized.
