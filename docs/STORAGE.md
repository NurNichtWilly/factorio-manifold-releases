# v0.3 storage ownership and integration

Cells are engine-owned `item-with-inventory` stacks, not serialized item counts. A cell's `item_main` inventory is its sole storage owner; the drive chest owns the removable cell item. The runtime stores only references for in-flight packet endpoints, never a duplicate cell-content ledger. Capacity is 16/64 inventory slots with normal per-item stack limits; four cells fit in a drive. Cell quality does not expand slots. Recipes for larger cells use raw materials and cannot consume a full smaller cell.

An automated transfer removes a plain stack into real one-slot escrow, then inserts into the chosen inventory after route capacity, network power and latency checks. Drive packet endpoints record the exact native inventory. If that inventory is no longer installed in that drive, the packet becomes recoverable for its admission force. Reinstalling a cell does not change ownership of orphaned packets. Surface/force isolation comes from topology; access requires the drive's live force and terminal's surface. Cells themselves are portable between forces via actual physical item movement.

Manual terminal transfer is immediate and synchronous. Destination insertion determines the committed quantity; only that quantity is removed from the original cursor/cell stack. Full inventories retain remainders. Actions are capped at one normal stack per withdrawal; deposits are at most the held stack. Each terminal interaction scans at most 32 stable-ID drives, four bays each, up to 64 slots per cell. The GUI warns about additional drives. Periodic row updates retain widgets when item identities stay the same; search and page changes rebuild only the displayed rows.

Native mining transfers complete cell stacks and their inventories to the mining inventory. Native destruction, surface deletion, item destruction or removing the mod can destroy contents just like ordinary Factorio goods. Only packet escrow has an independent recovery path. Unknown or unsupported contents are retained in native inventories and included in overall occupancy/item statistics; automated transport and terminal withdrawal expose only supported plain stacks.

The final prototype whitelist includes only nonspoilable `item` prototypes. Item-with-inventory, ammo, tools, tagged items and other item subclasses cannot nest inside cells. Runtime transport also rejects damaged/extra-data stacks. This avoids freezing spoilage and losing metadata; relaxing those rules is later work.

## Remote interface

The existing `manifold.inspect()` remains read-only. Three optional integration calls share the exact GUI access/transaction rules:

- `storage_inspect(player_index, terminal_entity)` returns `status`, `cells`, `slots`, `used`, `items`, `limited` and sorted `contents` rows `{name, quality, count}`. Inaccessible networks return zero contents and their status.
- `deposit_cursor(player_index, terminal_entity)` returns the actual moved count, leaving any remainder in the cursor.
- `withdraw(player_index, terminal_entity, item_name, quality_name, amount)` returns the actual moved count, capped to a normal stack. A nonpositive or NaN amount does nothing. Goods go into that player's main inventory.

These interfaces act only on real players, reachable same-force terminals and online networks. Third-party scripts remain trusted Factorio mods; this API does not create a security boundary between mods. GUI sessions are player-owned and removed when the player/entity is removed or inaccessible. No on-load mutations were added. Configuration changes initialize the new GUI-session field and rebuild topology without resetting existing packet inventories.

## v0.3.1 native machine windows

The terminal is now a native container with eight physical deposit slots. It is a scheduled source that routes only to installed drive cells, obeying ordinary powered route capacity, latency, full-cell backpressure and orphan recovery. Its physical inventory is not counted as stored cell capacity. Unsupported items remain in the terminal; native mining/destruction follows vanilla rules. Drive quality does not expand its four bays. Native player inventory controls move complete cells, and optional native slot filters can reserve bays for cell types.

Storage UI is a relative panel anchored to the actual container window. Escape/E, native Close, entity changes and configuration changes clean up the player-owned panel. Withdrawals use a grid of Factorio slot buttons with translated tooltips. Existing cells and their native content inventories are unchanged. The same-name terminal entity migration changes its engine type; configuration scanning discovers the replacement and rebuilds topology while retaining cell inventories and packet escrow.

## v0.4 physical storage

Storage buses add adjacent native chest inventories to the terminal window alongside cells, with deduplication and read/write policies. The window is bounded to the first 32 drives plus 32 buses. Configure filters, exact quality, destination priorities, targets and circuit conditions through the endpoint's Configure button. See LOGISTICS.md and RELEASE_0.4.md for semantics and acceptance evidence.
