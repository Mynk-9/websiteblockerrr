# Custom Website Blocker Chrome Extension (MV3)

A premium, high-performance, and visually stunning Chrome Extension that enables regex-based website blocking using Google Chrome's native Manifest V3 APIs.

---

## 🚀 Key Features

*   **Regex Filtering**: Easily block websites matching complex regular expressions.
*   **Frugal Permissions**: Zero host permissions requested (no `<all_urls>` warnings), ensuring maximum privacy and instant trust.
*   **High Performance**: Leverages Chrome's native `declarativeNetRequest` (DNR) C++ engine for near-zero matching latency.
*   **Aesthetic UI**: A beautifully designed dark glassmorphic control dashboard (Popup) and a premium, glowing landing page for blocked requests.
*   **Reliable Redirection**: Seamlessly redirects matching requests to an internal warning landing page, passing the original URL for audit and context.
*   **Production Reliability via TDD**: Backed by a comprehensive Vitest automated test suite with a strict **100% unit test coverage** requirement.

---

## 🧪 Automated Testing & TDD Workflow

This repository enforces **Test-Driven Development (TDD)**. All unit tests must be written and verified in a failing state (Red) before writing any production logic (Green).

### Setup and Dependencies
To install the testing rig (Vitest, JSDOM, and Coverage utilities), run:
```bash
npm install
```

### Running Tests
Execute the automated test suite locally:
```bash
# Run tests once
npm run test

# Run tests in live watch mode (hot reloading)
npm run test:watch
```

### Generating Coverage Reports
To analyze code paths and ensure maximum coverage:
```bash
npm run coverage
```
*Note: A coverage threshold of **100%** (branches, lines, statements, functions) is enforced in `vitest.config.js`. Build verification scripts will reject any code changes that drop below this threshold.*

---

## 🛠️ Tech Stack & Architecture

*   **API Framework**: Chrome Extension Manifest V3
*   **Storage**: `chrome.storage.local` (persistent active rules list)
*   **Matching Engine**: `chrome.declarativeNetRequest` (Dynamic dynamic filters)
*   **UI Layers**: Vanilla HTML5, ES6+ Javascript, Pure CSS3 (custom HSL color palette, micro-animations, and glassmorphism)
*   **Testing Rig**: Vitest, JSDOM environment, and custom Chrome API mocks (`tests/mocks/chrome.mock.js`)

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
