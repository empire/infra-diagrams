---
name: infra-diagrams
description: Generates on-prem infrastructure diagrams locally with open-source TypeScript (LikeC4, Mermaid). Use when the user asks for C4, network/VLAN/VM maps, Kubernetes topology, request sequences, blast-radius overlays, architecture-as-code, Promise infra diagrams, or a local diagram preview.
---

# Infra diagrams (local)

Generate diagrams from a **model**, then preview on this machine. Do not invent a one-off SVG or a SaaS embed when LikeC4 or Mermaid can express the picture.

Default tree (this skill ships with a sample at the repo root):

- `model/*.c4` — LikeC4 specification, logical C4, deployment, views
- `mermaid/*.mmd` — sequences you want in Markdown or `mmdc`
- `likec4.config.ts` — project name

If the user is not already inside a LikeC4 tree, create one beside their infra notes (copy this sample, or `npx likec4` in an empty folder) and keep working files out of `/tmp` unless they asked for `/tmp`.

## Pick a branch

| User asks for | Read | Write |
| --- | --- | --- |
| C4, landscape, containers, dependencies | [c4.md](c4.md) | `model/logical.c4`, a `view` / `view of` |
| Network, VLAN, VM, zone, rack, CIDR | [network.md](network.md) | `model/deploy.c4`, a `deployment view` |
| Kubernetes, ingress, namespace, workload | [k8s.md](k8s.md) | deployment nodes under `kubernetes`, plus optional `mermaid/*.mmd` |
| Sequence, hop, call flow | [sequence.md](sequence.md) | `dynamic view` and/or `mermaid/*.mmd` |
| Blast radius, failure domain, "if X is down" | [blast.md](blast.md) | tagged elements and a named blast `view` |

Stack rules and install commands: [libraries.md](libraries.md).

## Steps

1. **Name the picture.** One sentence: what fails, who talks, which zone, or which hop. If the user gave inventory, use their names and CIDRs. If they did not, keep the Promise sample fictional (`10.50.0.0/16`) and say so.
2. **Open the matching reference** from the table. Follow that file's completion criteria before drawing a second kind.
3. **Edit the model.** Add kinds only in `specification`. Add logical parts in `model`. Add machines and clusters in `deployment` via `instanceOf`. Add a **named view** for every picture you owe the user.
4. **Preview.** From the project root:

   ```sh
   npm install
   npm start
   ```

   `npx likec4 validate` must pass before you call preview done. LikeC4 serves a local page and hot-reloads `*.c4`.
5. **Export only if asked.**

   ```sh
   npx likec4 export png -o ./export
   npx likec4 gen mermaid
   ```

   For a hand-written `.mmd`: `npx mmdc -i mermaid/<file>.mmd -o export/<file>.svg`.

## House rules

- One model, many views. A new diagram is a `view`, not a second copy of the services.
- Leaf elements only on sequences (no parent box as a hop endpoint).
- Tags (`#uses-redis`, `#critical-path`) drive blast views. Do not color a one-off view and leave the model untagged.
- Open-source JS/TS only, runnable offline after `npm install`. LikeC4 first, Mermaid for sequences and Markdown. See [libraries.md](libraries.md) before adding a package.
- Do not paste live secrets, real customer data, or a full production inventory into a sample unless the user asked to diagram that inventory.
