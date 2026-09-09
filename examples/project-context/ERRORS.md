# Errors

This is a fictional example of a reusable debugging log.

Use this file for failures that took multiple attempts, had a surprising root cause, or are likely to waste time again later.

Do not turn this into a complete bug tracker.

## 2026-08-06

### Note: Metadata fetches can hang on servers that accept a connection but never finish the response

What did not work: Relying on the default `fetch()` behavior during metadata extraction. A test URL accepted the connection but never completed the response, which left metadata processing running much longer than expected.

What worked instead: Wrap metadata requests in an `AbortController` and enforce the configured timeout. Treat the timeout as a metadata failure, not a bookmark-creation failure.

Note for next time: Remote metadata is untrusted network work. Every fetch path needs an explicit timeout.

## 2026-08-12

### Note: URL normalization must happen before duplicate lookup

What did not work: Querying for an existing bookmark using the raw submitted URL and normalizing only before insert. URLs that differed only by a fragment or removable tracking parameters passed the duplicate check and were inserted twice.

What worked instead: Normalize first, then use `normalized_url` for both lookup and insert.

Note for next time: Validation and normalization order matters. Any uniqueness rule based on transformed data must use the transformed value before the existence check.

## 2026-08-19

### Note: Playwright test failures were caused by shared test data, not the archive feature

What did not work: Treating an intermittently failing archive test as a regression in the archive implementation. Re-running the test produced different failures depending on which test created bookmarks first.

What worked instead: Give each test a separate account and disposable database state. The archive flow passed consistently once tests stopped sharing user data.

Note for next time: When browser failures move between assertions or depend on test order, inspect shared state before changing application code.

## 2026-08-24

### Note: SQLite foreign keys were not enabled in one local script

What did not work: Assuming a local maintenance script had the same SQLite connection settings as the application. Deleting a bookmark left orphaned rows in the bookmark-tag join table because foreign-key enforcement was not enabled for that connection.

What worked instead: Explicitly enable foreign keys when creating the script's SQLite connection and add a small integrity check after destructive maintenance operations.

Note for next time: SQLite foreign-key behavior is connection-specific. Do not assume a standalone script inherits application database configuration.

## 2026-08-31

### Note: Browser favicon URLs are frequently relative

What did not work: Saving the raw `href` from `<link rel="icon">`. Many sites return values such as `/favicon.ico`, which produced broken image URLs when rendered directly.

What worked instead: Resolve icon URLs against the final response URL with `new URL(iconHref, pageUrl)` before saving them.

Note for next time: Treat extracted page URLs as potentially relative unless the relevant standard guarantees otherwise.
