<picture>
  <source media="(prefers-color-scheme: dark)" srcset="doc/displayxr_white.png" width="120">
  <source media="(prefers-color-scheme: light)" srcset="doc/displayxr.png" width="120">
  <img alt="DisplayXR" src="doc/displayxr.png" width="120">
</picture>

# DisplayXR Runtime — Archived Snapshot

> **⚠️ This repository is an archived, read-only snapshot.**
> It preserves the pre-2026 history of the DisplayXR runtime (through
> release `v1.1.2`, shell code excluded). The instructions below predate
> the May 2026 changes — the vendor plug-in extraction (ADR-019, Leia SR
> now ships as a separate plug-in), the shell and MCP framework splits,
> and the macOS installer. **Don't build from or rely on this snapshot.**
>
> - **Active development → [DisplayXR/displayxr-runtime](https://github.com/DisplayXR/displayxr-runtime)**
> - **Docs, downloads & guides → [displayxr.org](https://displayxr.org)**

---

## What this snapshot is

An open-source [OpenXR](https://www.khronos.org/openxr/) runtime for
spatial displays — 3D monitors and laptops with tracked stereo and
multiview lightfield display technology. Built on
[Monado](https://monado.freedesktop.org/) by Collabora, it strips away
headset-centric infrastructure (34 VR drivers, Vulkan server compositor,
tracking subsystems) and replaces it with a lightweight runtime
purpose-built for 3D displays: ~150 files, 3 drivers, native compositors
for every graphics API.

This mirror froze the codebase before the runtime was de-privatized and
before Leia SR, the shell, and the MCP framework were split into their
own repos. It is kept for historical reference only.

## Architecture (as of this snapshot)

```
App (any graphics API)
        |
   OpenXR State Tracker
        |
   Core xrt interfaces
        |
   +----+-----+--------+--------+
   |    |     |        |        |
 D3D11 D3D12 Vulkan  Metal   OpenGL   ← native compositors
   |    |     |        |        |
   Display Processor (LeiaSR / sim_display)
        |
   Display
```

Every graphics API gets its own native compositor — no Vulkan
intermediary, no interop overhead. Vendor-specific processing
(interlacing, lenticular weaving) is isolated in the display processor
layer. *(In the current runtime, vendor display processors such as
Leia SR ship as out-of-process plug-ins rather than in-tree — see
ADR-019 in the active repo.)*

## Where things live now

| Looking for… | Go to |
|---|---|
| The current runtime source & docs | [DisplayXR/displayxr-runtime](https://github.com/DisplayXR/displayxr-runtime) |
| Downloads, getting started, vendor integration | [displayxr.org](https://displayxr.org) |
| Leia SR display-processor plug-in | [displayxr-leia-plugin](https://github.com/DisplayXR/displayxr-leia-plugin) |
| DisplayXR Shell (spatial workspace) | [displayxr-shell-releases](https://github.com/DisplayXR/displayxr-shell-releases) |
| OpenXR extension specs & headers | [displayxr-extensions](https://github.com/DisplayXR/displayxr-extensions) |
| Unity / Unreal engine plugins | [displayxr-unity](https://github.com/DisplayXR/displayxr-unity) · [displayxr-unreal](https://github.com/DisplayXR/displayxr-unreal) |
| Projection math library | [kooima-projection](https://github.com/DisplayXR/kooima-projection) |

## License

Boost Software License 1.0
