# Achievement engine patch series

Start with upstream [EQEmu](https://github.com/EQEmu/EQEmu) commit **`c9c8747ac949deddb140d196d241fa4e777500c7`**. Patch0001 is the production subset of [PR5119](https://github.com/EQEmu/EQEmu/pull/5119), by **fryguy503**, pinned at head **`c68d0074bbc35974b6413c208c4523dd7fd21954`**. Upstream attribution and source licensing remain applicable. This patch is not designed for arbitrary older forks or a housing-modified local checkout.

Apply the five numbered patches in order from the EQEmu source directory:

```sh
git checkout c9c8747ac949deddb140d196d241fa4e777500c7
git apply /path/to/release/patches/0001-upstream-pr5119.patch
git apply /path/to/release/patches/0002-class-rewards-and-common-only.patch
git apply /path/to/release/patches/0003-council-destructible-and-ground-items.patch
git apply /path/to/release/patches/0004-unbound-component-completion-barrier.patch
git apply /path/to/release/patches/0005-shards-native-quest-support.patch
```

Patch0001 supplies definitions, state, progress, comparison, earned notification, reward selection, persistence, event hooks, repositories, commands, serializers and RoF2 mappings. Tests, test fixtures, example reward grants, the legacy ToB coverage report and its broad criteria repair SQL are excluded. The schema migrations remain included.

Patch0002 adds permanent-class reward eligibility, common-only claim authentication, cursor-persistence acknowledgement and two corrected skill IDs in the importer. Patch0003 supplies the destructible suffix/visibility and charged ground-item fixes needed by Crescent quest objects. Patch0004 prevents a partially authored definition from completing when only its mapped subset is satisfied. Patch0005 adds a lossless Lua shared-task instance identity and narrowly scoped NPC targeting permissions for the two Shards quest-item spells. The permissions require the exact item, spell shape, task activity, zone and eligible target; ordinary spell restrictions remain in effect. It includes no unrelated Spirit Shroud code. The matching [Shard’s Landing content package](content/shards-landing/README.md) supplies the tasks, focused quest hooks and installation guidance. Its provenance distinguishes native solo/single-member observations from additional isolated multiplayer checks, including Unspoken group ownership and the one-apparition limit.

Build the patched server using the upstream instructions for your platform. Apply both upstream achievement schema migrations (`2026_07_28_achievement_content.sql`, `2026_07_28_achievement_state.sql`) and the follow-up `2026_10_27_achievement_reward_classes.sql` to the server database before starting the new binaries. The first two are registered with the pinned upstream database updater; the added class-mask migration must also be applied explicitly. Back up the database before upgrading. Use the release's curated historical content overlay separately; importing a current Live client catalogue does not make it May2013 content.

This offline package passed `git apply --check` and sequential application of all five layers against the exact saved upstream changed-file preimages (plus the pinned unchanged `zone/zone.cpp` fetched for patch0003). A full clean-port Linux x86-64 build of both `zone` and `world` passed with GCC12.2, Release mode and upstream-default precompiled headers. Clean-port native validation remains pending. Native observations from the existing running local port validate that port, not this reconstructed build. `engine-provenance.json` records included/excluded files and patch digests.

The [protocol guide](protocol/README.md) provides mappings and packet layouts, including structures whose lengths depend on the catalogue. No client binaries/assets, raw client resource catalogues, captures, private character data, test files or housing/fellowship payloads are part of this package.
