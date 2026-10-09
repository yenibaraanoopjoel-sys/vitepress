# Investigation: Algolia Ask AI Background Scroll (Issue #5451)

## Problem Description
When interacting with the Algolia DocSearch Ask AI dialog or conversation history, clicking items causes the background page to unexpectedly scroll to the top.

## Root Cause Analysis
1. In `VPAlgoliaSearchBox.vue`, `transformItems` transforms search hits using `getRelativePath(item.url)`.
2. Ask AI conversation history entries and action buttons contain empty strings (`""`) as their `item.url`.
3. The previous `getRelativePath(url)` executed `new URL(url, location.origin)`. When `url` is `""`, `new URL("", location.origin)` resolves to `location.origin + location.pathname` (the current page).
4. As a result, clicking an Ask AI history item triggers an in-page navigation or router event to the current page, which resets the page scroll position to top.

## Solution Strategy
1. Extract `getRelativePath` into `src/client/theme-default/support/docsearch.ts`.
2. Add an explicit check: if `url` is falsy/empty, return `""` immediately.
3. Guard `navigator.navigate(item)` so that `router.go()` is only invoked when `item.itemUrl` is non-empty.
4. Update `src/client/app/router.ts` to ignore links with empty href attributes.
5. Add unit tests for `getRelativePath`.
