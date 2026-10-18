# Resource Compressor Extended

Use matching game branches: Manifold 0.11.4 + faccompress 3.0.0 for Factorio
2.0.77; Manifold 0.12.0 + faccompress 3.1.0 for Factorio 2.1.22.
Neither mod requires the other. Space Age is optional.

Compressed goods are ordinary items. Manifold transports, filters and stores them
without unpacking them. One compressed item consumes one transport unit and one
inventory position within its native stack, regardless of its represented mass.
Portable cells retain the real item identity and quality.

For automatic compression, place a crafting interface beside a compressor,
select a recipe in the compressor, and connect the interface, crafting CPU,
pattern encoder, terminal and storage bus to one powered network. Reserve a
separate machine for each compression step needed by the dependency chain.
The decompressor works in the same way. All ingredients, work and products stay
in real inventories. Remove modules for Manifold's bounded crafting mode.
Standalone compressors can use speed modules and beacons normally.

Compression and decompression can produce the same intermediate item, and bulk
and ordinary recipes can also overlap. Select an explicit recipe preference in
Manifold when both are attached. A reverse chain without enough physical stock
is a dependency cycle; Manifold rejects it without moving goods. It does not
silently unpack stored goods or switch a machine's selected recipe.

Compression recipes forbid productivity and quality effects. Item transport
still preserves existing quality. Do not compress stateful or perishable items;
the compressor's data-stage extension deliberately accepts only plain items.
Legacy compressed magazines remain unpackable but cannot be newly compressed.

Acceptance on 2026-10-18: both game branches passed native graphical compression,
Manifold dependency crafting, compressed-item transport and save/reload, with and
without Space Age. `tests/faccompress_unit.lua` covers exact quantities and
reversible-chain cycle rejection. The joint native fixture is maintained in the
companion faccompress development checkout, `tests/integration.lua`.
