# Good And Bad Entries

Every example below is either drawn from the sample project in `examples/`, or written to show the failure mode next to the fix. Read the pairs, not just the good halves.

## MEMORY.md

### Bad: a changelog line wearing a decision heading

```md
### Decision: Added the archive feature

What was decided: Users can now archive bookmarks.

Why: It was on the roadmap.
```

Nothing here survives contact with a future contributor. There is no alternative, no cost, and no reason anyone would need to know later. "It was on the roadmap" is not a reason, it is a schedule.

### Good: the same feature, but the part that was actually decided

```md
### Decision: Keep archive separate from permanent deletion

What was decided: Archive is a reversible state stored in `archived_at`. Permanent deletion remains a separate explicit action.

Why: Users often want to hide old bookmarks without losing them. Combining archive and deletion would make an ordinary cleanup action unnecessarily risky.

Rejected: A single Delete action with a short Undo window. It makes long-term recovery impossible once the undo expires.
```

The field name is there, the tradeoff is named, and the rejected option explains why the obvious simpler design was not taken.

### Bad: too vague to check

```md
### Decision: Improve duplicate detection

What was decided: Duplicate detection was made better.

Why: It was missing duplicates.

Rejected: Leaving it as it was.
```

"Better" is not a design. "Leaving it as it was" is not an alternative.

### Good: specific enough to verify against the code

```md
### Decision: Use normalized URLs for duplicate detection

What was decided: Duplicate checks use `normalized_url`, while the original submitted URL remains stored separately.

Why: Tracking parameters, fragments, and trivial formatting differences can make the same page appear to be different URLs. Normalization catches obvious duplicates without destroying the original input.

Rejected: Comparing only the raw submitted URL. It misses common duplicate cases.

Rejected: Aggressively canonicalizing every URL using site-specific rules. That adds complexity and can incorrectly merge distinct pages.
```

Two rejected options, one too weak and one too aggressive, which shows where the chosen design sits between them.

### Good: a decision not to build something

```md
### Decision: Search stays database-backed for now

What was decided: Search uses the existing database fields and indexes rather than adding an external search service.

Why: The current dataset and feature set do not justify another service, deployment dependency, or synchronization pipeline.

Rejected: Adding Elasticsearch or Meilisearch during the initial release. Both could become useful later, but they are unnecessary at the current scale.
```

"Not yet" decisions are some of the most valuable entries, because they are the ones most likely to be re-proposed by someone who assumes nobody considered it.

## ERRORS.md

### Bad: a symptom with no transferable lesson

```md
### Note: Metadata was broken

What did not work: Metadata extraction did not work.

What worked instead: Fixed it.

Note for next time: Be careful with metadata.
```

Nobody can recognize their own problem in this, and nobody can apply the fix.

### Good: the same incident, written to be findable

```md
### Note: Metadata fetches can hang on servers that accept a connection but never finish the response

What did not work: Relying on the default `fetch()` behavior during metadata extraction. A test URL accepted the connection but never completed the response, which left metadata processing running much longer than expected.

What worked instead: Wrap metadata requests in an `AbortController` and enforce the configured timeout. Treat the timeout as a metadata failure, not a bookmark-creation failure.

Note for next time: Remote metadata is untrusted network work. Every fetch path needs an explicit timeout.
```

The title describes the trap, so someone watching a request hang will find it. The last line generalizes past this one endpoint.

### Bad: a fixed bug that did not need an entry

```md
### Note: Favicon component crashed on null

What did not work: The favicon component threw when `favicon_url` was null.

What worked instead: Added a null check.

Note for next time: Check for null.
```

Found in one attempt, obvious cause, obvious fix. This is a commit, not a lesson.

### Good: the favicon problem that was worth writing down

```md
### Note: Browser favicon URLs are frequently relative

What did not work: Saving the raw `href` from `<link rel="icon">`. Many sites return values such as `/favicon.ico`, which produced broken image URLs when rendered directly.

What worked instead: Resolve icon URLs against the final response URL with `new URL(iconHref, pageUrl)` before saving them.

Note for next time: Treat extracted page URLs as potentially relative unless the relevant standard guarantees otherwise.
```

### Good: the root cause was not where the symptom was

```md
### Note: Playwright test failures were caused by shared test data, not the archive feature

What did not work: Treating an intermittently failing archive test as a regression in the archive implementation. Re-running the test produced different failures depending on which test created bookmarks first.

What worked instead: Give each test a separate account and disposable database state. The archive flow passed consistently once tests stopped sharing user data.

Note for next time: When browser failures move between assertions or depend on test order, inspect shared state before changing application code.
```

### Good: a setting that does not carry between processes

```md
### Note: SQLite foreign keys were not enabled in one local script

What did not work: Assuming a local maintenance script had the same SQLite connection settings as the application. Deleting a bookmark left orphaned rows in the bookmark-tag join table because foreign-key enforcement was not enabled for that connection.

What worked instead: Explicitly enable foreign keys when creating the script's SQLite connection and add a small integrity check after destructive maintenance operations.

Note for next time: SQLite foreign-key behavior is connection-specific. Do not assume a standalone script inherits application database configuration.
```

## OVERVIEW.md

### Bad: history leaking into a present-tense document

```md
## Search

Search was originally built on raw SQL LIKE queries. In August we moved it to
indexed columns, and we considered Meilisearch but decided against it for now.
Currently it searches titles and descriptions.
```

Two thirds of this is `MEMORY.md` content. The one useful sentence is buried at the end.

### Good: what is true now, with the reasoning left in the decision log

```md
## Search

Search runs against the database using indexed `title` and `description`
columns, scoped by `user_id`. It supports filtering by collection, tag, and
archived state. There is no external search service.
```

### Bad: vague enough to be useless

```md
## Bookmark Creation

The API handles bookmark creation with validation and some processing.
```

### Good: the flow, in order, with the invariant stated

~~~md
## Bookmark Creation

`POST /api/bookmarks` accepts:

```json
{ "url": "https://example.com/article" }
```

The route:

1. requires authentication
2. validates the URL
3. normalizes it into `normalized_url`
4. checks for an existing bookmark with the same `normalized_url` for this user
5. saves the bookmark
6. starts metadata extraction after the save returns

The raw URL is always saved before metadata processing begins. A metadata
failure must never prevent the bookmark from being created.
~~~
