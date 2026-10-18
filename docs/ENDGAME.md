# Vanilla endgame transport (v0.9)

Research **Near-instant Manifold networks** after Reinforced Manifold networks, vanilla space science, production science and utility science. The technology costs 1,000 each of automation, logistic, chemical, production, utility and space science packs at 60 seconds. Neither Space Age nor planetary science is required.

| Hardware | Source/link multiplier | Default source cap | Default researched cap | Controller demand / buffer |
| --- | ---: | ---: | ---: | ---: |
| Basic | 1× | 20 items/s | 35 items/s | 30 kW / 60 kJ |
| Reinforced | 2× | 40 items/s | 70 items/s | 60 kW / 120 kJ |
| Advanced | 8× | 160 items/s | 280 items/s | 1 MW / 2 MJ |

The researched cap includes all three bandwidth ranks. Advanced hardware recipes use reinforced hardware, processing units and low-density structures. v0.10 supplies dedicated centrifugal-controller and annular-conduit artwork. Native fast replacement and Upgrade Planner targets extend from basic to reinforced to advanced. Existing interfaces, buffers, drives and buses remain compatible. Multiple controllers still disable a connected network.

A researched advanced controller assigns new packets a **six-tick (0.10 s)** minimum latency. A packet remains a physical script inventory until delivery commits. Initial route discovery, congestion, full inventories, power loss and scheduler budgets can delay delivery. This is bounded near-instant local transport, with finite throughput; it does not bypass topology, permissions, exact quality, destination targets or item ownership. Cross-planet cargo still uses native rockets/platforms.

Copper links constrain mixed routes to the basic cap; reinforced links constrain them to the reinforced cap. Source hardware caps apply even when all links are faster. Reversing the endgame research makes installed advanced hardware use reinforced throughput/latency until research is restored. Existing packets retain their assigned due ticks. Optional planetary bonuses remain additional specializations.

## Large networks

Shortest-path discovery and reconstruction still process at most 256 steps per network per scheduling cycle. During reconstruction, maximal unbranched conduit corridors compile to one shared capacity ledger. The representative is the minimum physical edge ID along that corridor, independent of direction. Every usable route through that corridor shares its admission and delivery credits. Junctions and devices split corridors; the slowest hardware grade constrains the entire corridor. Dynamic edits invalidate affected graphs, paths and ledgers through the existing rebuild mechanism.

For example, a 10,000-conduit straight corridor needs one ledger rather than 10,001 edge updates per transfer. Diagnostic bottlenecks identify the representative edge of a corridor; they no longer store a duplicate traffic sample on every interior edge. `inspect()` reports `route_ledgers` and `route_cache` per network. Pure per-edge requests remain supported internally, while runtime transport/crafting routes between devices use compression.

Topology snapshots and Lua sorting still have costs proportional to the affected network. Branch-heavy paths may retain many separate ledgers. The implementation does not claim constant total cost for arbitrary graphs or unlimited traffic. The 256-node topology step, 128 route cache entries/network, 32 admitted networks/cycle, eight sources/network visit, 128 packet visits/cycle, 128 packets/network and 4,096 total packet cap remain enforced. Sleeping in-transit packets defer native endpoint queries until due; power, identity, topology and inventory ownership are rechecked before delivery.

See RELEASE_0.9.md for native benchmarks, acceptance and remaining limits.
