# AGENT.md — Maintaining the Monica Web Summaries Index

## Project Structure

```
monica_web_sum/
  index.html          ← Root landing page (this repo's entry point)
  AGENT.md            ← This file
  {topic-name}/       ← Each subfolder is a standalone concept page
    index.html        ← Self-contained HTML page (styles + content)
```

## When to Update `index.html`

Update the root `index.html` whenever:
- A **new folder** containing an `index.html` is added to the repo root
- A folder is **removed** or **renamed**
- The **title or description** of an existing sub-page changes significantly

## How to Add a New Card to `index.html`

### Step 1: Read the new sub-page

```bash
# Read the <title> tag and the first 30-50 lines of body content
# to extract a meaningful title and description
```

### Step 2: Extract the following metadata

From the sub-page's `<title>` tag and content, extract:
- **Title**: The page title (use the `<h1>` text or a shortened version of `<title>`)
- **Description**: A 1-2 sentence summary of what the page covers
- **Tags/ArXiv ID**: If the page references a paper, include its arXiv ID
- **Affiliation**: Organization/company behind the work
- **Key features**: What makes this page special (diagrams, calculators, tables, etc.)

### Step 3: Choose a tag badge

Pick an unused color rotation from these 4 options:
| Tag text | CSS backgrounds |
|----------|----------------|
| `.card:nth-child(1)` | `#dbeafe` / `#2563eb` (blue) |
| `.card:nth-child(2)` | `#ede9fe` / `#7c3aed` (purple) |
| `.card:nth-child(3)` | `#d1fae5` / `#059669` (green) |
| `.card:nth-child(4)` | `#fef3c7` / `#d97706` (amber) |

More than 4 cards? Add new `:nth-child(N)` rules or switch to class-based tags.

### Step 4: Insert the card

1. Open `index.html`
2. Locate the `</div>` closing tag that ends the `.grid` div
3. Insert a new `<a class="card" ...>` block before `</div>` (before `</div>` of `.grid`)
4. Keep cards in **alphabetical order** by folder name

### Step 5: Card template

```html
<!-- === TOPIC-NAME === -->
<a href="topic-name/" class="card">
    <span class="tag">Short Category</span>
    <span class="arrow">&#8599;</span>
    <h2>Page Title: Brief Subtitle</h2>
    <p class="desc">
        One or two sentences describing what this page covers.
        Keep it concise — under 200 characters is ideal.
    </p>
    <div class="meta">
        <span>&#128214; arXiv:XXXX.XXXXX</span>
        <span>&#127968; Organization</span>
        <span>&#9881; Feature hint</span>
    </div>
</a>
```

### Step 6: Verify

- The `href` points to the folder name with a trailing `/` (e.g., `href="topic-name/"`)
- The card is in alphabetical order relative to existing cards
- The URL works when served locally or via GitHub Pages
- Description text is factual and matches the page content

## Style Rules

- **No JavaScript** in the index page — keep it pure HTML + CSS
- **No external dependencies** — no CDN fonts, no frameworks
- The card color rotation uses `nth-child` selectors — if you add cards, reindexing may shift colors; this is acceptable
- Maintain the same font stack: `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif`
- Keep the `.add-guide` hint box at the bottom of the grid

## Deployment

The site is deployed via GitHub Pages. After updating `index.html` or any sub-page:

```bash
git add -A
git commit -m "your commit message"
git push origin master
```

If GitHub Pages is configured to serve from the root of the `master` branch, the site will update automatically.
