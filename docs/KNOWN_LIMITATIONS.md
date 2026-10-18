# Known limitations — 0.11.3

Manifold 0.11.3 is a first public preview for Factorio 2.0.77 and newer within the 2.0 series. Space Age and standalone Quality are optional. Factorio 2.1 and arbitrary third-party overhaul compatibility are not claimed. The UI currently has English localization only.

## Gameplay boundaries

- Three transport hardware tiers ship: basic/copper, reinforced and advanced. The original five science stages, blue/purple/yellow intermediate hardware, advanced storage drives and additional large cells are not all implemented. Energy-efficiency research is not implemented.
- Ordinary packets and cells accept undamaged plain nonspoilable items. Ammo, tools, blueprints, tagged stacks, vehicles and equipment-bearing items are unsupported. Cells have 16 or 64 native inventory slots; quality does not enlarge them.
- Freshness-aware logistics separately transfers perishables between native inventories. Digital cells, crafting escrow and regional freight reservations reject perishables. Freshness-aware crafting, age-based production planning and expiry alerts are not implemented.
- Autocrafting uses connected assembling machines with deterministic single-item-result recipes and at most eight supported ingredients. Fluids, furnaces, probabilistic/multiple-product recipes, modules and positive quality effects are rejected. Exact-quality ingredients and recipes must match. Machines should be empty when assigned; keep competing inserters/automation away from them. Cancel returns job-owned stock, not ingredients already delivered to a machine.
- A terminal indexes the first 32 drives and 32 buses in stable order (up to 128 cells/8,192 cell slots). Crafting discovery considers the first 32 interfaces; request queues hold up to 32 jobs. Regional planning considers the first 64 coordinators and up to 32 jobs. These are intentional work bounds, not unlimited factory support.
- Buses do not rebalance inventories automatically. Circuit conditions read an attached chest/machine (or the drive); network-wide stock broadcasting is not implemented.
- Routing selects deterministic shortest paths. Distinct branches share separate capacity, but equal or longer alternative paths are not selected dynamically to avoid congestion. No permanent traffic overlay, historical throughput chart or per-hop packet position is provided.
- Topology rebuilds and many-network/queue churn can cause spikes. Previous headless 10,000-conduit measurements are fixture results, not a production or multiplayer guarantee.

## Still needs real-world acceptance

- Two-client multiplayer, simultaneous terminal/recovery actions, late joins, desync checks and animation synchronization.
- Long campaigns and production-scale regional trains, including interactions with arbitrary train/logistics mods.
- A complete fueled rocket launch, platform voyage and physical landing under Manifold requests. Native request configuration and persistence were tested; a complete voyage was not.
- Broad player/robot blueprint workflows, force merges, surface deletion/recovery and conflicting external machine automation. Some focused robot upgrades, tag revival, cloning and save upgrades already have native tests; these do not prove every lifecycle combination.

Back up an existing save before adopting the preview. Report reproducible problems through the public issue tracker.
