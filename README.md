# Promise Infra diagrams (local)

On-prem architecture diagrams that render on your machine. No SaaS account.
The model is [LikeC4](https://likec4.dev/) (TypeScript CLI). Sequences can also
be [Mermaid](https://github.com/mermaid-js/mermaid).

`/tmp` is wiped on reboot. Copy this folder somewhere durable before you rely on it:

```sh
cp -a /tmp/sample-infra ~/Projects/sample-infra
```

## Preview

```sh
cd /path/to/sample-infra
npm install
npm start
```

Opens a local LikeC4 server (hot-reload). Edit `model/*.c4` and the browser updates.

## Export

```sh
npm run export:png          # PNG per view into ./export
npm run build               # static site into ./site
npx likec4 gen mermaid      # Mermaid from the same model
```

Optional Mermaid-only render (needs Chromium via mermaid-cli):

```sh
mkdir -p export
npm run mermaid
```

## What lives where

| Path | Job |
| --- | --- |
| `model/spec.c4` | Element kinds, tags, relationship kinds |
| `model/logical.c4` | C4 landscape (actors, systems, services) |
| `model/deploy.c4` | On-prem zones, VMs, Kubernetes |
| `model/views.c4` | Landscape, zoom, sequence, blast, deploy views |
| `mermaid/` | Hand-written sequences if you do not want LikeC4 dynamic views |
| `.cursor/skills/infra-diagrams/` | Agent skill that generates and edits these files |

## Cursor skill on this machine

Copy the skill so any local repo can invoke it:

```sh
mkdir -p ~/.cursor/skills
cp -a .cursor/skills/infra-diagrams ~/.cursor/skills/
```

This Cursor home also accepts:

```sh
cp -a .cursor/skills/infra-diagrams ~/.cursor/skills/ 2>/dev/null || true
```

Ask the agent for a C4 view, a VLAN/VM map, a Kubernetes topology, a request
sequence, or a blast-radius overlay. It should read the skill and edit the model
instead of inventing a one-off drawing.

## Libraries (all local, all open source)

- [LikeC4](https://github.com/likec4/likec4) (MIT): architecture-as-code, preview, PNG/Mermaid/D2 export
- [Mermaid](https://github.com/mermaid-js/mermaid) (MIT): sequences and Markdown embeds
- [@mermaid-js/mermaid-cli](https://github.com/mermaid-js/mermaid-cli) (MIT): `mmdc` SVG/PNG from `.mmd`

Do not add a third renderer unless LikeC4 and Mermaid cannot express the diagram.
