# AO3 Focus Mode Bookmarklet

AO3 Focus Mode Bookmarklet is a small browser bookmarklet project for reading Archive of Our Own works in a distraction-free layout.

The project is unofficial and is not affiliated with Archive of Our Own, the Organization for Transformative Works, or any browser vendor.

<p align="center">
  <img src="assets/ao3_focus.gif" alt="AO3 Focus Bookmarklet" width="720">
</p>

The referenced work, author profile, and series belong to their respective AO3 creator (See more in the `Video tutorial` section).

## Video tutorial

[Watch the step-by-step installation guide on YouTube](https://www.youtube.com/watch?v=qyFPsbTBrt4)

The tutorial uses real AO3 data for an objective demonstration:

- Work: [Deliverance](https://archiveofourown.org/works/69891001)
- Author: [LadyOfRandom](https://archiveofourown.org/users/LadyOfRandom/pseuds/LadyOfRandom)

The referenced work, author profile, and series belong to their respective AO3 creator.

## Features

- Toggle reading focus mode on AO3 work pages.
- Hides all page content outside the main work container (`#workskin`).
- Requests browser fullscreen mode when enabled.
- Automatically disables focus mode and restores page visibility when exiting fullscreen.
- Applies a custom reader skin with Cambria font, cream background colors, 21px font size, and 1.6 line height.
- Displays a progress bar at the top of the viewport to track reading progress.
- Compensates for scroll position shifts using paragraph-level anchoring when toggling the reader layout.

## Files

- `ao3-focus.js` - readable bookmarklet source.
- `scripts/build-bookmarklet.js` - dependency-free build script.
- `dist/ao3-focus.bookmarklet.txt` - generated raw bookmarklet.
- `dist/ao3-focus.bookmarklet.encoded.txt` - generated encoded bookmarklet.
- `AI_AUDIT_GUIDE.md` - suggested checklist and prompt for independent AI review.
- `PRIVACY.md` - privacy and disclaimer notes.
- `NOTICE.md` - license notice and attribution.
- `package.json` - build command.

## How it works

`ao3-focus.js` runs on AO3 work pages.

When clicked, the bookmarklet first checks for the presence of the `#workskin` container on the page; if missing, it immediately aborts execution. It then checks for the presence of its custom style element to determine if focus mode is active. If active, it disables the mode by removing injected styles and elements, restoring original page visibility, and exiting fullscreen. If not active, it enables the interface by requesting fullscreen, appending the custom style element, injecting the progress bar, hiding other page content, and adding listeners for scroll and fullscreen changes.

To prevent the user from losing their place during layout and font-size changes, the toggling action is wrapped in a scroll anchor helper. The helper finds the first visible paragraph inside `#workskin` (or defaults to the last paragraph if scrolled past the text) before the transition, and scrolls the page to restore its relative viewport position afterward.

The bookmarklet does not communicate with external servers. All styling, DOM transformations, and scroll tracking are processed entirely within the user's browser.

## Supported pages

- AO3 work pages such as `/works/12345678` (supports both single-chapter and entire work views)

## Build

This project uses Node.js only to build the bookmarklet text files.

There are no runtime dependencies and no npm packages to install.

```bash
npm run build
```

The build script generates:

```text
dist/ao3-focus.bookmarklet.txt
dist/ao3-focus.bookmarklet.encoded.txt
```

The repository may already include generated bookmarklet files in `dist/`. Users can use the provided bookmarklet directly, but reviewing the readable source and rebuilding it locally is recommended.

The raw bookmarklet is easier to inspect. The encoded bookmarklet is more URL-safe.

## Installation

1. Download the full repository as a ZIP file from GitHub, then extract it.
2. Review `ao3-focus.js`.
3. Use the provided `dist/ao3-focus.bookmarklet.txt`, or install Node.js and run `npm run build` in the extracted project folder to generate it yourself.
4. Press `Ctrl + Shift + B` to show the browser bookmarks bar.
5. Right-click the bookmarks bar, choose `Add page...`, then name it something clear, such as `AO3 Focus`.
6. Paste the contents of one `*.bookmarklet.txt` file into the bookmark URL field.
7. Open an AO3 work page.
8. Click the bookmarklet.

## Configuration

The main configuration values are inside the CSS template string in `ao3-focus.js`.

- `font-family`: Font family applied to reading text.
- `background`: Body background color.
- `background-color`: Reading container background.
- `font-size`: Main content text size.
- `max-width`: Reading page width.
- `line-height`: Paragraph line spacing.
- `background` (progress bar): Gradient values for the progress indicator.

After changing configuration, run `npm run build` again.

## Privacy

This project is designed to run entirely in the user's browser on AO3 pages.

The author does not receive AO3 usernames, work data, reading history, or any other personal information.

Before installing, users are encouraged to review the readable source code and build the bookmarklet themselves.

## Limitations

- The scroll compensation relies on paragraph query selectors inside `#workskin`, which requires the text container to contain paragraph nodes to align dynamically.
- Fullscreen requests may fail if blocked by browser settings or running inside restricted frames.

## Acknowledgements

My deepest thanks go to the friends and beta testers from the Phainon x Castorice (PhaiRice) shipper community. Your support, testing, and suggestions helped shape this project from a small personal tool into something worth sharing.

Thank you, sincerely.

## License

AO3 Focus Mode Bookmarklet is licensed under AGPL-3.0-only. See `LICENSE` for the full license text.

Copyright (c) 2026 phairiceismyotp (or3zz - Nguyen Tin)
