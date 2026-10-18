# Autocrafting — v0.6

Research Manifold autocrafting after Smart Manifold logistics and Automation 2: 200 red/green packs at 30 seconds. The encoder, crafting interface and CPU each cost ten steel plates and ten advanced circuits, taking three seconds. All are one-tile conducting network components with original graphics. The controller gates network operation; machines need their own electricity.

## Build and request

1. Connect exactly one CPU, an encoder, storage and a terminal to a powered network.
2. Put a crafting interface directly beside each assembler. Exactly one assembler may touch each interface. Multiple adjacent machines reject discovery and encoding; allow up to one second for endpoint refresh after placement changes.
3. Choose recipes in native machine windows, remove modules and empty machine inputs/outputs. The encoder automatically discovers selected supported recipes on the first 32 interfaces. **Encode attached machine recipe** optionally pins the selected recipe and quality. A changed pinned recipe pauses discovery until restored or re-encoded. Existing v0.5 name-only encodings mean normal quality.
4. Supply supported ingredients in cells or readable bus chests. Filters, circuit conditions and access policies apply.
5. Open **Crafting requests** from a terminal, CPU, encoder or interface, or use `/manifold craft`. Choose an item, an unlocked quality and 1–1,000 additional items. Vanilla has normal quality. Standalone Quality and Space Age are independently supported.
6. If multiple recipes make a needed item, click the desired recipe in the registry. This saves a CPU preference for that item and quality, including dependencies. **Clear preference** restores automatic selection when only one recipe exists. A missing preferred recipe rejects new requests; it never silently falls back. Duplicate machines for one recipe use the lowest interface ID. Selection does not load-balance machines or change recipes.
7. Watch machine diagnostics and job progress. Products and unused stock return to writable storage with room.

For four normal transport belts, select normal gear and belt recipes in two assemblers, store six normal iron plates and request four normal belts. Two gear crafts precede two belt crafts. For rare belts, select rare recipes at both machines, store six rare iron plates and choose rare in the request panel. Existing intermediates of the requested quality reduce dependency work; existing final products never satisfy an additional-production request.

Recipe preferences belong to the physical CPU and survive native saves/configuration changes. They are not copied by blueprints or CPU cloning. Explicit interface encodings retain both recipe and quality in native blueprint tags and clones. Jobs keep immutable plans; changing preferences affects only new requests. Automatic discovery reads selected recipes; it neither searches every force recipe nor sets machine recipes.

## Production monitoring

The live registry displays the selected quality's recipes and marks unresolved ambiguity. Machine rows show attached entity IDs, usable recipes, discovery/encoding failures and native craft progress. A cap warning appears above 32 interfaces. Hover a job for its waiting reason, exact quality, completed and remaining machine crafts, elapsed seconds, seconds since the last item transfer/completed craft, physically counted escrow/transit, attached machine and actual machine progress/status. Progress bars count machine crafts rather than wall-clock estimates. These are not output-rate predictions or completion deadlines.

Offline local jobs remain visible/cancellable, but offline inspection exposes neither external stock nor discovered recipes. Completed elapsed time freezes at completion. v0.5 jobs retain their remaining plans; completed-craft counters begin when upgraded, since v0.5 did not record that history.

## Physical reservations and transport

A bounded planner checks all dependencies before moving goods. Missing stock/patterns, cycles, recipe ambiguity and limits reject without inventory mutation. Stock is counted only at the exact requested quality. Every dependency recipe must match that quality; lower-quality ingredients or patterns cannot substitute.

Reservation transfers real supported stacks into a 128-slot engine-owned job inventory synchronously. The initial reserve may require at most 96 slots. Reserved goods leave storage and cannot be spent twice. Surplus intermediates are reused; excess products return physically. Machine feeds, collection and returns use one escrow stack per job, shortest routes, shared bidirectional edge/source capacity and tier/research latency. Delivery credits debit only actual insertion. Return targets account for matching item/quality transfers already admitted.

Machines receive one craft's ingredients at a time and own delivered goods until collection. Manifold never manufactures scripted products, advances machine progress or supplies energy. Keep external inserters/players away from assigned inventories. Exclusive machine ownership prevents competing jobs from spending one machine's production. Each job runs dependencies sequentially; independent machines can service separate jobs.

## Interruptions, cancellation and recovery

Controller power loss or disconnected routes pause transfers; a supplied machine can continue its real craft. Changing recipe **or recipe quality**, adding modules or positive quality effects pauses subsequent work and pending feeds. Restore the job's recipe/quality without modules to resume. A removed interface requires cancellation or restoring that original entity; a replacement gets a new ID.

Cancel returns uncommitted escrow to storage. Goods already delivered to a machine remain there; an active craft can finish. Empty that machine before assigning another job. Full destinations retain goods in escrow. Removed CPU/surface or changed ownership orphans its jobs for the recorded force. `/manifold recover` and analyzer recovery transfer remaining job goods into the player's native inventory, preserving exact quality. Full inventories retain any remainder. Replacing a CPU does not adopt old jobs.

Native machine destruction can destroy machine-owned items. No replacement stock is invented. Recover/finish jobs before removing the mod: disabling it deletes its engine-owned inventories.

## Bounds and supported scope

- 32 retained jobs globally; eight serviced per six ticks. Empty finished history retires on the next request.
- First 32 interfaces, 32 drives and 32 buses by stable ID. Split larger networks.
- Depth 16, 256 demand visits, 64 steps, 4,096 crafts and 96 initial reserve slots. Oversized requests reject before reservation.
- One deterministic plain, nonspoilable item result and one to eight plain, nonspoilable item ingredients. Normal and available unlocked qualities use the same exact-quality rules.
- No fluids, furnaces, probabilistic/byproduct recipes, spoilables, modules or positive quality bonuses. Random quality upgrades are not supported. No automatic machine recipe assignment, alternative-route/load-balanced production or global factory discovery.
- Multiplayer ordering is deterministic by construction, but two-client join/desync tests remain unverified.

## Integration API

The `manifold` remote interface exposes:

- `crafting_encode(player_index, interface)` pins the selected recipe/quality.
- `crafting_request(player_index, device, item_name, additional_amount, quality_name?)` defaults to normal; returns job ID/reason.
- `crafting_prefer(player_index, device, item_name, recipe_name_or_nil, quality_name?)` sets/clears a CPU recipe preference for new requests.
- `crafting_inspect(player_index, device, quality_name?)` returns the live registry, alternatives/preferences, machine diagnostics, interface cap warning and bounded job rows with measured progress and physically counted contents/transit.
- `crafting_cancel(player_index, device, job_id)` cancels locally, including offline.
- `recover(player_index)` transfers only that force's recoverable goods.

Mutation requests recheck player reach, force/surface ownership, online network and one CPU. Inspection checks reach/ownership, with local job visibility offline. No writable inventory references escape through the API. Interface discovery requires an encoder; already encoded patterns retain their existing v0.5 operation if the encoder is removed.
