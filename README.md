# UO Outlands on Mac (Apple Silicon)

[![GitHub stars](https://img.shields.io/github/stars/samdoidge/uo-outlands-mac?style=flat)](https://github.com/samdoidge/uo-outlands-mac/stargazers)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

Run the UO Outlands client on an Apple Silicon Mac without a Windows VM. Wine, a Sikarugir wrapper, and D3DMetal — with Razor and ClassicUO both working.

**Tested on** MacBook Pro M4 Pro, macOS 26.3. Apple Silicon is the supported path here; Intel Macs are untested.

**No game files are included.** Outlands is free to play and ships its own launcher.

## Why this setup

| Option | Tradeoff |
| --- | --- |
| **Wine + Sikarugir** (this guide) | No Windows licence or VM; roughly 5 GB installed; good performance |
| Parallels / VM | Full Windows, much heavier on RAM, CPU, and disk |
| CrossOver | Paid Wine wrapper; similar approach |

The Outlands client is a Windows build. Wine translates Windows calls to macOS; this is not a native macOS port, but it avoids a full VM.

## Prerequisites

1. **Rosetta 2** for Intel components:

   ```sh
   softwareupdate --install-rosetta
   ```

2. **Homebrew** — <https://brew.sh>

3. **Trust the Sikarugir tap.** Homebrew 7 refuses untrusted third-party taps, so the install fails without this:

   ```sh
   brew trust sikarugir-app/sikarugir
   ```

4. **Install Wine and Sikarugir:**

   ```sh
   brew install --cask wine-stable
   brew install --cask sikarugir
   ```

   Sikarugir's cask clears quarantine itself. On current Homebrew, do not add `--no-quarantine`; the flag no longer exists.

## Create the wrapper

1. Open **Sikarugir Creator** from Applications.
2. **Engine:** choose `WS12WineSikarugir10.0_1` (or the latest available).
3. **Create wrapper:** save as `Outlands.app` in `~/Applications/Sikarugir`.

## Configure the wrapper

1. Open `Outlands.app` — the Configure window appears.
2. Enable **Direct3D to Metal translation layer (D3DMetal)**. The client crashes without it.
3. **Winetricks** → install the MS .NET runtimes.
4. **Install Software** → select the [Outlands installer](https://patch.uooutlands.com/download).
5. **Windows app** → browse to `outlands.exe`, usually `C:\Program Files\Outlands\outlands.exe` or `C:\Outlands\outlands.exe`.

Point the wrapper at `outlands.exe` (the launcher), not `classicuo.exe`. The launcher is what keeps the client and Razor updated.

## Run

Double-click `~/Applications/Sikarugir/Outlands.app` (or launch it from Spotlight).

## Razor and ClassicUO windows

Razor and ClassicUO run inside the same Wine process, so macOS gives them one Dock icon. Switch windows with `Cmd` + backtick (`` ` ``) or the **Window** menu, which lists **ClassicUO** and **Razor Outlands Edition**.

## Troubleshooting

| Symptom | Fix |
| --- | --- |
| Audio static or popping | macOS **Audio MIDI Setup** → set the output device to 96 kHz |
| Installer download fails or hangs | Try a VPN; some ISPs and networks block the patcher |
| Keyboard input not working | Wrapper Configure → **Options** → check the keyboard mapping |
| Need config files or Razor scripts | Right-click the wrapper → **Show Package Contents** |
| Need to reconfigure the wrapper | **Show Package Contents** → `Contents/Configure.app` |
| Game crashes on launch | Confirm D3DMetal is enabled in the wrapper config |

## Notes

- Roughly 5 GB after the full install.
- Razor scripts work; users report running complex boss scripts without issues.
- Performance is generally good on Apple Silicon; this is still Wine, so treat client updates as the thing most likely to break.
- Official install guide: <https://uooutlands.com/connecting/>
- Rules: <https://uooutlands.com/rules/>
- Discord: <http://discord.uooutlands.com>
- Credit: based on Vercillo's method from the Outlands Discord `#unofficial-mac-linux-support` channel.

## Legal

Outlands is free to play and provides its own launcher. This repository contains no game files. Use the official ClassicUO + Razor clients and follow the Outlands rules.

If this saved you an evening, star the repo — it helps other Mac players find it.
