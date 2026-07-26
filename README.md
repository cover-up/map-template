# Cover Up! — Map Project Starter

A minimal starting point for authoring a **Cover Up!** custom map. This is a **skeleton**, not a
fully pre-generated Unity project — open it once in Unity 6000.5 and the editor fills in the rest
(`Library/`, the lockfile, the remaining `ProjectSettings/`, and generates the URP assets).

## First run

1. Install **Unity 6000.5.3f1** (the version this template is pinned to in
   `ProjectSettings/ProjectVersion.txt` — matching the shipping game).
2. Open this folder as a Unity project. Unity resolves `Packages/manifest.json`, which pulls in the
   **Cover Up! Map SDK** (`com.coverup.mapsdk`) by git URL plus URP.
3. When it opens, create a URP pipeline asset if Unity prompts (Assets → Create → Rendering →
   URP Asset), and assign it under **Project Settings → Graphics** / **Quality**. (The game ships
   URP 17.5.0; use the same major.)

## Author a map

- **Cover Up! → Maps → Create Example Sized Map** — drops a working `_CoverUpMap` scene into your
  `Assets/` to copy from.
- Give it a new identity on the `WorkshopMapInfo` component (**Map Id**, **Title**, preview).
- **Cover Up! → Maps → Validate Map**, then **Export Workshop Map**.
- Exports land in your local maps folder (`~/Documents/CoverUpMaps/<mapId>/`), which the installed
  game reads in **Sandbox** for live testing.

Full workflow: see **`Documentation~/MapCreatorGuide.md`** in the
[Map SDK repo](https://github.com/cover-up/map-sdk).
