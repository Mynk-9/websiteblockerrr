# LIVE DOCUMENTATION: Website Blocker Extension

> [!IMPORTANT]
> **ATTENTION ALL AI CODING AGENTS & DEVELOPERS:**
> This is a living documentation file. You **MUST** read this file in full before executing any command or writing any code in this repository.
> When completing a task, you **MUST** update this file to reflect the exact new state of the repository. Do not make this a historical changelog; keep it as a clean, current snapshot of the codebase.

---

## 1. Repository Status & Current Phase

*   **Current Phase**: `PLANNING PHASE`
*   **Active Sprint**: Phase 1 (Core Infrastructure & Architectural Design)
*   **Current State**: 
    *   No production source code files have been written.
    *   Architecture is fully planned (DNR-based, zero host permissions, dark glassmorphic styling).
    *   Plan is stored in `ORIGINAL_PLAN.md`.
    *   Ready for next developer or AI agent to begin implementation.

---

## 2. Core Architecture Snapshot

The extension is designed around a zero-permission/frugal-permission model in Chrome Manifest V3:

*   **Rule Engine**: Native `chrome.declarativeNetRequest` (DNR) dynamically updated via background service worker.
*   **Storage**: `chrome.storage.local` holds rules metadata (`id`, `pattern`, `createdAt`) and the global `enabled` toggle.
*   **Frugal Redirect Model**: Redirects to `/pages/blocked.html` are handled via `declarativeNetRequest` using `regexSubstitution` (appending `?url=\\0` to pass the blocked URL without requiring host permissions).
*   **Design System**: Pure HSL CSS, Cyberpunk Dark Slate base with vibrant Neon Orange-Red glow accents and Outfit/Inter typography.

---

## 3. Directory & File Blueprint

This tree maps the active files in the workspace. Files marked as `[PLANNED]` have not yet been created but represent the approved target architecture.

```
websiteblockerrr/
├── .cursorrules           <-- AI agent directives (Forces loading of LIVE_DOCUMENTATION.md)
├── .instructions.md       <-- Root-level workspace developer rules
├── ORIGINAL_PLAN.md       <-- Detailed project plan & technology choice (Static)
├── LIVE_DOCUMENTATION.md  <-- THIS FILE (Latest snapshot of codebase, keeps updating)
├── README.md              <-- General project overview & setup instructions
├── LICENSE
├── .gitignore
└── src/ [PLANNED]
    ├── manifest.json      [PLANNED] <-- Manifest V3 extension configuration
    ├── background/        [PLANNED]
    │   └── service_worker.js [PLANNED] <-- Dynamic DNR rules controller and storage syncing
    ├── popup/             [PLANNED]
    │   ├── popup.html     [PLANNED] <-- Sleek management dashboard interface
    │   ├── popup.css      [PLANNED] <-- Dynamic dark-mode glassmorphic styling
    │   └── popup.js       [PLANNED] <-- Regex validation and storage updating
    └── pages/             [PLANNED]
        ├── blocked.html   [PLANNED] <-- Radial-glow warning landing page
        ├── blocked.css    [PLANNED] <-- Sleek animations and styling for warning page
        └── blocked.js     [PLANNED] <-- Dynamic URL parsing and UI rendering
```

---

## 4. Implementation Status Tracker

| Feature / Step | Status | Target File(s) | Description |
| :--- | :--- | :--- | :--- |
| **Phase 1: Configs** | `NOT STARTED` | `src/manifest.json` | Manifest V3 setup, storage and DNR permissions. |
| **Phase 2: CSS styling**| `NOT STARTED` | `src/popup/popup.css`, `src/pages/blocked.css` | Premium HSL variables, fluid animations & styles. |
| **Phase 3: Service Worker**| `NOT STARTED` | `src/background/service_worker.js` | DNR Dynamic rules synchronizer, startup sync. |
| **Phase 4: Popup Controller**| `NOT STARTED`| `src/popup/popup.js`, `popup.html` | UI management, native `isRegexSupported` check. |
| **Phase 5: Landing Page** | `NOT STARTED` | `src/pages/blocked.js`, `blocked.html` | Parameter parsing, displaying matched pattern/URL. |

---

## 5. Rules for Keeping This Document Updated

To maintain documentation integrity, every developer or AI tool modifying this repository **MUST** adhere to the following rules:

1.  **Read First**: Always read `LIVE_DOCUMENTATION.md` at the start of your workspace session.
2.  **No Changelogs**: Do **NOT** turn this document into a changelog of what you did. Instead, modify the existing sections (e.g. updating the "Repository Status", changing `[PLANNED]` files to `[ACTIVE]`, or updating the "Status Tracker") to represent the exact current layout.
3.  **Update Promptly**: Perform modifications to this file at the end of every feature implementation or file change before declaring your task complete.
4.  **Consistency**: Keep the structure consistent. Maintain the HSL design variables, table format, and blueprints intact.
