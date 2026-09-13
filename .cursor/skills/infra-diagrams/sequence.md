# Sequences / hop maps

Two renderers, one story.

| Need | Tool |
| --- | --- |
| Same model as the C4 views, toggleable sequence layout | LikeC4 `dynamic view` |
| Markdown, Git, or `mmdc` SVG | `mermaid/*.mmd` |

Use both when the user will publish a doc **and** keep the architecture model. Keep hop names identical.

## Completion

Done when every hop is a **leaf** (component, database, queue) and the named view or `.mmd` lists the calls in order, including the response if they asked for it.

## LikeC4

```
dynamic view buy_confirm {
  title 'Buy confirm sequence'
  customer -> promise.panel.ui 'opens Panel'
  promise.panel.ui -> promise.edge.nginx 'POST /buy/confirm'
  promise.edge.nginx -> promise.edge.haproxy 'forward'
  promise.panel.ui <- promise.panel.api '200'
}
```

- Sequence layout: LikeC4 UI control, or `likec4 export` / serve with `--sequence`.
- Continuous form is allowed: `A -> B -> C` (a later `A` is a return).
- `parallel` / `opt` / `alt` when the user described those branches.

## Mermaid

`mermaid/buy-confirm.mmd`: `sequenceDiagram` + `autonumber`. Render with `npx mmdc -i mermaid/buy-confirm.mmd -o export/buy-confirm.svg`.

## Do not

- Point a step at `promise.panel` if `panel` has children. Use `panel.ui` / `panel.api`.
- Invent hops that are not in the logical model. Add the component first.
