# Grid Composition Audit Checklist

Use this checklist when reviewing or refining a visual composition.

## Hierarchy

- Identify the dominant element in each section.
- Verify heading scale, span, and placement dominate repeated modules below it.
- Check that labels, captions, and source notes recede without becoming illegible.

## Grid Contract

- Name the page frame lines and content region lines.
- Verify full-bleed sections return to the same content inset internally.
- Verify repeated modules in a section use one consistent span pattern.
- Look for accidental remainders: 5+1, 3+1, or lone final-row cards.

## Vertical Rhythm

- Compare top spacing, heading-to-body spacing, module spacing, and section exits.
- Flag modules using `align-content: space-between` when it separates title and copy too much.
- Flag side rails stretched to match unrelated content height.
- Check that section-to-section rhythm is intentional, not determined by incidental module heights.

## Border And Chrome

- Count borders/rules in the viewport. If every object has a line, the lines no longer communicate hierarchy.
- Remove graph-paper, boxed-card, and divider treatments that are not carrying information.
- Prefer fewer stronger rules: section entry, group boundary, or actual table/grid axes.

## Responsive Checks

Measure these at minimum: 390, 768, 1440, wide desktop.

- Overflow is zero.
- Track count matches the intended breakpoint contract.
- Text fits without awkward clipping or extreme measures.
- Repeated module rows are balanced at each breakpoint.
- Side rails move or compress when the content column becomes too narrow.

## Useful Browser Measurements

Use page evaluation or devtools to capture:

```js
({
  overflow: document.documentElement.scrollWidth - window.innerWidth,
  items: Array.from(document.querySelectorAll('.module')).map((el, index) => {
    const r = el.getBoundingClientRect();
    return { index: index + 1, x: r.x, y: r.y, width: r.width, height: r.height };
  }),
});
```

For row balance, group by rounded `y` values and ensure no row has one item unless intentionally featured.
