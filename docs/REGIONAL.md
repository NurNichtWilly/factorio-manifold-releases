# Regional and train logistics

v0.7 coordinates physical freight between separate Manifold networks on the same surface and force. It never moves goods directly between regions. Reservations and schedules are metadata; chests, inserters and cargo wagons retain all physical ownership.

## Set up three stops

Research **Distributed logistics** after Smart logistics and Automated rail transportation. Craft a **Regional coordinator**, place it on the local conduit grid with exactly one powered controller, and open it normally or with Ctrl+M. The coordinator has a dedicated gyroscopic routing-relay model and icon.

1. At the supply region, place a coordinator next to exactly one ordinary or logistic staging chest. Enter the exact name of a unique train stop within 32 tiles. Choose **Provider**, a plain item, its exact quality, the maximum dispatch batch and the stock reserve to retain. Enable coordination.
2. At the destination region, configure another coordinator and staging chest as **Requester**, with the same item/quality, a stock target, batch limit and optional priority. Requester free chest capacity also limits admission.
3. At a depot, connect another coordinator to a powered local network, choose **Depot**, enter the unique home stop name and enable it. A depot does not need a staging chest.
4. Park a fueled automatic cargo train at that depot. Its schedule must contain only the home stop, with a long wait condition; it must have no group, interrupts or fluid wagons. It must be empty and contain one to eight cargo wagons. This is the explicit enrollment arrangement. Other trains are left alone.
5. Build rails, signals and ordinary inserters to load from the provider chest and unload into the requester chest. Connect staging chests to their local Manifold inventories with existing buses or input/output interfaces. A coordinator does not provide an additional local transport endpoint.

The planner selects matching online providers and depot trains, reserves supply and inbound demand, and assigns **provider → requester → depot**. Priorities descend, with entity IDs breaking ties. Batch size is bounded by missing stock, supply above reserve, both endpoint batch limits, free requester space and actual wagon capacity including bars/filters. A train is assigned to only one active transfer.

The provider stop waits until the requested exact-quality quantity is physically aboard. The requester waits until the train is empty. Returning home restores its original single-stop schedule and permits another dispatch. For point-to-point rails, use compatible station directions and bidirectional trains; the mod does not build routes or fuel trains.

## Monitoring and recovery

Every reachable coordinator shows a same-force, same-surface federation of physical staging stock, separate inbound/outbound reservations, endpoint status and active transfers. Counts are read from live inventories, without duplicate backing storage. Shared staging chests or train stops are rejected. Duplicate stop names on the same force/surface reject routing; distant or missing stops reject too.

Power loss, disconnected networks, removed/replaced endpoints, mixed cargo, manual train control, edited schedules and no-path conditions retain reservations. Restore the original conditions to resume, or cancel at a surviving endpoint/depot coordinator. Jobs stalled for five minutes are flagged and retain their reservations. Cancellation restores the original schedule **in manual mode**, preserving partially loaded cargo for the operator. It does not return or destroy items. Destruction or splitting of the original train releases its planning reservation; surviving rolling-stock inventories remain native Factorio objects. Mining or destroying a chest/wagon has vanilla inventory consequences.

Configuration edits are rejected while the coordinator participates in a live transfer. Cancel first. Settings survive saves, clones, blueprint tags and settings paste; reservations and train assignments are save state rather than blueprint data. The panel refreshes stock and jobs every second without replacing fields being edited.

## Physical loading limits

Targets and reserves constrain **dispatch planning**. Inserters can load extra goods between one-second coordinator checks, or unload into a different chest if built incorrectly. Use wagon filters, inserter filters, circuits and the station layout to enforce physical item/quality and quantity control. Unexpected cargo blocks departure. A requester chest consumed by local machinery may need repeated replenishment. The coordinator tracks staging stock, not every item throughout the region, and does not claim proof of receipt when an operator diverts unloading elsewhere.

Supported cargo is plain nonspoilable items, one exact item/quality per transfer. Metadata items, fluids and cross-surface/interplanetary schedules are excluded. Quality and Space Age are optional. The first 64 coordinators by entity ID participate, with up to 32 active jobs; a train has at most eight cargo wagons. Planning runs once per second, visits registered coordinators, and queries exact train-stop names rather than scanning factory inventories.

## Remote interface

All calls use `remote.call("manifold", method, ...)`. Mutations and inspection require a real player on the entity's force/surface who can reach that coordinator.

- `regional_configure(player_index, entity, config)` → `boolean, reason?`. Keys: `enabled`, `mode` (`provide`, `request`, `depot`), `station` (exact stop name), `item`, `quality` (default `normal`), `target` (1–1,000,000), `batch` (1–100,000), `reserve` (0–1,000,000), `priority` (−100–100). New coordinators default disabled. Failure reasons include `permission` and `busy`.
- `regional_inspect(player_index, entity)` → `{stations, jobs, capped, completed, cancelled}` or nil. Stations expose physical `count`, `reserved_in`, `reserved_out`, normalized `config`, and `status`. Jobs expose ID, train ID, endpoints, item/quality, planned amount, loaded amount, phase, status and age in ticks. Counts are observational, not transferable inventory copies.
- `regional_cancel(player_index, entity, job_id)` → boolean. The coordinator must be that job's provider, requester or depot.

Use `/manifold regional` while selecting a coordinator to open the same panel.
