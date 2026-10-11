# Wolfenstein (2009) — 60 FPS

**Game:** Wolfenstein, EU, BLES00564, v01.00
**Executable:** `PPU-12237e198da5fc2939b39d895f9d818ec076d50d`
**Patch:** `[ byte, 0x00f34170, 0x31 ]`

## What caps it at 30

Wolfenstein runs on id Tech 4 (Raven). The engine ticks at 60 Hz and draws a
frame at most once every `com_minTics` ticks. On PS3 its default is `2`, so:

    60 Hz / 2 = 30 FPS

Game logic runs on the tick clock (`com_userCommandHz` defaults to `60`:
"Number of times per second a game update is run"), not on rendered frames.
So drawing every tick doubles the frame rate without speeding up the game.

## How it was found

1. RPCS3's frame limiter (Infinite) and raising the VBlank rate to 120 Hz did not
   change menu or gameplay FPS (VBlank 120 only sped up the intro videos), so the
   cap is inside the game, not tied to vsync.
2. Decrypted `EBOOT.BIN` with RPCS3 (Utilities → Decrypt PS3 Binaries).
3. Searched the strings for frame-related cvars: `com_minTics`, `com_fixedTic`,
   `com_syncGameFrame`, `com_userCommandHz`, `r_verticalSync`.
4. Followed the pointer table that defines each cvar (name, default value,
   description) to the default strings: `com_minTics` -> `"2"` at `0xf34170`,
   `com_userCommandHz` -> `"60"`.
5. Checked that `"2"` at `0xf34170` is referenced only by `com_minTics` (one
   pointer, no code building the address), then changed it to `"1"`.

## Result

About 60 FPS most of the time; game speed, movement and animation normal.
Holds 60 more consistently at the original 720p.
