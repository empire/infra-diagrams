# Local open-source stack

Default: **LikeC4**. Sequences also **Mermaid**. Install from npm onto the machine. No account.

## LikeC4 (MIT)

- Package: `likec4` (CLI + TS config). Sample pins `1.59.3`.
- Preview: `npx likec4 start` or `npm start`.
- Check: `npx likec4 validate`
- Export: `npx likec4 export png -o ./export`
- Also: `npx likec4 build ./site`, `npx likec4 gen mermaid`, `npx likec4 gen d2`
- Config: `likec4.config.ts` with `defineConfig` from `likec4/config`
- Docs: https://likec4.dev/ · source: https://github.com/likec4/likec4

Node 20+ (sample verified on Node 24).

## Mermaid (MIT)

- Hand-written: `mermaid/*.mmd`
- CLI: `@mermaid-js/mermaid-cli` (`mmdc`). Pulls a browser. Skip if the user only needs the LikeC4 preview.
- Use for `sequenceDiagram` and Kubernetes flowcharts the C4 model should not absorb.

## Allowed extras (only if LikeC4 + Mermaid cannot do the job)

| Package | When |
| --- | --- |
| `elkjs` | Custom SVG layout in an existing site (Milli blast-radius style) |
| D2 (`npx likec4 gen d2`, then the D2 CLI) | The user asked for D2 source |

## Do not add

- Closed SaaS diagram hosts as a required step (Lucid, IcePanel cloud, paid Structurizr).
- Python `diagrams` / Graphviz as the default. The user asked for JS/TS.
- A new icon kit when `tech:` / `bootstrap:` on LikeC4 already has the shape.

## Install (this sample)

```sh
npm install
npm start
```
