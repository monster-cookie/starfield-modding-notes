# Bethesda Creations Description Formatting

> Last verified: August 21, 2026

The Bethesda Creations website does not appear to have a publicly available formatting reference or official syntax table. Bethesda only states that Creation descriptions support "markup formatting and hyperlinks" when viewed on the website. The formatting is not applied when a description is viewed in-game.

The current website implementation provides a more precise answer: Creation descriptions are processed using **Markdown-it**, with several important features deliberately disabled. It is not currently an early or limited HTML system.

## Short Version

Use ordinary Markdown for headings, emphasis, lists, blockquotes, code, horizontal rules, and tables.

Do not rely on raw HTML, embedded images, ordinary Markdown links, or automatic conversion of pasted URLs. For a clickable external URL, use the angle-bracket autolink form:

```markdown
<https://example.com>
```

Always preview the description on the website before publishing. Bethesda can change the renderer without announcing every implementation detail.

## What Bethesda Officially Documents

Bethesda's December 2023 Creations website announcement says descriptions support "markup formatting and hyperlinks." It also explains that the formatting is applied on Creation profile pages on the website, but not to descriptions shown in-game. The announcement does not identify the markup language or list its supported syntax.

Source: [Bethesda Game Studios Creations website updates](https://elderscrolls.bethesda.net/en-US/news/5BlfGSKgiJIRB1v5DlL6x2/bethesda-game-studios-creations-website-updates)

## What the Current Website Uses

The current Creations website bundles the Markdown-it parser. Its Creation-content processing code constructs the parser and disables the normal link and image rules:

```javascript
new MarkdownIt().disable(["link", "image"])
```

The remaining default configuration also has the following options disabled:

- Raw HTML input
- Automatic conversion of bare URLs into links
- Typographic substitutions
- Converting every ordinary newline into a visible line break

Consequently, the accepted input is best described as **basic Markdown-it with links, images, raw HTML, and optional plugins removed**.

## Supported Formatting

| Feature | Example syntax | Current behavior |
| --- | --- | --- |
| ATX headings | `# Heading` through `###### Heading` | Supported |
| Setext headings | Text followed by `===` or `---` | Supported |
| Bulleted lists | `- Item`, `* Item`, or `+ Item` | Supported |
| Numbered lists | `1. Item` | Supported |
| Bold | `**bold**` or `__bold__` | Supported |
| Italic | `*italic*` or `_italic_` | Supported |
| Strikethrough | `~~text~~` | Supported |
| Blockquotes | `> Quoted text` | Supported |
| Inline code | `` `code` `` | Supported |
| Indented code blocks | Four leading spaces | Supported |
| Fenced code blocks | Triple backticks or triple tildes | Supported |
| Horizontal rules | `---`, `***`, or `___` | Supported |
| Tables | Markdown pipe-table syntax | Parsed; site styling may be basic |
| Hard line breaks | Two trailing spaces or a backslash before a newline | Supported |
| Angle-bracket autolinks | `<https://example.com>` | Supported by the active autolink rule |
| HTML entities | `&amp;`, `&#32;`, or `&#x20;` | Supported, but provide no special layout features |

## Links and Images

Links are the most surprising part of Bethesda's configuration.

### Clickable URL

Use an angle-bracket autolink:

```markdown
Project page: <https://example.com/project>
```

### Bare URL

A pasted URL remains ordinary text because automatic URL linkification is disabled:

```markdown
https://example.com/project
```

### Named Markdown Link

Normal Markdown link syntax is explicitly disabled by the current application:

```markdown
[Project page](https://example.com/project)
```

Do not depend on reference-style links either. Although the parser can recognize reference definitions, the rule that turns the reference into a link is disabled.

### Embedded Image

Markdown images are also explicitly disabled:

```markdown
![Description of image](https://example.com/image.png)
```

Use the Creation's supported media and screenshot fields instead of trying to embed images inside the description.

## Raw HTML Is Not Supported

The current parser has HTML input disabled. Tags such as these should not be used for formatting:

```html
<h2>Heading</h2>
<b>Bold text</b>
<br>
<img src="https://example.com/image.png">
```

Depending on the surrounding input and later processing, the tags will generally be escaped or displayed as text instead of acting as HTML elements.

The earlier description of the site as using an "early HTML set" may refer to an older Bethesda.net implementation, or it may have confused the HTML produced by the renderer with the syntax accepted from authors. The current site code does not support that characterization.

## Features That Are Not Included

The site does not load the optional Markdown-it plugins normally required for features such as:

- Task-list checkboxes
- Footnotes
- Definition lists
- GitHub-style callouts or alerts
- Emoji shortcodes
- Highlighted or inserted text extensions
- Subscript and superscript extensions
- Mathematical notation
- Custom containers
- Embedded video markup

Some unsupported syntax may remain visible as ordinary text rather than producing an error.

## Line Breaks and Spacing

A single newline inside a paragraph normally remains a soft break and may appear as an ordinary space in the rendered page. Use one of these methods when a visible separation is required:

### New Paragraph

Leave an empty line:

```markdown
First paragraph.

Second paragraph.
```

### Hard Line Break

End the first line with two spaces or a backslash:

```markdown
First line.  
Second line.
```

Be careful with indentation. Four leading spaces create a code block, which can make an otherwise normal section appear in a fixed-width code box.

## Copy-Paste Starter

```markdown
# Overview

A short explanation of the Creation.

## Features

- First feature
- Second feature
- Third feature

## Installation

1. Add the Creation to your library.
2. Download it in-game.
3. Place it in the appropriate load-order position.

## Compatibility

**Compatible:** Describe compatible mods or systems.

**Not compatible:** Describe known conflicts.

> Important information that players should not overlook.

## Support

Project page: <https://example.com/project>
```

## Website Versus In-Game Display

Bethesda explicitly says the formatting is website-only. Players reading the description from the in-game Creations interface may see the original Markdown punctuation rather than the formatted result.

For that reason:

- Keep headings and lists understandable as plain text.
- Avoid layouts that depend entirely on tables.
- Do not hide essential instructions behind formatting alone.
- Put critical compatibility and installation information near the beginning.
- Check both the website preview and the in-game description when possible.

## Technical Sources

- [Bethesda's official December 2023 Creations website announcement](https://elderscrolls.bethesda.net/en-US/news/5BlfGSKgiJIRB1v5DlL6x2/bethesda-game-studios-creations-website-updates)
- [Current Bethesda Creations application bundle](https://creations.bethesda.net/bundles/bethesdanet.040811a8fada26347e50.js)
- [Current Bethesda Creations vendor bundle](https://creations.bethesda.net/bundles/vendor.df8c4bb20f19808d5a61.js)
- [Markdown-it project and documentation](https://github.com/markdown-it/markdown-it)

The two bundle URLs contain deployment hashes and will change whenever Bethesda publishes a new site build. They document the implementation observed on the verification date, not a permanent Bethesda compatibility guarantee.
