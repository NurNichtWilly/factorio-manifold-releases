# Manifold player guide

For Manifold 0.11.2 on Factorio 2.0.77 or newer in the 2.0 series.

## First network

Research **Basic Manifold networks**, after Automation. Craft one controller, two copper conduits and one interface of each kind. Build this uninterrupted line, with each building on the next tile:

```text
Source chest (iron plates)
Input interface
Copper conduit
Basic controller ← supply electricity with an ordinary nearby electric pole
Copper conduit
Output interface
Destination chest
```

Put iron plates in the source chest. After the delay, plates arrive in the destination. All Manifold components conduct connectivity in four cardinal directions; ghosts do not connect until built. External chests are endpoints, not conduits. Put only one external inventory next to each interface: when several touch, the lowest entity unit number is selected deterministically. Machine output/input inventories are supported by the adapter but have not been exercised in the engine tests.

Click an interface or controller to inspect it in a panel docked to the native character window. Buffer diagnostics dock beside its actual container window. To inspect any selected component, press **Ctrl+M** or enter `/manifold`. Click a buffer normally to open its inventory. Analyzer throughput averages five completed seconds, so wait several seconds for the reading to settle. It reports declared controller demand and actual stored energy, rather than claiming a measured electrical supply rate.

Press **R** or **Shift+R** over a controller or interface to rotate it. These turn the actual machinery and its shadow. Over a buffer, **Ctrl+Alt+R** / **Ctrl+Alt+Shift+R** rotates its gauge assembly around the round tank. Press **Ctrl+Alt+V** over an input, output, conduit or buffer to cycle through three visual designs. Conduits reshape automatically to match adjacent Manifold components; rotation and variants do not change transport rules or inventory ownership. Blueprint tags retain selected designs and buffer gauge orientation when rebuilt, and native interface directions are retained by the engine.

To test interruption, remove a conduit, wait, then rebuild it. Transit packets should pause and resume. Remove electricity to test power gating; the controller's energy buffer allows brief continued operation. Fill the destination or set its chest bar to block insertion, then free space. Packets retain their items until insertion succeeds.

A buffer attached to the network receives input when no output can accept that item and can later feed outputs. Multiple controllers on a connected network disable transport: separate the networks or remove the extra controller.

If an interface or its external chest disappears while items are travelling, its packets become orphaned. Use **Recover orphaned items** in the analyzer, or `/manifold recover`, to retrieve your force's orphaned items into your character inventory. A full character inventory leaves the remainder in escrow. Disconnecting a conduit alone does not orphan a packet. Save and reload while packets are pending to test persistence.

## Central storage

Research **Manifold central storage** after Reinforced Manifold networks and Advanced circuits (150 red/green science). Craft a drive, a terminal and a 16- or 64-slot cell. Connect the drive and terminal tile-to-tile to a network with exactly one powered controller. They both conduct network connectivity.

Click the drive to open its native Factorio container window, with your character inventory beside four real cell slots. Move cells with the ordinary inventory controls; Shift-click transfers them between your inventory and the drive. The attached storage panel shows live capacity. There are exactly four bays, independent of drive quality. Installation and removal are physical actions and do not require network power. Native inventories own every cell's contents, so carrying, mining, dropping, reinserting and saving a cell preserve its inventory. Destruction follows vanilla chest/item rules and can destroy contents; do not treat cells as indestructible escrow.

**Capacity means inventory slots, with each item's normal stack limit.** A 16-slot cell holds up to 1,600 iron plates (100 per slot), or 800 steel plates (50 per slot). The 64-slot cell has four times the slots. Item names and qualities occupy separate stacks; partial stacks use a whole slot. There is no byte count, 1k-item claim, or item-type surcharge. Cell quality does not multiply its slot count. Larger-cell recipes use raw materials so they never consume a filled smaller cell.

Click the terminal to see item icons, quantities, cell count, occupied/total slots and total stored items. Search English/internal item names (spaces or hyphens) or quality. Results use Factorio slot buttons, translated tooltips and pages of 50 items. Shift-click ordinary items from your character inventory into the eight native terminal deposit slots. The network sends them to installed cells using packet latency/bandwidth; full or offline cells leave items in the terminal or its existing recoverable escrow. Alternatively hold an ordinary stack and click **Deposit items held in hand** for an immediate deposit; full cells leave the remainder in your cursor. Click an item icon to withdraw up to its normal stack size into your main inventory; Shift-click withdraws one. A full player inventory leaves the remainder in the cell. Item-grid withdrawals and the cursor-deposit button commit immediately; native terminal-slot, input/drive/output transfers use the existing packet latency and shared bandwidth.

Terminal actions require physical reach, the same surface/force, and an online network; they recheck permissions on every action. Disconnected, unpowered, rebuilding or multiple-controller networks expose no stored contents. A terminal accesses the first 32 drives by stable entity ID (up to 128 cells/8,192 slots), with an explicit warning for larger networks. This bound applies to terminal statistics and actions; automated transport can still visit other drives. Use separate storage networks for larger installations.

Inputs prefer accepting outputs, then cells/buses, then physical buffers. Installed cells supply outputs through ordinary transport. Removing a packet's source/destination cell makes that packet recoverable by its force; it is never silently delivered into a replacement cell. Reinserted goods become available again, while orphaned escrow uses the existing analyzer recovery action. Portable cells have no permanent force binding: their current physical holder owns the goods, and only the current drive's force can access them through its network.

Cells accept ordinary nonspoilable item prototypes and prohibit nested cells, ammo, tools, blueprints and other metadata-bearing item types. Damaged or extra-data stacks remain unavailable to automated transport and terminal withdrawal. Native player inventory operations can access cell contents directly. Bus-connected physical chests also appear in the terminal and can supply crafting reservations.

## Smart logistics (v0.4)

Click an input, output, buffer or storage bus and choose **Configure** in its analyzer. Drives have the same button beside their native bays. `/manifold configure` opens settings for the selected endpoint; Enter applies a numeric field. Settings include eight item filters (empty accepts all), allow/reject mode, optional exact quality, enabled state, external side, destination priority from -100 to 100, and a target per item/quality (zero means unlimited). Settings survive saves, blueprints, cloning and settings paste.

Outputs remain the first destination class, followed by cells and buses, then fallback buffers. Higher priorities fill first within each class; equal priorities rotate. Source scheduling stays fair. Targets include admitted packets so several imports cannot overshoot the target. Changing a filter, target or circuit condition can hold already admitted goods in escrow until it permits delivery again.

Research **Smart Manifold logistics** after central storage and Circuit network (150 red/green science). Place a **Storage bus** beside a physical chest and connect it to the network. Choose a side if several external inventories touch it. The bus has no item slots; goods remain in the chest. Bus access can be read/write, read only or write only. Inputs and terminal deposit slots can fill writable buses; readable buses supply exports. Buses do not automatically rebalance between chests or cells.

The terminal indexes up to 32 drives and 32 buses, using live physical counts. Duplicate buses to one chest count it once; the highest-priority bus in that window governs terminal access, with entity ID breaking ties. Filters and circuit/access settings apply to terminal deposit and withdrawal too. Full or offline networks retain staged deposits. Cursor deposit and withdrawal use the existing immediate, local terminal interaction.

To gate an interface or bus, wire its **attached chest or machine** to a circuit network, choose an enable signal, comparison and threshold. For a drive, wire the drive itself. Red and green values are added, absent signals read as zero, and an empty signal disables the condition. Ordinary wired chests can expose their contents through Factorio's native circuit controls. Network-wide item signal broadcasting is not included. See [logistics details](LOGISTICS.md).

## Autocrafting (v0.6)

Research **Manifold autocrafting** after Smart Manifold logistics and Automation 2 (200 red/green science). Connect one **Crafting CPU**, a **Pattern encoder**, storage, a terminal and one **Crafting interface** beside each assembling machine. Set recipes in the native machine windows; leave the machines empty and supply their electricity. The encoder automatically discovers selected recipes at the first 32 connected interfaces. Each interface must touch exactly one assembler; ambiguous placement is rejected. Optionally choose **Encode attached machine recipe** to pin its recipe and quality; encoded settings survive saves, blueprint tags and cloning.

Open the CPU or the terminal's **Crafting requests** button, choose an item and enter an additional production amount (1–1,000). For four transport belts, encode iron gear wheels and transport belts and store six iron plates. The planner reserves those six real plates, schedules two gear crafts followed by two belt crafts, and returns the four belts to storage. Existing intermediate stock reduces dependency work. Another request cannot spend stock already reserved.

Machine feeds, product collection and storage returns use shared network link/source credits and latency. Machines perform every craft using their own time and electricity. The recipe registry lists competing recipes; click one to save a preference per item/quality on the CPU. Missing preferred recipes reject new requests rather than silently switching. Machine rows show discovery diagnostics, and queue tooltips report completed/remaining crafts, elapsed time, last item movement, physical escrow and actual machine progress/status. Full storage, disconnected links, a changed recipe or power loss pause safely. **Cancel and return stock** returns goods still owned by the job; ingredients already delivered to a machine remain in that machine. If a CPU is removed, use `/manifold recover` or the analyzer recovery button to retrieve the remaining job escrow.

v0.6 supports deterministic, single-item-result recipes with at most eight plain, nonspoilable item ingredients in connected assembling machines without modules or positive quality effects. Select an unlocked quality in the request panel; every dependency machine recipe and reserved ingredient must use that exact quality. Standalone Quality and Space Age are optional; vanilla uses normal quality. Fluids, furnaces, probabilistic/byproduct recipes and random quality upgrades remain future work. Keep inserters and other automation away from assigned machine inventories. A request runs each dependency sequentially; the queue holds up to 32 requests. Read [crafting details and recovery](CRAFTING.md).

## Space Age and vanilla endgame (v0.8/v0.9)

Space Age is optional. Planet research adds bulk/recycling throughput, freshness-preserving movement between native inventories and Aquilo latency specialization. Research Interplanetary material requests, select a reachable hub/landing pad and run `/manifold space` to maintain native rocket/platform requests. Actual goods use ordinary rockets/platforms; digital cells still reject perishables. See [Space Age setup](SPACE_AGE.md).

Vanilla space science unlocks **Near-instant Manifold networks**, with 1 MW advanced controllers and endgame conduits. New local packets have a six-tick (0.10 s) minimum latency once routing is ready; default bandwidth is 160 items/s, reaching 280 with all bandwidth ranks. Copper/reinforced links remain bottlenecks. Shared corridor ledgers reduce long-route work without bypassing bandwidth or physical ownership. See [endgame setup](ENDGAME.md) and [known limitations](KNOWN_LIMITATIONS.md).

## Regional train logistics (v0.7)

Research Distributed logistics, then connect provider, requester and depot coordinators to separate powered networks. Providers and requesters bind one adjacent staging chest and a unique nearby train stop. Park an empty automatic cargo train at the depot with a single home-stop schedule and no group or interrupts. The planner reserves freight and assigns provider → requester → depot; ordinary inserters load and unload real wagons. Open a coordinator to configure requests and monitor regional stock. [Setup, loading controls and recovery](REGIONAL.md).

## Reinforced networks

After **Basic Manifold networks**, research **Reinforced Manifold networks** with red/green science and steel processing. Its recipes consume existing basic hardware plus steel (and circuits for the controller). All three tiers share their collision geometry and replacement group, and the basic entities have native Upgrade Planner targets.

A reinforced controller doubles source/link capacity and halves the configured base delay. Each of three bandwidth ranks adds 25% of base hardware capacity; each of three latency ranks reduces base hardware delay by 20%. At default settings:

| Hardware | Before speed research | With all six ranks |
|---|---|---|
| Basic controller / copper links | 20 items/s, 2.00 s minimum | 35 items/s, 0.80 s minimum |
| Reinforced controller / reinforced links | 40 items/s, 1.00 s minimum | 70 items/s, 0.40 s minimum |

Copper links cap mixed routes at the researched basic rate. A basic controller also limits reinforced links to basic capacity. Existing interfaces and buffers work with all tiers. See [vanilla endgame hardware](ENDGAME.md) for advanced 1 MW controllers, eightfold bandwidth and six-tick latency. Research belongs to each force and updates existing networks; packets already in transit keep their original due tick. Delay never drops below the six-tick scheduler interval. Rates scale with the startup throughput setting, preserving integral accounting.

The analyzer reports controller source capacity, the measured congested connection's own capacity and utilization, new-packet minimum latency, and the current controller's stored energy/demand. Aggregate independent-branch throughput can exceed one connection's cap.

## Safety and limitations

- Ordinary packet transport accepts undamaged plain `item` stacks with no extra engine data or spoil timer, preserving quality. Ammo, tools, blueprints, tagged items, vehicles and equipment-bearing items remain unsupported. Researched Freshness-aware logistics separately moves plain perishables between native inventories, preserving actual freshness; digital cells, terminal deposits and crafting/regional reservations still reject them.
- Each physical connection has **shared bidirectional capacity**, with separate admission and delivery credits. Each source also has an admission cap. Independent routes can exceed 20 items/s in total; shared trunks remain limited to 20 by default. Sources rotate priority to share contested capacity. The six-tick scheduler sets timing granularity.
- Routing chooses deterministic shortest paths and caches up to 128 routes per network. Search and path reconstruction process at most 256 steps per network per scheduling cycle. Route search can delay initial admission. There is no congestion-aware alternative-path selection or packet position simulation; delivery checks and debits the entire current route, with unbranched corridors sharing a compressed capacity ledger. A single source is still limited to the configured rate.
- Destination capacity is checked, not reserved. Other machines or players can fill it after admission; the packet then blocks safely. Queues cap at 128 packets per source network and 4,096 globally.
- Construction/removal rebuilds only touched components and adjacent components being joined; unaffected networks keep their routes, credits and transport. BFS/visual updates are bounded, but affected snapshot preparation remains O(affected nodes). Startup/configuration/force-merge reconciliation rebuilds the whole graph. Route checks remain O(path length), and scheduling many networks can lower throughput. Endpoint selection refreshes at most once per second for valid cached targets.
- Buffers contain normal physical items and follow vanilla chest mining/destruction behavior. Interfaces contain no inventory; use adjacent external inventories. The basic controller draws 30 kW with a 60 kJ buffer; the reinforced controller draws 60 kW with a 120 kJ buffer.
- Original Blender artwork uses matte weathered metals, native cast-shadow layers and matching pipe fittings. Both conduit tiers have sixteen connection shapes in three designs and do not join vanilla walls. Device connections and buffer gauges use small attached render objects; conduits use native sprites. All thirteen machines have state-driven mechanical animations with paired shadows, retaining their inventories and native identities. Fixed pipe manifolds, manual controls and sealed portable cells remain stationary.
- Only built entities produce topology; script-created components should raise build events. A configuration-change scan can discover existing components. Unraised destruction is tracked using engine destruction registrations.
- Empty all packets, recover orphaned items and empty buffers/cells before disabling/removing the mod. Removing a mod deletes its engine-owned inventories; no cross-mod uninstall preservation is implemented.
- Graphical interface inspection, Ctrl+M, output mining and player recovery have been verified. Multiplayer join/desync checks, blueprint/robot placement, surface/force migration remain unverified. Native Upgrade Planner selection was verified in the graphical client; engine construction robots completed controller/conduit upgrades during conserved live transit. See [known limitations](KNOWN_LIMITATIONS.md).

