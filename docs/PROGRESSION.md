# Progression

| Implemented stage | Science | Unlocks | Local latency | Default source/link cap |
| --- | --- | --- | --- | --- |
| Basic | Automation | Controller, copper conduits, physical interfaces/buffers | 2 s | 20 items/s |
| Reinforced | Automation + logistic | Reinforced hardware and three ranks each of bandwidth/latency research | 1 s; fully researched 0.4 s | 40; fully researched 70 items/s |
| Storage and logistics | Automation + logistic, with circuit/advanced-circuit prerequisites | Portable cells, drives, terminals, filters, buses, crafting and regional train coordination | Hardware-dependent | Hardware-dependent |
| Vanilla endgame | Automation, logistic, chemical, production, utility and space | Advanced controller/endgame conduits | Six-tick (0.10 s) minimum after routing | 160; fully researched 280 items/s |
| Optional planet branches | Corresponding planetary pack; native cargo requests use space science | Vulcanus/Fulgora bulk capacity, Gleba freshness, Aquilo latency, platform/landing-pad native requests | Context-dependent | Context-dependent |

Basic latency research reaches 0.8 s; reinforced reaches 0.4 s. Hardware throughput multiplies the startup rate, and mixed routes retain their slowest conduit tier. Force-owned research updates existing networks at the next scheduler cycle; packets keep their assigned due ticks. An advanced controller without its endgame research falls back to reinforced behavior. Power, queue caps, topology, stock targets and physical ownership remain mandatory.

The complete core progression is playable without Space Age. Optional planetary science does not gate vanilla endgame hardware. See ENDGAME.md and SPACE_AGE.md for exact recipes, costs and limits.
