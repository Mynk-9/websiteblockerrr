# ORIGINAL PLAN: Premium Website Blocker Chrome Extension (MV3)

This document outlines the detailed architectural blueprint, user experience design, technology selection, and execution roadmap for building a state-of-the-art Chrome Extension for website blocking using Manifest V3.

---

## 1. Vision & Core Philosophy

The goal is to create a visually striking, highly secure, and extremely lightweight Chrome Extension that empowers users to block websites using regular expressions (regex).

### Key Principles:
*   **Zero Compromise on Performance**: Offload matching to the browser's native engine (`declarativeNetRequest` API) instead of parsing every page request in JavaScript.
*   **Frugal Permissions**: Run with the absolute minimum number of permissions possible. No general host permissions (`<all_urls>`) should be requested, maximizing trust, privacy, and speed.
*   **Wow-Factor UI/UX**: Break away from generic, boring extension layouts. Provide a stunning, modern dark-themed user interface with fluent animations, glowing glassmorphic elements, and harmonious HSL color palettes.

---

## 2. Technical Architecture & APIs

```mermaid
graph TD
    subgraph UI Layers (Frontend)
        A[Popup UI<br/>popup.html/css/js] -->|Save/Delete Regex| B[(chrome.storage.local)]
        C[Blocked Landing Page<br/>blocked.html/css/js]
    end
    
    subgraph Browser Engine (MV3 Core)
        B -->|Read/Sync Rules| D[Background Service Worker<br/>service_worker.js]
        D -->|Update Dynamic Rules| E[declarativeNetRequest API]
        E -->|Block & Redirect Request| C
    end
```

### 2.1 MV3 Declarative Net Request (DNR)
We will leverage Chrome’s native `chrome.declarativeNetRequest` API.
*   **Why**: Manifest V3 deprecates blocking `webRequest` in favor of declarative rules. The browser evaluates these rules directly in C++ before requests are dispatched, which is extremely fast and requires no host permissions.
*   **Dynamic Rules**: Since users can add/remove regexes dynamically, we will use `chrome.declarativeNetRequest.updateDynamicRules()` to modify rules at runtime.
*   **Frugal Redirect Hack**: To pass the original blocked URL to our custom `blocked.html` landing page *without* needing extra permissions (like `"webNavigation"` or `"tabs"`), we will use dynamic `regexSubstitution` in our redirect rule action:
    ```javascript
    const redirectUrl = chrome.runtime.getURL("pages/blocked.html") + "?url=\\0";
    const rule = {
      id: ruleId,
      priority: 1,
      action: {
        type: "redirect",
        redirect: { regexSubstitution: redirectUrl }
      },
      condition: {
        regexFilter: userRegexPattern,
        resourceTypes: ["main_frame"] // Block only full page navigations to avoid breaking API subresources
      }
    };
    ```
    *Note: `\0` in `regexSubstitution` is replaced by the entire matching URL, passing it cleanly to our landing page!*

### 2.2 Permissions Analysis
We will keep our permissions extremely frugal by requesting ONLY:
1.  `"declarativeNetRequest"`: To register blocking/redirection rules.
2.  `"storage"`: To persist user-defined regex patterns and global configurations (like the master toggle).

**What we will NOT request:**
*   `"<all_urls>"` or `"*://*/*"` (Host permissions): Not needed because `declarativeNetRequest` performs the redirect to internal extension pages without requiring host access.
*   `"webNavigation"` or `"tabs"`: Not needed since the original blocked URL is passed directly as a query parameter in the redirect action.

---

## 3. High-Fidelity UI/UX & Aesthetics

We will build a cohesive visual identity using curated HSL color schemes and premium styles.

### 3.1 Design System (Theming)
*   **Theme**: Cyberpunk Dark Slate / Neon Orange-Red glow.
*   **Typography**: `Outfit` or `Inter` imported from Google Fonts.
*   **Primary HSL Colors**:
    *   Background: `hsl(224, 25%, 12%)` (Deep slate)
    *   Card Overlay: `hsla(224, 25%, 20%, 0.6)` (Glassmorphism with backdrop-filter)
    *   Accent Glowing Red: `hsl(354, 85%, 56%)` (Warning / Blocked color)
    *   Accent Green: `hsl(142, 70%, 45%)` (Valid / Success color)
    *   Text Primary: `hsl(210, 40%, 98%)`
    *   Text Secondary: `hsl(215, 20%, 65%)`

### 3.2 View 1: Management Popup (`popup.html`)
A sleek, interactive dashboard (width: `360px`, height: `520px`):
*   **Header**: Glassmorphic banner featuring an organic animated logo, an active rule counter (e.g., `"5 active filters"`), and a custom-designed sliding master toggle switch with a deep orange-red glow when active.
*   **Add Filter Box**: 
    *   An input field with an animated floating border that changes from slate to orange-red on focus.
    *   Real-time regex validation using Chrome's native `chrome.declarativeNetRequest.isRegexSupported()`. Displays a smooth green checkmark or a bouncing red warning icon with standard validation feedback.
    *   An "Add" button that scales down slightly on click (`transform: scale(0.95)`) for premium haptic feel.
*   **Rule List**: 
    *   A list displaying each regex with a nice card design.
    *   Hovering over a rule reveals an elegant trash bin icon with a subtle shake animation.
    *   Smooth entry (`fade-in-slide-up`) and exit (`slide-out-fade`) animations for list items.

### 3.3 View 2: Redirect Landing Page (`blocked.html`)
A premium full-screen page displayed when a website is blocked:
*   **Background**: A deep dark slate background with a slow-moving, large radial gradient that pulses like an ambient warning light.
*   **Center Panel**: A large, floating glassmorphic container with high blur (`backdrop-filter: blur(16px)`) and a subtle white border (`border: 1px solid rgba(255,255,255,0.08)`).
*   **Visual Assets**: A glowing orange shield with a pulsing core, rendered using vanilla CSS and SVG paths.
*   **Typography**: Huge bold header `"Access Restricted"` followed by a detailed display of the original URL and the matching regex that triggered the block.
*   **CTA Button**: A massive "Go Back" button styled with an active background gradient and a custom ripple effect to return the user safely to their previous page.

---

## 4. Implementation Steps & Roadmap

Since we are in the planning phase, no code should be written yet. Below is the strict phase-by-phase implementation checklist:

### Phase 1: Infrastructure & Configurations
1.  Initialize `src/manifest.json` setting up Manifest V3, permissions, and icons.
2.  Set up background service worker registry in manifest.
3.  Configure HTML files for both `popup.html` and `blocked.html` along with their assets.

### Phase 2: Design Tokens & CSS Foundations
1.  Establish a shared standard in `src/popup/popup.css` and `src/pages/blocked.css` defining global custom CSS properties (variables) for HSL colors, animations, and typography.
2.  Implement base layout systems with Flexbox and CSS Grid.
3.  Write keyframe animations: `.fade-in`, `.slide-out`, `.pulse-glow`, and `.button-ripple`.

### Phase 3: Core Service Worker Logic
1.  Write `src/background/service_worker.js` with storage listeners.
2.  Implement the DNR synchronization system:
    *   A function `syncRulesWithDNR(rules, isEnabled)` that clears existing dynamic rules and installs new ones based on active regexes.
3.  Set up listeners for installation (`chrome.runtime.onInstalled`) to register default values and rules.

### Phase 4: Popup Management Controller
1.  Develop `src/popup/popup.js` to read/write from `chrome.storage.local`.
2.  Implement native Chrome regex validation check in the popup.
3.  Hook up popup events to trigger the background rules synchronization.
4.  Construct the animated list of rules.

### Phase 5: Landing Page & Parameter Parsing
1.  Build the layout of `src/pages/blocked.html`.
2.  Write `src/pages/blocked.js` to parse `window.location.search` for the `url` parameter.
3.  Display a cleaned version of the blocked URL and the matched pattern in the glassmorphic card.
4.  Bind "Go Back" button event to `window.history.back()` (falling back to closing the tab if history is empty).

---

## 5. Verification & Testing Strategy

*   **Regex Compatibility Tests**: Verify rules with complex patterns, wildcard expressions, and simple matches. Ensure that invalid/unsafe RE2 patterns are caught gracefully inside `popup.js` before reaching dynamic rules registration.
*   **Permission Verification**: Confirm in `chrome://extensions` that the extension requests absolutely zero host access warnings.
*   **Performance Benchmarks**: Test page loading speeds of non-blocked pages to prove the dynamic rule matching introduces zero latency.
