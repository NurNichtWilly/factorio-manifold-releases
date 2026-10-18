# Manifold

![Manifold industrial transport hardware](release/media/hardware.png)

**From copper conduits to a connected factory.** Manifold adds powered item networks, portable storage and production requests fulfilled by real Factorio machines. Research improves existing networks; better controllers and conduits raise their limits. Belts, trains and inserters still have work to do.

**First public preview · v0.11.2 · Factorio 2.0.77+ within the 2.0 series · Space Age optional · English UI**

[Download releases](https://github.com/NurNichtWilly/factorio-manifold-releases/releases) · [Report a bug](https://github.com/NurNichtWilly/factorio-manifold-releases/issues/new/choose) · [Player guide](docs/GUIDE.md) · [Known limitations](docs/KNOWN_LIMITATIONS.md)

## What you can build

- **Powered transport:** tile-adjacent networks with real item ownership, shared connection bandwidth, delivery latency, buffers and recoverable interrupted transfers.
- **Central storage:** portable 16- and 64-slot cells, four-bay drives, searchable terminals and physical chest storage buses.
- **Smart logistics:** item/quality filters, priorities, stock targets and circuit enable conditions.
- **Machine crafting:** automatic recipe discovery, explicit recipe preferences, dependency planning and physical material reservations. Your assembling machines do every craft.
- **Regional freight:** coordinate providers, requesters and depot trains. Inserters load and unload real wagons.
- **Vanilla endgame:** advanced hardware reaches a six-tick minimum local packet delay; default capacity is 160 items/s, or 280 with all bandwidth ranks.
- **Optional Space Age:** planetary research, freshness-preserving movement between native inventories and native rocket/platform material requests.
- **Original industrial artwork:** animated operating mechanisms across all thirteen machine families, with paired shadows and 55 direction/design views.

![Machine crafting and production monitoring in Factorio](release/media/crafting-ui.png)

## Install

1. Download `manifold_0.11.2.zip` from the release assets. GitHub's automatic **Source code** archives contain this release website, not an installable mod.
2. Put the ZIP, without extracting it, in your Factorio `mods` folder.
3. Enable **Manifold** in Mods and restart Factorio.
4. Start a game or load a backed-up save. Research **Basic Manifold networks** after Automation.

Mod folders: Windows `%APPDATA%\Factorio\mods`; macOS `~/Library/Application Support/factorio/mods`; Linux `~/.factorio/mods`.

Factorio **2.1 is not supported by this release**. Space Age and Quality are optional. This is an early public preview: multiplayer, long campaigns and arbitrary overhaul-mod combinations have not been fully validated.

## Your first network

Build an uninterrupted line, placing each component on the next tile:

```text
Source chest
    ↓
Input interface
    ↓
Copper conduit
    ↓
Basic controller ← electricity from a nearby pole
    ↓
Copper conduit
    ↓
Output interface
    ↓
Destination chest
```

Supply the controller from an electric pole and put iron plates in the source chest. Use exactly one controller per connected network and one adjacent external inventory per interface. Default transport begins after two seconds and is capped at 20 items/s per source and shared connection.

Click a component or press **Ctrl+M** over it for diagnostics. Remove and reconnect a conduit to try interruption handling. Destroyed endpoints can leave recoverable items: use **Recover orphaned items** or `/manifold recover`.

Next, unlock central storage and connect a drive with a cell and a terminal. For crafting, connect a CPU, encoder and crafting interfaces beside empty assembling machines with their recipes selected. The [player guide](docs/GUIDE.md) walks through storage, filtering, train setup and crafting.

## Scope of this preview

The core logistics, storage and bounded crafting systems are implemented. The original five-stage design remains a longer-term target; the current game has three transport hardware tiers. Crafting supports deterministic recipes with a single item result and up to eight nonspoilable item ingredients, without modules or positive quality effects. Fluids, furnaces and probabilistic recycling/quality production are outside its current scope.

[Known limitations](docs/KNOWN_LIMITATIONS.md) describes practical bounds and unverified cases. [Progression](docs/PROGRESSION.md) lists actual unlocks and rates. The MIT license covers original mod code and artwork; Factorio is required and is not included.

## Feedback

Please include your Factorio version, Manifold version, enabled mods, steps to reproduce, expected/actual behavior and, when useful, a save, screenshot and `factorio-current.log`. Review logs and saves before posting personal information. Use the public repository's [issue tracker](https://github.com/NurNichtWilly/factorio-manifold-releases/issues).

This public repository contains released documentation, screenshots and release assets. Development sources, tests and editable Blender scenes are maintained separately. The installable ZIP includes the Lua code and assets required to run the mod.
