# FOND BUT NOT IN LOVE

Website for the label and management service. Two static pages, no build step,
no JavaScript, no dependencies.

```
index.html          home
impressum/          Impressum / Datenschutzerklärung
fonts/              Bernoru Black Ultra Expanded
```

Serve it locally with anything:

```bash
python3 -m http.server 8765
```

## How it is put together

Both pages are hand-written HTML with the CSS inline in a `<style>` block.
The original was a Canva Websites export; this replaces it with editable source.

**Two colours, nothing else.**

| | |
|---|---|
| red | `#FF324B` |
| green | `#ADFA48` |

The home page is red with green text; the Impressum inverts it — green ground,
red display type, black body copy.

**Text rewraps, it does not rescale.** Every reading size is a fixed pixel
value, so narrowing the window rebreaks lines instead of shrinking type. The
same body paragraph runs 3 lines at 1280px and 11 at 375px, all at 8.75px.
There are no layout breakpoints.

**The headline's green hugs the words.** It is painted on an inline span with
`box-decoration-break: clone`, so each wrapped row gets its own box and steps
in with that row's width. `line-height` is set to `1.07741` — the measured
height of that inline background box — which makes consecutive rows touch with
zero gap. Bernoru's own metrics predict `1.071429`, but browsers round ascent
and descent to whole pixels, so the measured figure is the one that closes it.

**Display type scales, reading text does not.** The headline holds 64.9714px
down to 320px wide and only scales below that, when the word "LOVE" can no
longer fit. The Impressum title scales earlier, because "DATENSCHUTZ" is a
single unbreakable word that fills its line — a soft hyphen lets it break as a
German compound rather than arbitrarily.

## Fonts

The display face is **Bernoru Black Ultra Expanded** (`fonts/`).

It has no `ß`, no `§` and no `„`, so it cannot set German legal text. That is
why the Impressum's running copy uses a monospace stack and reserves Bernoru
for the heading. Do not move that body copy back into Bernoru.

The Impressum's body face on the original Canva site was served under an
obfuscated name and could not be identified. It advances 8.023px per character
at render size — a 0.6em monospace advance at 13.37px — so a normal monospace
stack reproduces the character grid and every line break exactly, and only the
glyph shapes differ.

## Known, and deliberate

- **Green on red measures 2.85:1**, below WCAG AA and below even the 3:1
  large-text floor. It is the brand's palette and is kept on purpose. Black on
  the red measures 5.81:1 if a compliant variant is ever wanted.
- The Impressum lists two different addresses, matching the original.
