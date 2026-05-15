---
name: grid-composition-design
description: Design and audit typography-led visual compositions using CSS Grid, editorial proportions, section-level grid contracts, responsive rhythm, and screenshot/geometry validation. Use when creating or refining landing pages, editorial pages, reports, dashboards, visual essays, Figma-to-code layouts, or any UI where typography, grids, proportions, hierarchy, whitespace, and visual consistency matter.
---

# Grid Composition Design

Attribution: created from DesignAnswers Composer responsive-grid experiments by Vitali Gusatinsky / DesignAnswers.

Use this skill to make visual compositions feel deliberate rather than assembled. It is for typography-led layouts, editorial pages, data/report pages, visual essays, dashboards, and UI sections where grid, proportion, rhythm, and hierarchy carry the design.

## Working Loop

1. State the composition thesis: what should dominate, what supports it, and what should recede.
2. Map the content hierarchy before touching spacing: title, kicker, body, modules, rails, notes, sources, actions.
3. Pick one page frame grid and one section contract per section.
4. Build or revise the CSS with named grid lines, consistent spans, and proportional gutters.
5. Capture desktop, tablet, and mobile screenshots. Use geometry measurements when a layout claim matters.
6. Keep changes only when the screenshots and measurements show clearer hierarchy, fewer loose elements, and no overflow.

For review-heavy tasks, read [references/audit-checklist.md](references/audit-checklist.md).
For visual precedents from the Composer work, read [references/example-gallery.md](references/example-gallery.md) and inspect `assets/examples/` only when helpful.

## Composition Principles

Start with visual weight, not components.

- The dominant idea of a section should be obvious in one glance.
- Headings must dominate the modules they introduce. If numbers, charts, cards, or images feel louder than the title, scale or span the title up.
- Whitespace should group related material and separate unrelated material. Large gaps inside a component are usually a bug; large gaps between sections can be intentional.
- Repeated modules inside one section need one grammar. Equal items should use equal spans, equal rhythm, and equal treatment.
- Avoid decorative complexity that does not increase comprehension.

## Grid Model

Use layered grids instead of one overloaded grid.

- Page frame: define only `full-start`, `content-start`, `content-end`, `full-end`.
- Content grid: define the 12/8/4 columns inside each content region.
- Full-bleed bands may span `full-start / full-end`, but their inner content must return to the same content inset and column contract.
- Do not put `column-gap` on an outer frame that also has flexible outer gutters; it creates overlay drift.
- Use `minmax(0, 1fr)` for flexible tracks.
- Use subgrid when nested elements need to align to the section columns.

Preferred responsive contract:

```css
.page {
  --outer: clamp(1rem, 4vw, 4.5rem);
  --content-max: 77rem;
  --page-inset: max(var(--outer), calc((100vw - var(--content-max)) / 2));
  --content-inline: calc(100vw - (2 * var(--page-inset)));
  display: grid;
  grid-template-columns:
    [full-start] var(--page-inset)
    [content-start] minmax(0, var(--content-inline))
    [content-end] var(--page-inset)
    [full-end];
}

.section {
  grid-column: content-start / content-end;
  display: grid;
  grid-template-columns: repeat(12, [col-start] minmax(0, 1fr) [col-end]);
  column-gap: var(--gap);
}
```

At tablet/mobile, change the section contract to 8/4 columns and remap modules consistently.

## Section Contracts

Give each section a clear internal grammar.

- Repeated grids must balance final rows. Do not leave a single orphan item unless it is deliberately promoted as a feature.
- A six-item ledger should usually be `3 x 2` on desktop, `2 x 3` on tablet, and one column on mobile.
- Avoid odd/even alternation within a section unless the asymmetry is the concept. If row 1 uses 3-up equal modules, row 2 should not suddenly use 2-up wide/narrow modules.
- Side rails, source rails, timelines, and marginal navigation need independent rhythm. Do not stretch them to the full article height unless they are explicitly a full-height axis.
- Sticky elements must remain useful for the full range where they appear. A sticky nav visible only for the first slice reads as broken; make it static or redesign the section around it.

## Typography And Rhythm

Use type scale and line-height to create cadence.

- Display type should have tight leading and strong weight, but must fit its assigned span.
- Body text should be dense enough to scan: avoid loose line-height and overly wide measures.
- Body measure should usually stay in the 45-75ch range; narrower side notes can be shorter.
- Define vertical spacing as named multiples or clear fractions of the base line height before tuning one-off modules.
- Use the same rhythm ladder for section padding, row gaps, paragraph spacing, placeholder heights, aside offsets, and repeated module heights.
- Do not let labels and descriptions drift far apart inside a module. A title-to-copy gap around one line-height often reads better than `space-between` in tall boxes.
- If a module has a large internal empty field, either add meaningful content or reduce the block size.

## Border Economy

Use borders as structure, not decoration.

- Prefer one shared section rule or one entry rule over boxed grids around every item.
- Remove fake graph-paper backgrounds unless the content is actually a chart, matrix, or coordinate field.
- Avoid vertical dividers between every stat unless comparison requires them.
- If borders are doing the work of alignment, fix the grid instead.
- A sparse editorial layout usually improves when border density goes down and span logic gets clearer.

## Visual Modules

For stat blocks, source ledgers, timelines, and visual placeholders:

- Stat rows: numbers can dominate, but the section title must still establish the context. Keep stat cards equal unless one is intentionally featured.
- Source ledgers: balance rows, use equal widths, and keep metadata compact.
- Timelines: use a compact intrinsic rhythm, a clear side rail, and enough gap from prose to read as secondary.
- Asides: give side prose, marginal comments, source notes, and timeline rails a consistent secondary contract: smaller type, compact leading, a quiet entry rule or offset, and enough separation from primary prose.
- Visual placeholders: give rectangles equal section-level heights derived from the rhythm ladder. Use quiet fills plus stable label/copy placement, and replace placeholders with real visual material when available.
- Dark sections: check heading contrast and hierarchy against numbers; dark backgrounds amplify weak spacing decisions.

## Responsive Rules

Do not only make the layout fit. Make each breakpoint have a coherent composition.

- Desktop: 12-column contracts, generous separation, side rails allowed.
- Tablet: 8-column contracts, side rails usually move below or become compact rows.
- Mobile: 4-column contracts. Compact modules can use `span 2`; dense prose often spans all 4.
- Do not keep desktop odd/even placement rules on mobile if they produce visual noise.
- Check text fitting at common widths: 390, 768, 1440, and one wide desktop size.
- Watch high-specificity desktop exceptions at mobile. Section-specific rules such as `#friction .section-title` need explicit tablet/mobile overrides so they do not escape into the 8/4-column contracts.

## Validation

Before signing off, provide evidence.

- Screenshot the relevant viewport(s), not only the full page.
- Inspect overlay or bounding boxes when claiming alignment.
- Check `document.documentElement.scrollWidth - window.innerWidth` for overflow.
- Measure repeated module rows: row populations, widths, and gaps.
- Confirm section titles are not visually smaller/weaker than the modules they introduce.
- Run lint/type checks available in the project.
- If a browser tool fails from sandboxing, request escalation and rerun outside the sandbox.

Report the result with file paths, screenshots, and the specific before/after measurements that prove the composition improved.
