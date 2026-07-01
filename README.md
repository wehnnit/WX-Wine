# WX-Wine

**WehniX Wine** — official engine releases for running Windows games on Mac.

WX-Wine is the home for **WehniX Engine** builds: self-contained Wine runtimes packaged for macOS, designed to work with the [WehniX](https://github.com/wehnnit/WehniX) desktop app. Each release ships as a ready-to-use `.app` bundle (and `.zip`).

> **Renderer support:** WehniX Wine currently supports **DXMT only**.  
> DirectX titles are translated to Metal through DXMT. Other backends (DXVK, D3DMetal, D9VK, etc.) are **not** supported on this engine line at this time.

---

## What is WehniX Wine?

| | |
|:---|:---|
| **What it is** | A macOS-native Wine engine bundle built for Windows game compatibility |
| **Who it's for** | WehniX users and anyone integrating WehniX Engine releases |
| **How it works** | Runs x86_64 Windows apps through Wine, with **DXMT** handling DirectX → Metal |
| **Distribution** | Released here as versioned `.zip` archives per engine generation |

WehniX Wine is **not** a standalone game launcher. It is the **runtime** that powers bottles, Epic installs, and game launches inside WehniX.

---

## WehniX Engine 11.11

The first engine in the WX-Wine release line.

| Spec | Detail |
|:---|:---|
| **Release name** | WehniX Engine 11.11 |
| **Wine base** | `wine-11.11` |
| **Graphics API** | **DXMT only** (DirectX 11 → Metal) |
| **Architecture** | x86_64 Windows apps via Rosetta on Apple Silicon |
| **Bundle format** | `WehniX Engine 11.11.app` |
| **Download size** | ~1.3 GB (compressed `.zip`) |
| **macOS required** | macOS 14.0 (Sonoma) or later |
| **Bundle ID** | `com.wehnix.engine.11.11` |

---

## What's inside Engine 11.11

| Component | Role |
|:---|:---|
| **Wine 11.11** | Core Windows compatibility layer |
| **DXMT** | DirectX-to-Metal translation (`d3d11.dll`, `dxgi.dll`, `winemetal.so`) |
| **MoltenVK** | Vulkan support layer bundled for runtime dependencies |
| **Wine prefix** | Clean, portable prefix inside the engine bundle |
| **Launch tooling** | DXMT launch path for Windows executables |

---

## Supported renderers (Engine 11.11)

| Renderer | Status | Notes |
|:---|:---|:---|
| **DXMT** | Supported | Default and only supported graphics path |
| DXVK | Not supported | Not included in WehniX Wine at this time |
| D3DMetal / GPTK | Not supported | Use WehniX's separate GPTK engine option in the main app |
| D9VK | Not supported | — |
| Stock Wine D3D | Not officially supported | Present for internal/debug use only |

---

## Epic Games compatibility (via WehniX + Engine 11.11)

These titles are tested/supported when launched through WehniX with Engine 11.11 and DXMT:

| Supported | Not supported |
|:---|:---|
| Alan Wake 2 | Fortnite |
| Alan Wake Remastered | |
| Control | |
| Dead Island 2 | |
| DEATH STRANDING | |
| Grand Theft Auto V Enhanced | |
| Hogwarts Legacy | |
| KINGDOM HEARTS HD 1.5+2.5 ReMIX | |
| KINGDOM HEARTS III + Re Mind | |
| Red Dead Redemption 2 | |
| Rise of the Tomb Raider | |
| Rocket League | |
| Shadow of the Tomb Raider | |
| Sifu | |
| Tony Hawk's Pro Skater 1 + 2 | |

> Compatibility lists may expand in future WX-Wine releases. Always check the release notes for the engine version you download.

---

## Downloads

| Engine | Release asset | Size (approx.) |
|:---|:---|:---|
| **WehniX Engine 11.11** | `WehniX Engine 11.11.zip` | ~1.3 GB |

Future engines (11.0, GPTK packs, etc.) will be published in this repository as separate tagged releases.

---

## Installation (manual)

| Step | Action |
|:---:|:---|
| 1 | Download `WehniX Engine 11.11.zip` from the latest Release |
| 2 | Extract the archive |
| 3 | Place `WehniX Engine 11.11.app` where WehniX expects it, **or** follow WehniX's in-app engine install instructions |
| 4 | Select **WehniX Engine 11.11** in WehniX → Settings → Wine Engine |
| 5 | Ensure **DXMT** is selected as the renderer |

Most users should install engines through the **WehniX** app rather than manually.

---

## Requirements

| | |
|:---|:---|
| **macOS** | 14.0 (Sonoma) or later |
| **Chip** | Apple Silicon (M-series) recommended |
| **Rosetta** | Required for x86_64 Windows binaries |
| **WehniX app** | Recommended for bottles, Epic library, installs, and launches |
| **Internet** | Required for first-time WehniX setup and Epic sign-in |

---

## Engine roadmap

| Engine | Status in WX-Wine |
|:---|:---|
| **WehniX Engine 11.11** | Available — DXMT only |
| WehniX Engine 11.0 | Planned / separate release |
| Game Porting Toolkit 3.0 | Planned / separate release |

---

## Legal

WehniX Wine engines are proprietary releases distributed by **WehniX**.  
Copyright © 2026 WehniX. All rights reserved.

Wine is used under its respective license. Third-party components (DXMT, MoltenVK, etc.) remain subject to their own licenses.

---
