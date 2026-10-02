# Kyrix

**Silent background performance optimization for Minecraft Java Edition 1.21.4 (Fabric).**

Kyrix is designed to be completely invisible. After installing it you simply launch Minecraft and play normally. There is no HUD, no FPS counter, no chat messages, no notifications, no new menus, and no automatic graphics-quality reductions.

## Goal

Reduce unnecessary CPU/GPU work, lower frame-time spikes, improve 1% lows and frame-time consistency, and gain as much FPS as possible **without visibly changing normal gameplay**.

Even a modest 5–10 FPS improvement or smoother frame times is considered a success.

## What Kyrix does

Kyrix continuously (and silently) measures:

- Frame time
- Tick time
- Chunk rebuild pressure
- Entity density
- Overall load factor

Based on these internal measurements it adaptively applies lightweight optimisations only when the client is actually under pressure:

1. **Adaptive particle work reduction** – near-end-of-life particles skip redundant physics steps during particle storms.
2. **Light entity processing** – distant ambient/peaceful entities may skip every other AI tick under heavy load (they still exist and render).
3. **Chunk-rebuild awareness** – the system marks periods of heavy chunk activity so remaining work can be prioritised intelligently.
4. **Deferred non-critical ray-casts** – under extreme load the targeted-entity ray is refreshed less frequently (crosshair and interaction still work).

All of the above are purely client-side, never affect world state, never give multiplayer advantages, and never change visuals or vanilla mechanics.

## Compatibility

Kyrix is written to coexist with the most common Fabric performance mods:

- Sodium
- Lithium
- FerriteCore
- ImmediatelyFast
- EntityCulling
- ModernFix
- Iris

It does not duplicate the work those mods already perform and avoids any conflicting changes to rendering or world logic.

## Requirements

- Minecraft **1.21.4** (exactly)
- Fabric Loader ≥ 0.16.9
- Fabric API
- Java 21

## Building

```bash
./gradlew build
```

The finished JAR will be in `build/libs/kyrix-1.0.0.jar`.

## Installation

1. Install Fabric for Minecraft 1.21.4.
2. Install Fabric API for 1.21.4.
3. Drop `kyrix-1.0.0.jar` into the `mods` folder.
4. Launch the game. Nothing visible will appear – that is intentional.

## Versions used

| Component          | Version              |
|--------------------|----------------------|
| Minecraft          | 1.21.4               |
| Yarn mappings      | 1.21.4+build.8       |
| Fabric Loader      | 0.16.14              |
| Fabric Loom        | 1.9-SNAPSHOT         |
| Fabric API         | 0.119.4+1.21.4       |
| Java               | 21                   |

## Known limitations

- Optimisations are intentionally conservative. They only activate under real load so that smooth sessions stay 100 % vanilla.
- Because Kyrix never changes render distance, entity visibility, particle counts or graphics settings, the absolute FPS ceiling is still determined by Sodium / the GPU.
- The adaptive system resets every session; there is no persistent learning across restarts (this keeps the mod simple and free of configuration).
- Mixin targets may need minor updates if Mojang renames methods in a future 1.21.4 patch (unlikely).

## License

MIT
