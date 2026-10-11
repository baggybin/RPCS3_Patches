# RPCS3 Patches

Game patches for [RPCS3](https://rpcs3.net), the PS3 emulator, that aren't in
the official patch list (yet). All patches are in [`patches.yml`](patches.yml),
in RPCS3's own patch format.

## Patches

| Game | Serial | Version | Patch | Status |
|---|---|---|---|---|
| Wolfenstein (2009) | BLES00564 (EU) | 01.00 | 60 FPS | Tested: ~60 FPS, normal game speed |

Write-ups of how each patch was found are in [`notes/`](notes/).

## Installing

1. Download [`patches.yml`](patches.yml).
2. In RPCS3, open **Manage → Game Patches** and drag the file onto the window
   (or copy its entries into `patches/imported_patch.yml` in RPCS3's config folder).
3. Tick the patch for your game and launch it.

A patch only shows up if your game's executable matches: same region, same
version (including installed updates). RPCS3 prints the executable hash in its
log at boot as `PPU executable hash: PPU-...`.

## Other regions and versions

Each region/version of a game has a different executable, so the patch address
differs. If you have one that isn't listed (e.g. Wolfenstein US, BLUS30298),
open an issue with the `PPU executable hash` from your RPCS3 log.
