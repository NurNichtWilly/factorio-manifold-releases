# Manifold 0.11.3 — reliable recovery

Fixes a recovery corner case: when a crafting job's escrow was full, Recover returned the stored job items but left its in-flight transfer for a second action even if the player had enough space. Recovery now drains both real inventory owners directly in one action when capacity permits, preserving quality and item totals.

The analyzer button and `/manifold recover` now report exact returned and remaining counts. They distinguish remaining stock due to inventory capacity from the absence of a character inventory. Existing integrations still receive a numeric recovered count; `recovery_status(player_index)` adds a read-only breakdown.

## Install

Download **manifold_0.11.3.zip**, put it unextracted in the Factorio mods directory and enable Manifold. The adjacent SHA-256 file verifies the download. GitHub's automatic source archives are not installable mods.

This remains a public preview for Factorio **2.0.77+ within 2.0**; Factorio 2.1 is not supported. Space Age and standalone Quality remain optional. Multiplayer, full platform voyages and the remaining original-spec features are still unverified or incomplete as documented in Known Limitations.
