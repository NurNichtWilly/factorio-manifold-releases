# v0.11.3 — 2026-10-18

- Recover pending crafting-transfer goods directly alongside job-owned stock, even when the job escrow is full.
- Report exact recovered/remaining counts and distinguish a full main inventory from having no character inventory.
- Preserve numeric recovery API compatibility; add read-only recovery status for integrations.
- Validate future release versions and reconcile immutable release artifacts before publishing.

# v0.11.2 — 2026-10-18

- Prepare the first public preview with an in-game/mod-portal thumbnail and current descriptions.
- Add illustrated player documentation and explicit compatibility/gameplay limitations.
- Package only runtime assets and player documentation; keep development sources and release distribution separate.
- Fix the vanilla crafting quality selector showing a missing translation instead of Normal.
- Preserve v0.11.1 gameplay and animation behavior.

# v0.11.1 — 2026-10-17

- Fix attached layers applying prototype and runtime speed twice (0.2×0.2, effectively 2.4fps).
- Replace coarse 12/24fps source loops with genuine 60fps scene sampling while preserving intended cycle durations.
- Match position and velocity at cycle boundaries; remove the encoder tape teleport with a covered continuous feed.
- Preserve moving-part and shadow phase when activity or electricity stops and resumes.
- Validate source seams and actual native cycle repetition; use correctly timed MP4/WebP previews instead of GIF for 60fps review.

# v0.11.0 — 2026-10-17

- Animate every machine family and all cosmetic views: tier-controller drives/impellers, pneumatic inlet/outlet hardware, buffer pointers, cassette access, punched-tape machinery, feed actuators, cooling fan and regional gyroscopes.
- Preserve fixed housings/manual controls, entity types, inventories and transport behavior; drive working actuators from committed material movement and pause offline machinery.
- Add 55 editable keyframed Blender views, 110 paired animation atlases, complete raster/prototype contracts and native per-view motion/power/save/clone acceptance.

# v0.10.1 — 2026-10-17

- Animate the basic controller flywheel and crank in four native directions with matching moving shadows.
- Use Factorio electrical activity to drive the 24-frame loop; preserve entity identity, power demand and network rules.
- Add editable keyframed Blender scenes, targeted rendering and native power/rotation/save-load visual acceptance.

# v0.10.0 — 2026-10-16

- Upgrade every hardware family with refined original Blender geometry, machined metal highlights, enamel accents and subtle wear.
- Replace tinted regional/advanced reuse with dedicated models; make all 18 item and 18 research icons distinct, including every technology rank and optional branch.
- Double world sprites/shadows to 256px at scale 0.25; preserve collision boxes, tile-edge alignment, native rotations/styles and save identities.
- Add tightly framed item icons, editable source models, global showcases and complete raster/prototype/native visual acceptance.

# v0.9.0 — 2026-10-16

- Add vanilla space-science advanced controllers/endgame conduits, native upgrade targets, 1 MW demand, eightfold capacity and six-tick minimum local latency.
- Compile unbranched conduit corridors into shared bidirectional capacity ledgers while preserving mixed-tier bottlenecks; defer sleeping packet endpoint reads.
- Add native 10,000-conduit benchmarks, differential accounting tests, optional-mode endgame checkpoints and archived v0.8 upgrade acceptance.
- Fix the cargo request GUI's reserved field names; add bounded request scrolling and permission-checked analyzer/space UI remote calls.

# v0.8.0 — 2026-10-16

- Add optional planet-specific logistics research, freshness-preserving native inventory transfers, and native hub/landing-pad cargo requests with configuration UI and permission-checked remote APIs.
- Preserve vanilla/standalone Quality, script-inventory spoilage restrictions, physical item ownership and player logistics sections.
- Add real-engine planet, request, freshness and checkpoint acceptance.

# Changelog

## 0.7.0 — 2026-10-16

- Regional coordinator and distributed-logistics research for physical freight between separate networks.
- Provider/requester/depot settings, exact item/quality matching, priorities, batch limits, supply reserves and inbound demand reservations.
- Live federation of staging-chest stock and separate reservation counts; shared chests/stops and duplicate stop names fail closed.
- Exclusive empty depot-train dispatch through provider, requester and home; real inserters and cargo wagons carry every item.
- Wagon capacity and requester space bound plans; power loss, changed endpoints, unexpected cargo and manual/schedule overrides pause safely.
- Native monitoring/configuration panel, cancellation with cargo retained, blueprint/clone settings and persistent train jobs.
- Existing original terminal artwork is reused with a regional blue tint.

## 0.6.0 — 2026-10-15

- Automatic discovery of selected recipes at the first 32 connected crafting interfaces; explicit encoding pins recipe and quality.
- Live recipe registry, deterministic duplicate handling and saved CPU preferences per item/quality; ambiguous machines and missing preferred recipes fail safely.
- Exact-quality dependency plans, physical reservations, machine feeds, product collection, storage returns and recovery; optional standalone Quality or Space Age.
- Production monitor with discovery diagnostics, completed/remaining crafts, elapsed time, last movement, escrow counts and native machine progress/status.
- Stable recipe buttons, progress bars and queue controls; quality survives encoded blueprints, clones and native saved jobs.
- Engine acceptance covers vanilla, Quality and Space Age, conserved real-machine production, quality changes, checkpoint replay and v0.5.1 upgrade.

## 0.5.1 — 2026-10-15

- Dedicated original Blender models, native sprites/shadows and item icons for storage bus, pattern encoder, crafting interface and crafting CPU.
- Separate smart-logistics and autocrafting research illustrations replace shared storage artwork.
- Three Astra art subagents produced editable scenes and reproducible generators integrated into the existing rendering pipeline.
- Existing entity identities, ports, collision geometry, inventories and crafting behavior are preserved.

## 0.5.0 — 2026-10-15

- Pattern encoder, crafting interfaces, crafting CPU and red/green-science autocrafting technology.
- Explicit assembling-machine patterns, recursive bounded dependency planning, physical material reservations and a 32-request production queue.
- Real machine ingredient feeds, product collection and storage returns share source/edge capacity and latency; no scripted crafting output.
- Normal-quality deterministic item recipes, missing-material/cycle/ambiguity rejection, cancellation, removed-CPU recovery and per-request status UI.
- Save/reload preserves reservations, plans and transfer escrow; pattern tags and cloning retain encoded recipes.

## 0.4.0 — 2026-10-15

- Configurable import/export, buffer, drive and bus filters, exact quality, destination priorities, stock targets and enable conditions.
- Storage buses expose adjacent physical chests with read/write access; terminal indexing deduplicates chests and retains real item ownership.
- Circuit conditions read the attached inventory’s red and green signals; filters, targets and conditions revalidate at delivery.
- Stock targets reserve in-flight deliveries, including immediate terminal deposits, without clearing stacks at zero remaining room.
- Native logistics configuration panel, blueprint tags, cloning and settings-paste persistence.
- Vanilla/Space Age logistics conservation, real save/reload and v0.3.1 transit-save upgrade verified.

## 0.3.1 — 2026-10-14

- Terminal and drive use actual Factorio container windows with native character inventories, machine preview, slots and inventory controls.
- Searchable storage is a native-style item grid with tooltips, quantities and stable buttons.
- Terminal has eight real deposit slots; supported items travel to installed cells with normal packet latency, bandwidth and full/offline backpressure.
- Drive has exactly four native cell slots at every quality, with optional native slot filters.
- Analyzer docks to native character/buffer windows and uses a compact two-column diagnostics panel. Controllers now open diagnostics on click.
- Terminal entity migration preserves existing cells, network escrow and topology through the 0.3.0 upgrade.

## 0.3.0 — 2026-10-14

- Native portable 16-/64-slot cells, four-bay storage drives and searchable paginated terminals.
- Cursor deposits, stack/one-item withdrawals, real capacity statistics and per-action power/reach/force/surface checks.
- Drives participate in delayed, bandwidth-limited transport; removed cells retain contents and orphaned packets stay recoverable.
- Native inventories preserve cell contents through mining, movement and save/reload; no hidden ownership ledger or destructive cell-upgrade recipes.
- Original Blender storage cabinet, console, cell icons and research illustration, with editable scenes.
- Vanilla/Space Age storage conservation, full-cell backpressure, metadata/spoilage policy, save/reload and v0.2 transit-save upgrade passed.
- Real-player and graphical terminal search, withdrawal, drive bay removal/reinsertion and Close/Escape verified.

## 0.2.0 — 2026-10-14

- Green-science reinforced controller/conduits, native upgrade targets and mixed-tier physical capacity.
- Three force-owned ranks each of bandwidth and latency research affect existing hardware.
- Original Astra-assisted Blender reinforced sprites/icons, research illustrations and editable scenes.
- Construction rebuilds affected components while unrelated networks continue transporting.
- Analyzer reports actual bottleneck capacity, researched minimum delay and tier power figures.
- Engine coverage for upgrade marking/replacement, research/reversal, mixed routes, rebuild restart, actual construction-robot completion, finite-stock conservation and researched save/reload.
- Graphical client verification caught and fixed mixed-edge bottleneck ties and custom research-effect icons.

## 0.1.3 — 2026-10-14

- Deterministic shortest paths with bounded search/reconstruction and a capped route cache.
- Shared bidirectional per-edge admission/delivery capacity; independent branches transport concurrently.
- Per-source admission credits and rotating priority for shared bottlenecks.
- Analyzer edge capacity, busy/congested connection IDs, measured utilization and capacity waits.
- Item-conserving topology reroutes and old-release transit-save upgrade validation.
- New pure Lua routing tests and actual branch/trunk engine fixtures.

## 0.1.2 — 2026-10-14

- Matte weathered metal art, fixed outdoor lighting and separate model-cast shadow layers.
- Native four-direction controller/interface rotation; round buffers have rotating gauge assemblies.
- Three input/output covers, conduit lids and buffer gauge variants, selected with Ctrl+Alt+V.
- Matching device fittings and topology-driven connectors meet conduits at tile boundaries.
- Cosmetic state persists through saves, cloning and tagged blueprint revival.
- Interfaces migrate to rotatable native simple entities; pending packet IDs are remapped without recreating item stacks.

## 0.1.1 — 2026-10-14

- Original Blender controller, conduit, input, output and buffer models, sprites and icons.
- Original research illustration, editable models and deterministic render tooling.
- Sixteen native conduit connection variants reflect actual device adjacency.
- Conduit type migration tested with v0.1.0 in-transit items and save/reload.
- Original code and artwork use the MIT license.

## 0.1.0 — 2026-10-14

- Initial red-science transport network with powered controller, copper conduits, interfaces and physical buffers.
- Real inventory-backed packets, minimum latency, integer shared bandwidth and bounded scheduling.
- Connectivity rebuilds, blocked/orphaned packet handling and explicit recovery.
- Native diagnostics, measured throughput/latency, English locale and startup transport settings.
- Isolated Lua/engine validation, real save/load fixtures, expansion smoke tests and release packaging.
- Long-term design, architecture, progression and test documentation.

Storage buses, configurable filters and autocrafting are deferred. Interface GUI interaction and local-player recovery have been visually verified. Multiplayer validation remains outstanding.
