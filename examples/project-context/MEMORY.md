# Memory

This is a fictional example of a project decision log.

Use this file for significant decisions that future contributors or AI agents may otherwise revisit without knowing the original reasoning.

Do not log every tiny implementation choice.

## 2026-08-04

### Decision: Save bookmarks before metadata extraction

What was decided: A submitted URL is saved as a bookmark before title, description, favicon, or site metadata is fetched.

Why: Saving the bookmark is the user's primary action. A slow, blocked, or malformed remote website should not cause the user to lose the URL they were trying to save.

Rejected: Fetching metadata first and only creating the bookmark after extraction succeeds. That makes a secondary network operation part of the critical save path.

### Decision: Use normalized URLs for duplicate detection

What was decided: Duplicate checks use `normalized_url`, while the original submitted URL remains stored separately.

Why: Tracking parameters, fragments, and trivial formatting differences can make the same page appear to be different URLs. Normalization catches obvious duplicates without destroying the original input.

Rejected: Comparing only the raw submitted URL. It misses common duplicate cases.

Rejected: Aggressively canonicalizing every URL using site-specific rules. That adds complexity and can incorrectly merge distinct pages.

## 2026-08-09

### Decision: Keep collections single-level

What was decided: Collections do not support nesting.

Why: The current product only needs simple grouping. Nested collections would complicate navigation, moving items, breadcrumb behavior, and mobile UI without solving an observed problem.

Rejected: Parent/child collections. Revisit only if real usage shows that flat collections are becoming difficult to manage.

### Decision: Deleting a collection does not delete bookmarks

What was decided: When a collection is deleted, its bookmarks become uncategorized.

Why: Collections are organizational metadata. Deleting a container should not destroy the user's saved content.

Rejected: Cascading collection deletion into bookmark deletion. Too destructive for an organizational action.

## 2026-08-17

### Decision: Keep archive separate from permanent deletion

What was decided: Archive is a reversible state stored in `archived_at`. Permanent deletion remains a separate explicit action.

Why: Users often want to hide old bookmarks without losing them. Combining archive and deletion would make an ordinary cleanup action unnecessarily risky.

Rejected: A single Delete action with a short Undo window. It makes long-term recovery impossible once the undo expires.

## 2026-08-22

### Decision: Metadata extraction cannot overwrite user-edited titles

What was decided: Once a user manually edits a bookmark title, later metadata refreshes keep that title unless the user explicitly asks to replace it.

Why: User-authored data should take precedence over automated enrichment.

Rejected: Always replacing the title with the latest remote page title. That could silently erase a name the user intentionally chose.

## 2026-08-29

### Decision: Search stays database-backed for now

What was decided: Search uses the existing database fields and indexes rather than adding an external search service.

Why: The current dataset and feature set do not justify another service, deployment dependency, or synchronization pipeline.

Rejected: Adding Elasticsearch or Meilisearch during the initial release. Both could become useful later, but they are unnecessary at the current scale.

## Example Session Summary

Use session summaries only if the project workflow calls for them.

### Session Summary: 2026-08-29

Worked on:
- Search filtering
- Archive behavior

Completed:
- Added archived-only search mode
- Added tests for restore behavior

In progress:
- Search result highlighting

Decisions made:
- Keep search database-backed for now

Next session priorities:
- Finish highlighting
- Check mobile search layout
