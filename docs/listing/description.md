# Listing copy

Copy for the extension platforms (extensions.blender.org for the add-on, Yak
for the `.gha`), assembled from the 0.8.1 release notes. Keep it in step with
the README; the platform upload itself is a later decision recorded in
[plan.md](../plan.md).

## Add-on (extensions.blender.org)

**Name:** Stageloom

**Tagline:** Grasshopper definitions as stackable modifiers in Blender

**Short description** (plain text, one paragraph):

Drive Grasshopper definitions from Blender as stackable modifiers, next to
native Geometry Nodes modifiers, in one visible object per stack. Geometry and
parameters flow through the stack, so parameters can be keyframed, driven, and
played back.

**Long description:**

Stageloom connects Blender and Grasshopper over one local WebSocket. Add a
stage to any mesh, curve or point object and its Grasshopper definition runs on
every edit, with no buttons: the definition's output shows through a modifier
in the stack, where it composes with native modifiers in either order.

- Geometry both ways: meshes, curves, point clouds, SubD control cages, and
  Breps (meshed on the way out, with a warning).
- Named attributes travel with the geometry; Attribute Get and Attribute Set
  read and write them inside a definition.
- Blender instances cross as Grasshopper blocks, nested and multi-part
  definitions included.
- Param components expose float, int, bool, vector, colour, value-list and text
  parameters in Blender's N-panel, with ranges, keyframes and drivers.
- Live playback: Play Every Frame waits for each stage; Freeze and the native
  Bake stage cover offline frames and rendering.

A Grasshopper definition runs on the machine's own Rhino 8 install; without
Rhino, the bundled stand-in (`tools/fake_gh`) answers the loop so the add-on
can be explored on its own. Requirements: Blender 5.2 or newer, Online Access
enabled (the add-on listens on localhost), and Rhino 8 with Grasshopper for the
Grasshopper half. GPL-3.0-or-later; source and issue tracker at
https://github.com/miscasquel/stageloom.

**Permissions rationale:**

| Permission | Why |
|---|---|
| `network` | The add-on listens on `127.0.0.1` for the Grasshopper connection; nothing outside the machine can connect. |
| `files` | The add-on writes its logs under the extension's user data directory. |
| `clipboard` | Copy stage key copies the stage key so it can be pasted into the Grasshopper components. |

**Support:** https://github.com/miscasquel/stageloom/issues

## Grasshopper plugin (Yak)

**Name:** Stageloom

**Version:** follow the manifest; the `.gha` and the add-on release together.

**Summary:**

Stage In, Stage Out, Param, Attribute Get/Set and the Stageloom Connection
component. Grasshopper becomes the solver behind a Blender modifier stack:
Blender sends geometry, the definition runs on each edit or frame, and the
result returns through one generic Geometry input and output. Parameters,
attributes and blocks travel both ways over a local WebSocket (default port
59130, configurable in Stageloom Connection). Requires the matching Blender
add-on from https://github.com/miscasquel/stageloom/releases.

## Screenshots

Captured from the DEMO.md scene, not private project data. Three static PNGs,
16:9, under ~2 MB each; no heavy GIFs (the platform calls them out).

1. **Blender.** Viewport with a stack object, the Stageloom modifier, the
   Stageloom N-panel showing parameters and an `ok` stage.
2. **Grasshopper.** Rhino/GH with Stage In → definition → Stage Out + Param,
   with the Blender result visible.
3. **No Rhino.** `fake_gh` running in a terminal and the panel connected, so a
   reviewer can see the add-on works without Rhino.

Save them here as `screenshot-1.png`, `screenshot-2.png`, `screenshot-3.png`
(or keep the originals and upload from this directory).
