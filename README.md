# EQEmu RoF2 achievements

A source release of the **RoF2 achievement engine, opcode mappings, packet layouts and reward selection support**. It targets the May10,2013 RoF2 client and a pinned EQEmu source baseline.

This first milestone supplies the engine and protocol. It does **not** claim that every achievement or quest through Rain of Fear is playable. The separately researched historical catalogue currently admits254 identities; quest content and historical coverage will be released as reviewed milestones rather than bundled with unfinished work.

## What is included

- Achievement definitions, primary state, progress updates, comparisons and completion notifications.
- Persistent achievement/task reward selection, permanent-class filtering and common-only reward claiming.
- Event hooks and quest APIs for authoring criteria.
- **All12 achievement/reward opcode mappings**, a standalone packet-prefix header, variable layout documentation and canonical serializer source excerpts.
- Four ordered production patches, provenance and the upstream license. No tests, captures, client assets or private runtime records.

## Install

Read [ENGINE.md](ENGINE.md) for the exact source commit, patch order, schema migrations and build instructions. This is a source upgrade requiring a server rebuild; it is not a binary drop-in or a complete content/database replacement.

Start with upstream commit `c9c8747ac949deddb140d196d241fa4e777500c7`. Apply these in order:

1. `patches/0001-upstream-pr5119.patch` — achievement/reward engine and RoF2 protocol.
2. `patches/0002-class-rewards-and-common-only.patch` — class eligibility, common-only claims and persistence corrections.
3. `patches/0003-council-destructible-and-ground-items.patch` — quest-object rendering and ground-item charges.
4. `patches/0004-unbound-component-completion-barrier.patch` — prevent partially mapped definitions from falsely completing.

Apply the schema migrations before launching patched binaries. See [the protocol reference](protocol/README.md) for the opcode table and structures. [engine-provenance.json](engine-provenance.json) lists exact file scope and patch digests.

## Verification

Each layer passed sequential patch-application checks against the pinned source preimages. The current running local port has native achievement/reward observations. The four-patch series built both `zone` and `world` successfully from a clean pinned checkout on Linux x86-64 using GCC12.2, Release mode and upstream's default precompiled headers. Native gameplay on this reconstructed clean-port build remains pending; existing local-port observations are a separate claim.

## Attribution

The engine originates in [EQEmu PR5119](https://github.com/EQEmu/EQEmu/pull/5119) by **fryguy503**, pinned at `c68d0074bbc35974b6413c208c4523dd7fd21954`. Follow-up changes were prepared during this project's RoF2 achievement restoration. The upstream EQEmu source is licensed under [GPLv3](LICENSE); retained upstream notices and license terms apply. See [ATTRIBUTION.md](ATTRIBUTION.md).
