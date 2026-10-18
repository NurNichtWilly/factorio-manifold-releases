# Optional Space Age logistics (v0.8)

Manifold still requires only Factorio base >= 2.0.77. Optional dependencies on `space-age` and `quality` enforce load order without requiring expansion ownership. Standalone Quality retains exact-quality transport, storage, crafting and regional requests. The following technologies exist only with Space Age:

| Technology | Additional science | Effect |
| --- | --- | --- |
| Vulcanus bulk logistics | Metallurgic | Doubles source/link capacity on Vulcanus; foundries expose their native item inventories to ordinary interfaces. Fluids remain in pipes. |
| Fulgora recycling logistics | Electromagnetic | Doubles source/link capacity on Fulgora. Attach ordinary input/output interfaces to native recycler inventories and use exact-quality filters to build physical recycling loops. Recycling yields remain engine controlled. |
| Freshness-aware logistics | Agricultural | Enables direct movement of plain perishables between physical inventories, with native freshness/quality preservation. |
| Aquilo transfer optimization | Cryogenic | Halves latency on Aquilo. Requires ordinary powered infrastructure; it creates no frozen storage. |
| Interplanetary material requests | Vanilla space science | Configure native cargo logistics on reachable friendly hubs and landing pads. |

These are optional branches after Smart Manifold logistics. No planetary science gates core storage, crafting, trains or the vanilla endgame.

## Perishables

After Freshness-aware logistics, inputs, buffers and physical storage buses may move plain perishable items into other physical inventories. Each source examines at most 32 slots per visit, preferring the oldest perishable among those sampled. An eligible plain nonperishable encountered first retains the existing dispatch behavior. The source warms up for its local latency, then uses the normal per-source and per-route admission/delivery budgets. Blocked goods stay in the source and continue to spoil. Native `transfer_stack` preserves quality and handles freshness merging; Manifold never recreates a perishable from an item name/count.

Destination visits examine at most 32 slots, honor inventory bars and native slot restrictions, filters, circuit enable conditions, priorities and stock targets. Destination cursors rotate to cover larger inventories. Spoilables never enter script packet inventories, portable storage cells, terminal deposits, crafting reservations or regional train reservations. Native inserters, rockets and platforms retain their normal spoilage behavior. Spoil products may subsequently use ordinary transport if supported.

## Cargo requests

Research Interplanetary material requests, select a friendly hub or landing pad within reach, then run `/manifold space`. Choose a slot (1–16), item, exact quality and stock target (up to 1,000,000). A target of zero removes that slot. Platform hubs may specify an import planet; landing pads receive native platform drops. Refresh displays actual inventory stock and configured native requests. Existing native logistics sections are preserved; Manifold allocates an ungrouped manual section. Assigning that section to a shared logistics group prevents further Manifold edits.

The engine maintains stock targets and cargo ordering. Build and fuel rockets, set platform schedules, provide supplies and use the native cargo UI to inspect pending deliveries. Manifold writes request filters; it does not create cargo, script cross-surface transfers or alter platform schedules. At most 64 live hubs/pads can have configured request records. Deleting an endpoint permits a new record at the next configuration attempt. Native sections and Manifold request references persist through save/reload.

The permission-checked remote calls are `space_configure(player_index, entity, {slot,item,quality,count,import_from})` and `space_inspect(player_index, entity)`. The latter returns configured requests with current stock plus a bounded sample of the first 32 cargo slots, including spoilage percentage. Configuration rejects invalid item/quality/location, count, slot, foreign force, distance, surface and missing research.

See RELEASE_0.8.md for actual acceptance evidence and limits. Native requests do not by themselves prove a complete launched rocket/platform voyage.
