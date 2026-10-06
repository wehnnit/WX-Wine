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

The 11.11 list above applies to Engine 11.11 only. It is not a compatibility claim for 11.17.

---

## WX-wine 11.17

Self-contained Wine 11.17 runtime for Apple Silicon, with **DXMT v0.80** as the only game renderer.

| Spec | Detail |
|:---|:---|
| **Release name** | WX-wine 11.17 |
| **Wine base** | Wine 11.17 |
| **Graphics API** | **DXMT v0.80 only** (DirectX → Metal) |
| **Architecture** | x86_64 Windows apps via Rosetta on Apple Silicon |
| **Bundle format** | `WX-wine-11.17.app` |
| **Download** | `WX-wine-11.17.tar.xz` |
| **Download size** | ~669 MB |
| **SHA-256** | `daafa42bfd82731ec8a89feb04e55a1876bdba11e31edc05ca766eacac10d081` |
| **macOS required** | macOS 14.0 (Sonoma) or later |
| **Archive layout** | One top-level member: `WX-wine-11.17.app/` |

The archive does not include a Steam login or installed games. The first launch downloads the official Windows Steam client into the bundle.

### Patches in 11.17

| Patch | What it does |
|:---|:---|
| **Steam VC++ 2015–2019** | Extracts Steam’s official cabinet outside Wine, installs the 14.28 runtime DLLs, and checks that both 32-bit and 64-bit builds load. This avoids Wine’s `FDICopy` cabinet failure (installer exit 1603) when Steam runs the VC++ redistributable. |
| **DirectX June 2010** | Checks the required helper DLLs in both `system32` and `syswow64` before the Steam step is marked complete. `DXSETUP` itself is not run, because that installer hung. |
| **Per-game prerequisites** | VC++ 2015, 2017 and 2019 (all served by the 14.28 runtime) and June 2010 DirectX are supported. VC++ 2022 is left to Steam's own installer. Other Steam redistributables (for example PhysX or XNA) are reported as unsupported instead of skipped as success. |
| **CS2 "game file missing or corrupted"** | When Steam's VC++ installer failed inside Wine, its rollback deleted the C++ runtime DLLs that were already in `system32`, so Counter-Strike 2 could not start. Wine's installer now backs up files before overwriting them and restores them on rollback. It also retries a cabinet file it missed. Runtime DLLs whose files are missing still load as Wine builtins, and the launchers put back any missing system DLL before Steam or a game starts. |
| **DXMT shader cache after moving the app** | The shader cache and Metal HUD log paths now follow the app when it is moved, so DXMT no longer reports "Failed to open file for locking". |
| **DXMT v0.80** | Default game renderer. The DXMT shader cache stays inside the app. D3DMetal and GPTK are not included. |
| **Steam UI** | Steam’s login window uses the existing CEF repair. Metal HUD is off for Steam and on for games. |
| **App icon** | WehniX icon on the bundle. |
| **Steam first-run crash (WoW64 / Rosetta)** | Fixes the intermittent `Steam.exe` page fault at `7BC41139` while "Updating Steam…". Under Rosetta 2, a switch between 32-bit and 64-bit mode could land in the wrong mode; Wine now checks the mode after each switch and retries. CryptoAPI providers stay loaded instead of being unloaded on every operation. |
| **Crash recovery** | No Wine debugger dialog. The Steam bootstrap retries if Wine crashes, and Steam is relaunched automatically after a crash (up to 3 times). |
| **DXMT window resize** | The DXMT view follows window resizes, so a game window that grows after start-up (for example a borderless fullscreen switch) no longer shows the image in one corner with black everywhere else. |
| **Steam networking** | Received TOS/TTL socket data is now delivered on macOS, fixing the Steam networking-sockets assertion "No control data returned even though we asked for TOS" in games that use it. |

11.17 does not claim that every Windows game runs. Online play and anti-cheat were not tested for this release.

### How to use 11.17

| Step | Action |
|:---:|:---|
| 1 | Download `WX-wine-11.17.tar.xz` from the [v11.17 release](https://github.com/wehnnit/WX-Wine/releases/tag/v11.17) |
| 2 | Extract it: `tar -xJf WX-wine-11.17.tar.xz` |
| 3 | Move `WX-wine-11.17.app` where you want to keep it |
| 4 | On Apple Silicon, install Rosetta if it is not already installed (`softwareupdate --install-rosetta`) |
| 5 | Open `WX-wine-11.17.app`. The first run downloads official Steam into the bundle |
| 6 | Install and launch games from that Steam client. DirectX games use DXMT |

---

## Downloads

| Engine | Release asset | Size (approx.) |
|:---|:---|:---|
| **WehniX Engine 11.11** | `WehniX Engine 11.11.zip` | ~1.3 GB |
| **WX-wine 11.17** | `WX-wine-11.17.tar.xz` | ~669 MB |

Future engines (11.0, GPTK packs, etc.) will be or not be published in this repository as separate tagged releases.

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
| **WX-wine 11.17** | Available — DXMT v0.80 only |
| WehniX Engine 11.0 | Won't Be released |
| Game Porting Toolkit 3.0 | Won't Be released |

---

## Legal

WehniX Wine engines are proprietary releases distributed by **WehniX**.  
Copyright © 2026 WehniX. All rights reserved.

Wine is used under its respective license. Third-party components (DXMT, MoltenVK, etc.) remain subject to their own licenses.

---
