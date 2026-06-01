# LIVE DOCUMENTATION: Website Blocker Extension

> [!IMPORTANT]
> **ATTENTION ALL AI CODING AGENTS & DEVELOPERS:**
> This is a living documentation file. You **MUST** read this file in full before executing any command or writing any code in this repository.
> When completing a task, you **MUST** update this file to reflect the exact new state of the repository. Do not make this a historical changelog; keep it as a clean, current snapshot of the codebase.

---

## 1. Repository Status & Current Phase

*   **Current Phase**: `PLANNING PHASE`
*   **Active Sprint**: Phase 1 (TDD Setup & Core Infrastructure Plan)
*   **Current State**: 
    *   No production source code or unit test files have been written.
    *   Architecture is fully planned (DNR-based, zero host permissions, dark glassmorphic styling).
    *   Rigorous Test-Driven Development (TDD) workflow is established using **Vitest** + **JSDOM** mock environment targeting **100% unit test coverage**.
    *   Blueprint and specs are stored in `ORIGINAL_PLAN.md`.
    *   Ready for next developer or AI agent to begin setting up test rigs and writing unit tests first.

---

## 2. Core Architecture Snapshot

The extension is designed around a zero-permission/frugal-permission model in Chrome Manifest V3:

*   **Rule Engine**: Native `chrome.declarativeNetRequest` (DNR) dynamically updated via background service worker.
*   **Storage**: `chrome.storage.local` holds rules metadata (`id`, `pattern`, `createdAt`) and the global `enabled` toggle.
*   **Frugal Redirect Model**: Redirects to `/pages/blocked.html` are handled via `declarativeNetRequest` using `regexSubstitution` (appending `?url=\\0` to pass the blocked URL without requiring host permissions).
*   **Design System**: Pure HSL CSS, Cyberpunk Dark Slate base with vibrant Neon Orange-Red glow accents and Outfit/Inter typography.
*   **Testing Rig**:
    *   *Runner*: Vitest with JSDOM environment for browser API emulation.
    *   *Mock Infrastructure*: Custom Chrome API mock (`tests/mocks/chrome.mock.js`) to simulate storage, runtime, and declarativeNetRequest operations.
    *   *Coverage Goal*: Strict 100% coverage threshold enforced for all production logic.
    *   *Methodology*: Strict Test-Driven Development (TDD) — all component tests MUST be written and run to verify failure BEFORE writing implementation.

---

## 3. Directory & File Blueprint

This tree maps the active files in the workspace. Files marked as `[PLANNED]` have not yet been created but represent the approved target architecture.

```
websiteblockerrr/
├── .cursorrules           <-- AI agent directives (Forces loading of LIVE_DOCUMENTATION.md)
├── .instructions.md       <-- Root-level workspace developer rules
├── ORIGINAL_PLAN.md       <-- Detailed project plan, testing specifications, and mock blueprints (Static)
├── LIVE_DOCUMENTATION.md  <-- THIS FILE (Latest snapshot of codebase, keeps updating)
├── README.md              <-- General project overview, TDD setup, and install instructions
├── LICENSE
├── .gitignore
├── package.json           [PLANNED] <-- Project packages, Vitest dependency and testing scripts
├── vitest.config.js       [PLANNED] <-- Vitest environment configurations & coverage thresholds (100%)
├── tests/                 [PLANNED] <-- ALL testing code is placed here
│   ├── mocks/
│   │   └── chrome.mock.js [PLANNED] <-- V8-based simulation of Chrome Extension MV3 APIs
│   ├── background.test.js [PLANNED] <-- Unit tests for service_worker.js
│   ├── popup.test.js      [PLANNED] <-- DOM/logic unit tests for popup.js (using JSDOM)
│   └── blocked.test.js    [PLANNED] <-- DOM/logic unit tests for blocked.js (using JSDOM)
└── src/                   [PLANNED] <-- Production extension code
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
| **Phase 1: Configs & Rig** | `NOT STARTED` | `package.json`, `vitest.config.js` | Initialize test environments, Vitest configurations, thresholds. |
| **Phase 1b: Chrome Mock** | `NOT STARTED` | `tests/mocks/chrome.mock.js` | Write Chrome API mock engines for storage, DNR and runtime. |
| **Phase 2: CSS styling** | `NOT STARTED` | `src/popup/popup.css`, `src/pages/blocked.css` | Premium HSL variables, fluid animations & layouts. |
| **Phase 3a: Worker Tests**| `NOT STARTED` | `tests/background.test.js` | **TDD Step**: Unit tests for background dynamic rules logic. |
| **Phase 3b: Worker Logic**| `NOT STARTED` | `src/background/service_worker.js`| Sync rules logic and startup listener implementation. |
| **Phase 4a: Popup Tests** | `NOT STARTED` | `tests/popup.test.js` | **TDD Step**: Unit tests for validation, list edits, toggle changes. |
| **Phase 4b: Popup Logic** | `NOT STARTED` | `src/popup/popup.js`, `popup.html` | management UI events, dynamic rendering, isRegexSupported checks. |
| **Phase 5a: Page Tests**  | `NOT STARTED` | `tests/blocked.test.js` | **TDD Step**: Unit tests for URL parameters and navigation. |
| **Phase 5b: Page Logic**  | `NOT STARTED` | `src/pages/blocked.js`, `blocked.html` | Parameter loading, layout bindings, and history fallback logic. |

---

## 5. Rules for Keeping This Document Updated

To maintain documentation integrity, every developer or AI tool modifying this repository **MUST** adhere to the following rules:

1.  **Read First**: Always read `LIVE_DOCUMENTATION.md` at the start of your workspace session.
2.  **No Changelogs**: Do **NOT** turn this document into a changelog of what you did. Instead, modify the existing sections (e.g. updating the "Repository Status", changing `[PLANNED]` files to `[ACTIVE]`, or updating the "Status Tracker" table) to represent the exact current layout.
3.  **TDD Observance**: Do not advance status rows for logic from `NOT STARTED` to `COMPLETED` unless the corresponding test row is already marked `COMPLETED` and unit test coverage reports indicate 100% metrics.
4.  **Update Promptly**: Perform modifications to this file at the end of every feature implementation or file change before declaring your task complete.
