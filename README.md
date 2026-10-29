# affy landing templates

Starting points for the recruiting landing page of a merchant on affy.ink or an organization on bffy.ink. Each template is a Markdown text in Korean and English plus a small design file (palette, font, size, layout, button style). MIT licence: copy, change and publish them freely.

This folder is self-contained. It lives in the affy.ink repository today and is meant to be published later as `affyink/landing-templates`; nothing in it imports code from the repository.

## Templates

| Key | Best for | Palette | Font | Layout |
|-----|----------|---------|------|--------|
| `storyteller` | a brand with a story | paper | serif | single column |
| `outdoor-trail` | gear, sport, travel | forest | Pretendard | hero + two columns |
| `beauty-ritual` | beauty, care, wellness | berry | serif | campaign cards |
| `tech-minimal` | software, devices, tools | graphite | Inter | single column |
| `food-table` | food, drink, kitchen | sunset | Pretendard | campaign cards |
| `night-studio` | games, audio, creative tools | midnight | Inter | hero + two columns |
| `lifestyle-coast` | fashion, home, lifestyle | ocean | Pretendard | hero + two columns |

## Files of one template

```
<key>/
  template.json   key, names and descriptions (en, ko), the design, and per language the heading and the meta description
  en.md           the text in English
  ko.md           the text in Korean
```

`template.json`:

```json
{
  "key": "storyteller",
  "names": { "en": "Storyteller", "ko": "스토리텔러" },
  "descriptions": { "en": "...", "ko": "..." },
  "design": { "paletteKey": "paper", "fontKey": "serif", "sizeKey": "M", "layoutKey": "single-column", "buttonStyleKey": "solid", "accentColorHex": null },
  "locales": { "en": { "aboutHeading": "Our story", "metaDescription": "..." }, "ko": { "aboutHeading": "...", "metaDescription": "..." } }
}
```

The design values are the allow-lists of the page builder; anything else is refused when the page is saved:

| Key | Values |
|-----|--------|
| `paletteKey` | `platform`, `paper`, `ocean`, `forest`, `sunset`, `berry`, `graphite`, `midnight` |
| `fontKey` | `platform`, `pretendard`, `inter`, `serif`, `mono` (all self-hosted) |
| `sizeKey` | `S`, `M`, `L` |
| `layoutKey` | `single-column`, `hero-two-columns`, `campaign-cards` |
| `buttonStyleKey` | `solid`, `pill`, `outline`, `square` |
| `accentColorHex` | `null` (the palette's accent) or one `#rrggbb` colour that keeps a contrast of 4.5:1 on the palette's backgrounds (WCAG AA) |

## Writing the Markdown

- CommonMark and GitHub tables. No HTML, no scripts: they are refused.
- Headings start at `##` (the page owns the single `h1`). `{{companyName}}`, `{{websiteHost}}` and `{{websiteUrl}}` are replaced with the merchant's name and website when a template is applied (write the website as `[{{websiteHost}}]({{websiteUrl}})`: a bare address followed by Korean text is read as one long address and refused).
- The commission, cookie days, payout rules, the four steps to join and the disclosure are written by the platform from the merchant's data, never in the text. Do not promise income or restate numbers.
- Links only to the merchant's own website, affy.ink / bffy.ink, `mailto:` and YouTube / Vimeo; images only uploaded to affy or on the merchant's website, with alt text.
- A video is a line of its own: `[Caption](https://www.youtube.com/watch?v=...)`, or the Markdown-Videos form `[![Caption](thumbnail-url)](video-url)`. It loads only after a click.
- At least 300 characters of text, otherwise search engines are asked not to index the page.

## Adding a template

1. Copy a folder, change the key (lower case letters, digits and hyphens).
2. Write `en.md` and `ko.md`, then fill `template.json`.
3. Run the checks of the affy.ink repository: `pnpm --filter @affyink/api exec vitest run src/__tests__/landing-templates.test.ts` validates every design, every text and the placeholders, and `pnpm --filter @affyink/dashboard landing-templates` rebuilds the copy the dashboard ships (no runtime fetch).
4. Open a pull request with a screenshot of the page in both languages.
