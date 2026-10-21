# Manifold — sandbox and infinity-chest fixes

- Infinity chests now work with I/O interfaces, storage buses and regional chest endpoints.
- The analyzer opens without a character. Storage panels open independently when no main inventory exists; god/editor inventories keep native chest controls.
- Crafting and configuration windows remain accessible in god, editor and spectator modes. Withdrawals and recovery still require a main inventory.
- Standalone windows close normally, including when replacing a native container window.

Use **0.11.5 for Factorio 2.0.77+** or **0.12.1 for Factorio 2.1.22+**. Both packages contain the same bugfixes. Kux-BlueprintExtensions 4.3.18 with Kux-CoreLib 4.17.10 was tested on 2.1.22.

Validation covers native infinity generation and transport, finite-stock conservation, real player GUI opening/closing in god/editor/spectator modes, normal character inventory controls, and save/reload. This remains a public preview; multiplayer, long campaigns and arbitrary overhaul combinations remain unverified.
