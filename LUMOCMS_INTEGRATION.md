# Integrating this LumoCMS content into your frontend

This repository's content lives as plain JSON under `content/` with the schema
in `cms.config.json`. Read it at **build time** so your pages render to static
HTML (good for SEO).

## Reader

```bash
npm install @lumocms/reader
```

```ts
import { getCollection, getEntry, getSingleton } from '@lumocms/reader'

const root = process.cwd()
const posts = getCollection(root, 'posts')        // all entries in content/posts/
const one   = getEntry(root, 'posts', 'my-slug')  // one entry by _id
```

Works with Next.js, Astro, SvelteKit, or any tool that can read files at
build time. The dashboard's "Frontend Integration" panel has copy-paste snippets
for each framework.

## Per-collection prompts

Paste a section below into your coding agent (Claude Code, Cursor, …) to scaffold
pages for that collection.

---

## Context

I'm building a frontend for a LumoCMS-powered site.
Content is stored as plain JSON files in a GitHub repository.

Each entry file automatically includes these system fields:
  _id           unique identifier (also the filename without .json)
  _createdAt    ISO 8601 creation timestamp
  _updatedAt    ISO 8601 last-modified timestamp

────────────────────────────────────────────────────────

## Collection: Posts

Folder:  content/posts/
Each entry is a separate .json file named after its _id field.

### Fields

  title                 string        required
  excerpt               string        optional
  body                  string        optional
  coverImage            string        optional
  publishedAt           string        required

### TypeScript interface

export interface Posts {
  title: string
  excerpt?: string
  body?: string
  coverImage?: string
  publishedAt: string
}

────────────────────────────────────────────────────────

## Task

Please implement the following using [your framework]:

1. A utility function `getPostsList()` that reads all entries from `content/posts/`
2. A utility function `getPosts(id: string)` that reads a single entry by its `_id`
3. A list page that statically generates at build time
4. A dynamic detail page using `_id` as the URL segment (e.g. /posts/[id])

Use TypeScript throughout. Fetch all content at build time (static generation),
not at request time. The content folder lives at the repository root.
