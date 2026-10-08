# Inline image text section

## Build plan
Content section for landing pages, available on all templates. Reuses the rich-text section shell, page-width container, section color scheme, background and responsive padding conventions. Typography remains owned by existing blocks.

## Ownership and composition
- sections/inline-image-text.liquid: scoped shell, alignment, circular image crop and section preset.
- blocks/eyebrow.liquid: existing static introductory text.
- blocks/editorial-text.liquid: existing static rich text, image markers, five image pickers, image links, typography and block editor attributes.
- Both allowed block types have categorized presets. Two static blocks plus up to six dynamic blocks of those types. No app blocks or nested broad allow-list.
- Default text follows the reference in two paragraphs, with three enabled circular image slots (60px desktop, 40px mobile). Missing image slots show editor placeholders and are omitted on the storefront by the existing block.
- No additional JavaScript. Existing editorial-text runtime handles its lifecycle; reveal is disabled in the preset.

## Acceptance and release checklist
| Key | Status | Evidence |
| --- | --- | --- |
| contract | pass | Existing shell, typography, color and padding conventions reused. |
| schema | pass | Valid schema JSON; categorized allow-list; default values match existing block settings. |
| liquid | pass | Local Theme Check, no errors and no finding for the new section. |
| css | pass | Section-scoped selectors; responsive image width comes from reused block; circular object-fit crop. |
| js | pass | No new JS; preset disables reveal. |
| responsive | pass | Storefront verified at desktop and 390px viewport; no section horizontal overflow. Image presentation requires merchant assets. |
| accessibility | blocked | Text rendered and readable. Image alt/link reviewed in reused block; actual images are not selected yet. |
| editor | blocked | Static IDs and presets reviewed; live add/select/reload validation pending. |
| release | blocked | Code ready for editor insertion; external MCP validation rejected by automatic approval review. Local check passed with 32 existing warnings. No commit or release performed. |

## Usage
Add section > Inline image text. In Editorial text, choose Image 1, Image 2 and Image 3. Markers [img1], [img2] and [img3] determine inline placement. Use block settings for font size and image width, and section settings for alignment, color and padding. Exact reference images were not available as separate assets; merchant image selection is required.
Homepage integration: templates/index.json beauty_message now uses the new section in its existing position, directly after Best Sellers.

Heading update: Editorial text now exposes HTML tag choices div and H1-H6, following the heading block contract. This section and its homepage instance default to H2. Heading content uses span lines instead of nested paragraph tags. Storefront H2 and both text lines verified. Theme Check: zero errors, 32 warnings; editorial block retains its existing excessive-settings warning (now 54 settings).

Image controls update: all five image slots default to desktop 90px/mobile 64px. Desktop width range remains 20-500 with 5px steps (97 values); mobile remains 20-300 with 4px steps (71 values), supporting exact 64px within Shopify slider limits. Existing border radius choices now label inherited styling Default. Homepage and section preset use 90/64px. Theme Check: zero errors, 32 warnings.

Static heading update: this section uses inline-image-heading with three image slots and no Scroll settings. Both editorial-text and inline-image-heading reuse snippets/editorial-text-content.liquid; the static heading passes disable_scroll_reveal=true and does not load the scroll script. Existing editorial blocks elsewhere retain scroll controls.

Display typography fix: heading tags map H1/display, H2/xl, H3/lg, H4/md, H5/sm, H6/xs, matching blocks/heading.liquid. Global responsive variables supply desktop/tablet/mobile Theme Settings sizes. Explicit size presets and custom sizes retain their own visual scale.

Global typography: Heading Display uses tag-specific H1-H6 global variables. Text now offers Display mapped to body-md (Paragraph Base size). Theme Settings Typography/Paragraph includes opt-in mobile size; global body-md switches at the existing 767.98px breakpoint. XS-XXL explicit scale values are unchanged. Browser verification of this update remains pending because local preview redirects to the store password page.

Basic block update: saved section name is Inline image text. Static eyebrow replaced by Text (XS default), preserving intro copy and spacing settings. Allow-list includes all 17 categorized Basic blocks discovered from current block schemas. Saved homepage heading Display and section padding from the development theme were preserved.

## Theme typography defaults

- All existing block font-size selects default to Display, including responsive size selects. Block presets and saved template/section-group typography values also use Display. Explicit manual size options remain available.
- `typography-size-token` resolves semantic H1–H6 to the existing heading tokens; body Display uses Paragraph (`--font-body-md`). Components without a heading tag retain their existing global heading role. Eyebrow and button text continue to inherit their dedicated global theme styles.
- Local Theme Check: 0 errors, 32 existing warnings. Shopify development CLI reports successful synchronization for changed blocks, presets, and JSON templates. Storefront visual/Theme Editor QA remains blocked by the storefront password page.
