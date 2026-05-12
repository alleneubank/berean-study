---
name: berean-study
description: "Expand sermon notes or Bible passages with additional scripture references, biblical context, and cross-testament connections. Outputs a beautifully designed single HTML page for a personal study library."
---

# Berean Study

> "Now the Berean Jews were of more noble character than those in Thessalonica, for they received the message with great eagerness and examined the Scriptures every day to see if what Paul said was true." — Acts 17:11

Take teaching and dig into the Word to expand, verify, and connect.

## Input Types

The skill accepts three kinds of input:

1. **Sermon notes** — From a Fearless House email or any church sermon. Read the images, extract the notes, then expand.
2. **A passage** — "Study Romans 8" or "Berean study on John 15:1-17". Start from the text itself.
3. **Pasted notes** — User provides their own notes or outline to expand.

## Expansion Process

For each point or section in the source material:

### 1. Identify the Core Truth
State the main idea in one sentence. What is this point really saying?

### 2. Add Scripture References (3-6 per point)
Find verses that:
- **Reinforce** the point from a different book or testament
- **Deepen** it with additional context or nuance
- **Show the pattern** across Scripture (OT → NT continuity)
- **Apply** it practically

For each reference, include:
- The full verse text (use ESV as the baked-in text)
- A 1-2 sentence explanation of how it connects to the point
- The book, chapter, and verse in standard format

### 3. Biblical Placement
For each major section, write a short paragraph explaining:
- Where this passage sits in the biblical narrative
- What was happening historically when it was written
- How it connects to the broader arc of Scripture

### 4. Cross-Testament Threads
When an OT passage is fulfilled or echoed in the NT (or vice versa), call it out explicitly. These threads reveal the unity of Scripture.

## Series Awareness

Check the `studies/` directory for existing HTML files. Look for:
- Same series name (e.g., other "You've Heard It Said" parts)
- Same church/source
- Related topics

If previous studies exist in a series, link to them in the header navigation.

## Output

### File Generation

Generate a single self-contained HTML file using the template at:
`.claude/skills/berean-study/template.html`

Read the template and generate the output file with all content filled in.

**Filename:** `studies/{date}-{slugified-title}.html`
Example: `studies/2026-03-22-youve-heard-it-said-pt2.html`

### Library Index

After generating the study file, update `studies/index.html`:
- If it doesn't exist, create it using the library template at `.claude/skills/berean-study/library-template.html`
- Add the new study to the list
- Maintain reverse chronological order
- Group by series when applicable

### Content Structure in the HTML

The generated HTML must include:

1. **Header** — Church/source name, date, series title, part number
2. **Series navigation** — Links to other parts if they exist
3. **Table of contents** — Anchor links to each section
4. **Expanded sections** — Each point with:
   - Section heading with drop cap on first paragraph
   - Primary scripture in a featured block
   - Expansion text with inline scripture references
   - Additional references as expandable blocks
   - "Biblical Placement" in a distinct aside style
5. **Scripture Index** — All verses referenced, in canonical order (Genesis → Revelation), each linking to its section and to Blue Letter Bible

### Scripture Reference Format

Every scripture reference in the HTML must be:
- Wrapped in `<a>` tags with class `scripture-ref`
- `data-book`, `data-chapter`, `data-verse` attributes for the JS translation switcher
- `href` pointing to Blue Letter Bible (default ESV)
- `target="_blank"` with `rel="noopener"`

The translation dropdown (stored in localStorage) updates all BLB links on the page via JavaScript.

### Blue Letter Bible URL Pattern

```
https://www.blueletterbible.org/{translation}/{book-abbrev}/{chapter}/{verse}/
```

Book abbreviations for BLB URLs:

| Book | Abbrev | Book | Abbrev |
|------|--------|------|--------|
| Genesis | gen | Matthew | mat |
| Exodus | exo | Mark | mar |
| Leviticus | lev | Luke | luk |
| Numbers | num | John | jhn |
| Deuteronomy | deu | Acts | act |
| Joshua | jos | Romans | rom |
| Judges | jdg | 1 Corinthians | 1co |
| Ruth | rth | 2 Corinthians | 2co |
| 1 Samuel | 1sa | Galatians | gal |
| 2 Samuel | 2sa | Ephesians | eph |
| 1 Kings | 1ki | Philippians | phl |
| 2 Kings | 2ki | Colossians | col |
| 1 Chronicles | 1ch | 1 Thessalonians | 1th |
| 2 Chronicles | 2ch | 2 Thessalonians | 2th |
| Ezra | ezr | 1 Timothy | 1ti |
| Nehemiah | neh | 2 Timothy | 2ti |
| Esther | est | Titus | tit |
| Job | job | Philemon | phm |
| Psalms | psa | Hebrews | heb |
| Proverbs | pro | James | jas |
| Ecclesiastes | ecc | 1 Peter | 1pe |
| Song of Solomon | sng | 2 Peter | 2pe |
| Isaiah | isa | 1 John | 1jo |
| Jeremiah | jer | 2 John | 2jo |
| Lamentations | lam | 3 John | 3jo |
| Ezekiel | eze | Jude | jud |
| Daniel | dan | Revelation | rev |
| Hosea | hos |
| Joel | joe |
| Amos | amo |
| Obadiah | oba |
| Jonah | jon |
| Micah | mic |
| Nahum | nah |
| Habakkuk | hab |
| Zephaniah | zep |
| Haggai | hag |
| Zechariah | zec |
| Malachi | mal |

### Supported Translations

| Name | BLB Code | Display |
|------|----------|---------|
| English Standard Version | esv | ESV |
| New King James Version | nkjv | NKJV |
| King James Version | kjv | KJV |
| New American Standard Bible | nasb20 | NASB |
| New International Version | niv | NIV |
| New Living Translation | nlt | NLT |

Default: ESV

## Quality Standards

- Every verse reference must be accurate — book, chapter, verse verified
- Inline verse text must be faithful to the ESV (the baked-in translation)
- Expansion should be substantive, not filler — each added reference should genuinely illuminate the point
- Biblical placement sections should be historically grounded
- Tone: reverent but accessible, scholarly but warm — like a trusted study partner, not a commentary
