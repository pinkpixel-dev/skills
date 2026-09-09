# Lantern Overview

Lantern is a fictional self-hosted reading-list application used as an example for an AI coding context workflow.

The product goal is simple: save articles and links quickly, organize them into useful collections, and make them easy to find later.

This document is an example of what a living technical overview can look like. It should describe the current state of a project, not its history.

## Stack

- Next.js with TypeScript
- React
- Tailwind CSS
- SQLite with Drizzle ORM
- Better Auth for authentication
- Vitest for unit tests
- Playwright for browser-level tests
- Docker for self-hosted deployment

## Core Product Flow

1. A signed-in user submits a URL.
2. The API validates and normalizes the URL.
3. A bookmark record is saved immediately.
4. Metadata extraction runs after the save.
5. The title, description, site name, favicon, and reading status are stored.
6. The bookmark appears in the user's library.
7. Users can search, filter, tag, archive, or move bookmarks into collections.

The raw URL should always be saved before optional metadata processing begins. Metadata failures must not cause the bookmark itself to be lost.

## Project Structure

```text
src/
├── app/
│   ├── api/
│   ├── library/
│   ├── collections/
│   └── settings/
├── components/
├── db/
├── lib/
│   ├── bookmarks/
│   ├── collections/
│   ├── metadata/
│   └── search/
└── tests/
```

Project documentation lives in `/DOCS`.

Important files:

- `/DOCS/OVERVIEW.md`: current architecture and behavior
- `/DOCS/MEMORY.md`: significant decisions and rejected alternatives
- `/DOCS/ERRORS.md`: difficult bugs, failed approaches, and reusable fixes
- `/DOCS/ROADMAP.md`: planned work
- `README.md`: user-facing project documentation
- `CHANGELOG.md`: release history

## Data Model

### bookmarks

Important fields:

- `id`
- `user_id`
- `url`
- `normalized_url`
- `title`
- `description`
- `site_name`
- `favicon_url`
- `reading_status`
- `archived_at`
- `created_at`
- `updated_at`

### collections

Important fields:

- `id`
- `user_id`
- `name`
- `slug`
- `created_at`

### tags

Tags are user-scoped.

Bookmarks and tags use a join table so a bookmark can have multiple tags.

## Authentication

Authentication is handled through Better Auth.

Protected routes require an authenticated user.

Every bookmark, collection, and tag query must be scoped by `user_id`.

Cross-account access is considered a security bug.

## Bookmark Creation

`POST /api/bookmarks` accepts:

```json
{
  "url": "https://example.com/article"
}
```

The route:

1. requires authentication
2. validates the URL
3. normalizes the URL
4. checks whether the user already saved the normalized URL
5. creates the bookmark
6. starts metadata processing

Metadata processing is intentionally secondary. If metadata extraction fails, the saved bookmark remains usable.

## Metadata Extraction

Metadata extraction may populate:

- page title
- description
- site name
- favicon

Metadata extraction must:

- use a reasonable timeout
- reject unsupported protocols
- avoid fetching private/internal network addresses
- fail gracefully
- never overwrite a user-edited title without explicit rules allowing it

## Search

Search currently covers:

- bookmark title
- URL
- description
- tags
- collection name

Search is user-scoped.

Archived bookmarks are excluded from ordinary library search unless the archived filter is enabled.

## Collections

Users can:

- create collections
- rename collections
- delete collections
- move bookmarks between collections

Deleting a collection does not delete its bookmarks. Bookmarks in the deleted collection become uncategorized.

## Archive Behavior

Archiving a bookmark sets `archived_at`.

Archived bookmarks:

- disappear from the default library view
- remain searchable from the archived view
- can be restored
- are not permanently deleted

Permanent deletion is a separate action.

## Important Routes

- `/` landing or redirect
- `/library` main bookmark library
- `/collections` collection list
- `/collections/[slug]` collection detail
- `/archive` archived bookmarks
- `/settings` account and application settings

## API Routes

- `GET /api/bookmarks`
- `POST /api/bookmarks`
- `GET /api/bookmarks/[id]`
- `PATCH /api/bookmarks/[id]`
- `DELETE /api/bookmarks/[id]`
- `GET /api/collections`
- `POST /api/collections`
- `PATCH /api/collections/[id]`
- `DELETE /api/collections/[id]`
- `GET /api/search?q=...`

## Testing

Use the smallest relevant test set for the task.

Typical commands:

```bash
npm run lint
npm run typecheck
npm test
npm run test:e2e
npm run build
```

Browser-level tests are most useful for:

- authentication boundaries
- cross-account isolation
- bookmark creation
- archive/restore flows
- collection management
- important mobile interactions

Do not run the full browser suite after trivial text or styling edits unless browser behavior is directly affected.

## Deployment

The application is deployed as a Docker container.

Deployment requires explicit authorization.

The release process should verify:

- the production build passes
- required environment variables are documented
- database migrations are reviewed
- no development secrets are included
- the changelog is current when a release warrants one

## Environment

Example local environment:

```bash
DATABASE_URL=file:lantern-dev.sqlite
BETTER_AUTH_SECRET=
BETTER_AUTH_URL=http://localhost:3000
METADATA_FETCH_TIMEOUT_MS=8000
```

Do not commit real secrets.

## Current Limits

- Browser extension capture is not implemented.
- Full-text article content is not stored.
- Offline support is limited.
- Shared/public collections are not implemented.
- Import from browser bookmark exports is planned but not implemented.

Keep this section accurate. An overview is only useful when it reflects what the project actually does today.
