# Cover Up! — Map Project Starter

A minimal starting point for authoring a **Cover Up!** custom map. This is a **skeleton**, not a
fully pre-generated Unity project — open it once in Unity 6000.5 and the editor fills in the rest
(`Library/`, the lockfile, and the remaining `ProjectSettings/`).

## First run

1. Install **Unity 6000.5.3f1** (the version this template is pinned to in
   `ProjectSettings/ProjectVersion.txt` — matching the shipping game).
2. Open this folder as a Unity project — **Unity Hub → Projects → Add → Add project from disk**,
   then pick this folder. Unity resolves `Packages/manifest.json`, which pulls in the **Cover Up!
   Map SDK** (`com.coverup.mapsdk`) by git URL, plus URP. The first open needs network access and
   `git` on your PATH.

   > **The first open takes 15–25 minutes, and looks like it has hung.** You'll get a progress bar
   > reading `Shader Universal Render Pipeline/Lit: preparing variants…` counting toward tens of
   > billions. That is normal and it is not stuck: URP's Lit shader has dozens of independent
   > keyword switches, and Unity enumerates their combinations once per project. It is a one-time
   > cost — `Library/` is gitignored, so you pay it per clone, not per open. **Don't kill it**;
   > a half-built shader cache just makes it start over. Check `Logs/Editor.log` if you want to
   > watch it tick along.
3. **Check the render pipeline is assigned.** A URP asset ships with this template at
   `Assets/Settings/MapProjectRenderPipeline.asset`. Open **Project Settings → Graphics** and make
   sure it is set as the *Scriptable Render Pipeline Settings*, and likewise under
   **Project Settings → Quality**.

   > This matters more than it looks. With no URP asset assigned, Unity renders with the built-in
   > pipeline, every material you author is a built-in material, and your map loads **pink** in the
   > game — a failure that surfaces at the very end, far from its cause. While you're there, confirm
   > **Player → Other Settings → Color Space** is **Linear**, which is what the game uses; authoring
   > in Gamma means your lighting won't match what players actually see.

## Author a map

- **Open `Assets/Maps/Scenes/starter_island.unity`.** Every map is an island: the game draws one
  endless sea at the scene's Y 0, the same sea the lobby island stands in 850 m away, and what you
  build rises from it (players see your island on the lobby's horizon between rounds). The starter
  is a complete, working `_CoverUpMap`: sand rising from the shallows the way the lobby island does,
  the bounds drawn as outlines in knee-deep water, spawns, the arena sun, the island sky, Tiny and
  Small built, one open-sided shed. Build on it or replace the land; keep floors above Y 0, or draw
  a `MapSeaHole` over a dry one (a cave, a basement). Want a fresh copy? **Cover Up! → Maps → Create
  Starter Island** regenerates it (delete the scene first). The old indoor corridor example is still
  under **Create Example Sized Map (legacy)**.
- **Build inside `Base/Content`.** A map scene is `_CoverUpMap → Base → {Fixtures, Content}`
  (plus `Sizes` for the size variants). `Fixtures` holds the few objects the map can't lose —
  the spawn disc and the sun — and `Content` holds everything you author. The split is
  enforced: `Validate Map` errors on a missing group or on anything left loose under `Base`.
  Have a scene that isn't in this shape? **Cover Up! → Maps → Group Base** sorts it out in one
  pass without deleting anything.
- Give it its own identity on the `WorkshopMapInfo` component (**Map Id**, **Title**, **Preview**).
  A preview is required to publish, and the in-game browser draws it **full-width as the entire map
  card** — aim for ≈1280×720, 16:9, under 1 MB.
- **Cover Up! → Maps → Validate Map** checks the scene against the map contract; then
  **Export Workshop Map** builds the package.
- Exports land in your local maps folder (`~/CoverUpMaps/<mapId>/` on Linux/macOS,
  `Documents\CoverUpMaps\<mapId>\` on Windows), which the installed game reads in **Sandbox** for
  live testing.

## What a map may contain

A map is a **pure environment**: Map SDK components and stock Unity components, nothing else. The
game strips anything outside that allowlist as it loads, so a stray script that rode in on an asset
pack won't throw an error — it will just silently stop working. `Validate Map` catches these before
you export. Run it.

Full workflow: see **`Documentation~/MapCreatorGuide.md`** in the
[Map SDK repo](https://github.com/cover-up/map-sdk).
