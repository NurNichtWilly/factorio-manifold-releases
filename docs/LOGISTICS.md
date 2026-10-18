# Smart logistics — v0.4

Settings are stored per endpoint in schema-1 state. Click an interface, buffer, bus or drive and choose Configure. Apply commits all fields together after checking player force, surface and physical reach. Existing saves without settings retain unrestricted behavior. Blueprint/ghost tags, cloning and settings paste carry normalized settings; settings contain no item ownership or script inventories.

| Setting | Behavior |
| --- | --- |
| Enabled | Pauses admissions, deliveries and terminal actions involving this endpoint. |
| Item filters | Up to eight ordinary item names, allow or reject mode. Empty accepts all. |
| Quality | Optional exact quality, independently of item mode. |
| Priority | -100 to 100, descending destination preference within outputs or storage. Equal priorities rotate. |
| Target | Per item/quality in the destination inventory; 0 means unlimited. Physical counts plus pending deliveries bound new admission. For cells, the limit is per native cell inventory. |
| Side | Automatic chooses the lowest entity ID among compatible adjacent inventories; N/E/S/W restricts discovery. |
| Bus access | Read/write, read only or write only, applying to transport and terminal actions. |
| Circuit condition | Optional item/fluid/virtual signal compared with a signed integer using >, < or =. Red and green are added. No signal means no condition. |

Wire the external chest/machine used by an input, output or bus. Wire a drive itself to gate cell access. This uses the native inventory entity's connectors; buses do not emit aggregate network signals. A storage bus uses a green variant of the existing terminal artwork. Its body has zero slots; its circuit connector is not the condition source.

Inputs prefer outputs, then combined drive/bus storage, then buffers. Terminal staging fills drives and buses. Drives, buffers and readable buses supply outputs. Sources rotate fairly, visiting up to eight per network/cycle. Each destination priority tier samples up to eight peers with a rotating cursor. Large tiers may take several cycles to discover capacity. Buses never rebalance directly between storage chests or cells, avoiding automatic storage loops. Attaching distinct networks to the same physical chest intentionally shares that chest's goods.

All scheduled transfers retain native escrow, powered connectivity, edge/source capacity and minimum latency. Admission checks destination target reservations against matching pending goods. Delivery checks actual stock again, so outside inserters cannot cause Manifold to insert beyond the current target. External inserters can themselves exceed that target. A configuration change can block existing escrow; restore compatible settings to resume. Changing/removing the adjacent inventory or endpoint retains the existing recoverable-packet behavior. Mining a bus leaves the external chest untouched.

The terminal reads live inventories for the first 32 drives and first 32 buses by stable entity ID. A warning marks larger networks. Buses pointing at one chest count it once; highest priority in this bounded window selects the terminal policy, lowest ID breaks ties. Automated transport still visits buses outside the terminal window. Contents rows represent supported, currently readable items; capacity/item totals describe the physical inventories in the window, including items unavailable to automation. Counts are rebuilt for each interaction/refresh, not held in an ownership ledger.

Cursor actions are immediate local terminal interactions, with power/reach/force/surface checks. Cursor deposits use destination priorities, filters, access and target reservations. Withdrawals use readable policies and retain exact quality. Native terminal slots instead use normal scheduled transfer. Unsupported metadata/spoilable goods follow the existing transport policy and remain physical goods.

Multiplayer with two clients and broad third-party inventory compatibility remain unverified. Supported bus targets are native containers and logistic containers; wagon, fluid, machine and remote cross-surface storage indexing are outside v0.4. Inputs/outputs retain existing chest, assembler and furnace support.
