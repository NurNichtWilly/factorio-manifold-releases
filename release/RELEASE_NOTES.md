# Manifold — sandbox click fix

The previous sandbox patch fixed the window APIs, but ordinary clicks could still fail before reaching them: a characterless controller can display an entity highlight while `player.selected` is empty. Manifold now resolves the target from the input's cursor position for clicks and Ctrl+M, while ignoring inputs over GUI elements.

Use **0.11.6 for Factorio 2.0.77+** or **0.12.2 for Factorio 2.1.22+**. The infinity-chest and standalone-window fixes remain included.

Validation includes the registered production input handlers, native selection recovery from an empty selection in god/editor/spectator modes, window access and persistence, and a real mouse/keyboard reproduction with Kux-BlueprintExtensions 4.3.18 and Kux-CoreLib 4.17.10. The previous version's empty-selection click failure was reproduced directly.

This remains a public preview. Multiplayer, long campaigns and arbitrary overhaul combinations remain unverified.
