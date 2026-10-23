# Manifold — Portal feedback update

Downloads: **0.11.7 for Factorio 2.0.77+**, **0.12.3 for Factorio 2.1.22+**.

- Fix visible component windows in remote sandbox views while the character remains on another surface.
- Add furnace autocrafting using the last smelting recipe. Prime a furnace once and empty it before assigning it; supply burner fuel separately.
- Feed bounded batches so machines can work through multiple crafts before another full feed/collection cycle.
- Request crafts directly in the storage terminal. Search/sort attached recipes, click for one item or Shift-click for ten, and see recursively craftable quantities (capped at 1,000).
- Add storage sorting and hide detailed component/recipe/machine diagnostics behind explicit buttons.
- Remove the Pattern Encoder entirely. Existing encoder entities and items disappear on upgrade without refund. Reconnect network gaps with conduits. Existing interface pins and CPU preferences remain.

Shared bandwidth/latency still limit production; 100% uptime is not guaranteed. Fluids, probabilistic/multiple-product recipes, modules and positive quality effects remain outside the supported scope. Multiplayer and arbitrary overhaul combinations remain unverified.

Native production, GUI, save/reload and upgrade tests passed on Factorio 2.1.23, including Blueprint Sandboxes 3.3.0, standalone Quality and Space Age. The 2.0 package has static API and archive checks; a fresh 2.0 engine run was unavailable. Both remain public previews.
