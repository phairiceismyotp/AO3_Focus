# Privacy and Disclaimer

AO3 Focus Mode Bookmarklet is designed to run in the user's own browser on Archive of Our Own pages.

## Data handling

- The bookmarklet reads and modifies the current AO3 page DOM to toggle the reading interface.
- It does not automatically send data to third-party domains, analytics services, or author-controlled servers.
- It does not collect AO3 passwords, read cookies directly, or store reading history.
- It keeps only temporary in-page toggle state and elements references on `window.ao3Focus` and local closure scope variables.
- It does not use persistent browser storage such as `localStorage` or `sessionStorage`.

When running, the browser naturally handles AO3 session cookies for requests and layout rendering on AO3, the same way it does during normal browsing.

## User responsibility

Users are responsible for reviewing the source code, rebuilding the bookmarklet if desired, and deciding whether to use the generated bookmarklet file.

Users should also follow AO3's terms, respect authors' works, and configure browser settings appropriately.

## Disclaimer

This project is provided without warranty. The author is not responsible for browser behavior, account issues, changed AO3 page structure, or data loss.

This project is unofficial and is not affiliated with, endorsed by, or maintained by the Organization for Transformative Works or Archive of Our Own.
