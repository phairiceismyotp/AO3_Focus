# AI Audit Guide

This guide helps users perform an independent, low-noise review before using or rebuilding the bookmarklet.

## Audit scope

Review these source files first:

- `ao3-focus.js`
- `scripts/build-bookmarklet.js`

After reviewing the source and build script, you may compare the generated files in `dist/` against a fresh local build.

Do not upload private AO3 account data, private bookmarks, downloaded works, browser cookies, or personal browsing history into an AI tool.

## Expected runtime behavior

The runtime bookmarklet is expected to:

- Run only when manually clicked by the user.
- Accept only `archiveofourown.org` pages containing the `#workskin` container, aborting immediately if it is missing.
- Read the current AO3 page DOM to toggle the focus style sheet.
- Inject a temporary style element (`#ao3-focus-style`) and a progress bar element (`#ao3-focus-progress`).
- Use browser APIs to request fullscreen mode (`requestFullscreen`) and register a `fullscreenchange` listener.
- Walk the DOM to hide other elements on the page by setting display styles, and restore them when disabled.
- Detect the first visible paragraph (`<p>`) element inside `#workskin` (or fall back to the last paragraph if scrolled past) to adjust the scroll position (`window.scrollTo`) when transitioning layouts.
- Keep temporary toggling functions and state on `window.ao3Focus` and local closure scope.

Do not treat these behaviors as vulnerabilities by themselves. They are normal for this bookmarklet.

## Expected build behavior

The build script is expected to:

- Run locally with Node.js.
- Use `fs`, `path`, `process.argv`, `console`, and `process.exitCode`.
- Use `new Function` only to validate JavaScript syntax during the local build.
- Read the source file.
- Minify the runtime source.
- Write raw and encoded bookmarklet files into `dist/`.

The build script should not contact the network or install packages.

## Suggested AI prompt

```text
Please audit these files as a security, privacy, and transparency review before I use this AO3 focus mode bookmarklet:

Files:
- ao3-focus.js
- scripts/build-bookmarklet.js

Context:
- The runtime code is a browser bookmarklet for Archive of Our Own.
- It should run only when manually clicked on archiveofourown.org pages, aborting immediately if the #workskin reading container is missing.
- It should toggle fullscreen mode, hide non-essential DOM elements, style the remaining content, and create a top scroll progress bar.
- DOM injection, a temporary style block, fullscreen requests, paragraph element anchoring, scroll compensation, and window.ao3Focus state are expected behavior.
- The runtime should not send page data to third-party domains.
- The runtime should not collect AO3 credentials, read cookies directly, store private data, or upload content.
- The build script should only read local source, validate/minify JavaScript, and write generated bookmarklet files into dist/.

Please:
1. List every external domain, URL, or link target, and say whether it is contacted automatically or only opened after user action.
2. Identify whether the runtime uses fetch, XMLHttpRequest, sendBeacon, WebSocket, remote scripts, eval/new Function, localStorage, sessionStorage, cookies, clipboard APIs, or form submission.
3. Confirm whether any AO3 page data is sent anywhere.
4. Confirm whether the runtime host/page checks or script targets match the stated AO3-only scope.
5. Confirm whether the build script performs only local file reads/writes and JavaScript validation/minification.
6. Classify findings as:
   - Expected by design
   - Worth checking
   - Real issue
7. Avoid flagging expected DOM injection, CSS, fullscreen triggers, scroll triggers, or temporary in-page state as issues unless they are used to send or persist data unexpectedly.
8. Do not rewrite the code unless I ask for a patch.
```

## Findings that should matter

Treat these as real concerns if found:

- Runtime automatically contacts any non-AO3 domain.
- Runtime sends AO3 page data, credentials, cookies, or reading history to any third party.
- Runtime loads remote scripts, images, stylesheets, or analytics.
- Runtime uses `fetch`, `XMLHttpRequest`, `sendBeacon`, `WebSocket`, `eval`, or runtime `new Function`.
- Runtime writes private data to persistent storage.
- Runtime modifies AO3 bookmarks, account settings, forms, comments, works, or user profile data.
- Build script contacts the network, installs packages, executes generated code beyond syntax validation, or writes outside the intended output path.

## Expected safe shape

- Runtime should only read/modify the current page DOM and create temporary UI elements.
- Runtime should not collect or persist private AO3 data.
- Runtime should not have automatic third-party network behavior.
- `window.ao3Focus` should contain only the toggle functions.
- `new Function` and filesystem writes should appear only in `scripts/build-bookmarklet.js`.

## Important limit

AI review is helpful, but it is not a formal security audit. If you modify the code, review the diff again before rebuilding and using the bookmarklet.
