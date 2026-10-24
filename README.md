# ⚡ MotionForge

**A free, open-source Roblox Studio plugin for building custom combat moves visually.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/Version-v1.6.1-brightgreen)](https://github.com/hopeigbinosa123/MotionForge/releases)
[![Roblox](https://img.shields.io/badge/Roblox-Creator%20Store-blue)](https://create.roblox.com/store/asset/80433496048831/MotionForge-Beta)
[![Made with Lua](https://img.shields.io/badge/Made%20with-Lua-2C2D72?logo=lua&logoColor=white)](https://www.lua.org/)

## 📖 Table of Contents

- [Features](#-features)
- [Installation](#-installation)
- [Quick Start](#-quick-start)
- [Hitbox Fields](#-hitbox-fields)
- [Usage Example](#-usage-example)
- [Animation Preview](#-animation-preview)
- [Cutscene Controls](#-cutscene-controls)
- [Save / Load](#-save--load)
- [Export Options](#-export-options)
- [Built-in Templates](#-built-in-templates)
- [Notes and Limits](#-notes-and-limits)
- [Why MotionForge?](#-why-motionforge)
- [Support Development](#-support-development)
- [Changelog](#-changelog)
- [License](#-license)

---

## 🎮 Features

| Feature | Description |
| :--- | :--- |
| **Visual Timeline Editor** | Add hitboxes, sounds, and effects at specific times with a simple click, with copy and paste |
| **Full Hitbox Control** | Damage, knockback, size, forward offset, and active time per hit, with input validation |
| **Hitbox Visualizer** | See the hitbox drawn on a dummy, color-coded by damage. Click an event to preview that hitbox |
| **Cutscene System** | Camera shake, zoom, rotation, and slow motion, played on the client, with a live preview |
| **Combat Hooks** | `OnHit`, `CanHit`, and a handle with `Cancel()` so your combat scripts stay in control |
| **Safe One-Click Export** | Valid Lua every time. Re-exporting updates in place and never creates duplicates |
| **Save/Load** | Persistent move storage across Studio sessions |
| **Template Library** | Built-in templates (Quick Jab, Dragon Punch, Kamehameha, etc.) + save your own |
| **Animation Preview** | Spawn a dummy, load your Animation ID, and play it with hitboxes flashing at their event times |
| **Free & Open Source** | MIT License — use it anywhere, modify it freely |

---

## 📥 Installation

### Method 1: Roblox Creator Store (Recommended)

1. Open **Roblox Studio**
2. Go to the **Plugins** tab
3. Click the **Toolbox** icon
4. Search for **"MotionForge"**
5. Click **Install**

### Method 2: Manual Install

1. Download `MotionForge.rbxmx` from [Releases](https://github.com/hopeigbinosa123/MotionForge/releases)
2. In Roblox Studio, go to **Plugins** → **Plugins Folder**
3. Place the file in the folder
4. Restart Studio

> When you first export, Studio may ask for script injection permission. Allow it, since MotionForge needs it to write the move scripts into your game.

---

## ⚡ Quick Start

1. Open the **MotionForge** panel from the Plugins tab
2. Give your move a name. Use `Character_Move`, for example `GlitchKing_LightPunch`. The name becomes the module name on export
3. Use **+ Add Event** to drop hitboxes, sounds, and effects onto the timeline
4. Turn on **Hitbox Preview** and tune size and offset against the dummy
5. Use **Play Preview** to watch the hitboxes fire at their event times, with or without an animation
6. Click **Export to ReplicatedStorage** to generate your move

Starting another move? Click **🆕 New Move** in the Save / Load card (save the current one first).

---

## 🎯 Hitbox Fields

Click the ✏️ on a Hitbox event to edit it.

| Field | Meaning |
| :--- | :--- |
| **Damage** | Damage dealt on hit |
| **Knockback** | Studs per second of velocity. **30** weak, **50** normal, **100** launcher (max 300) |
| **Hitbox Size** | `X,Y,Z` in studs, for example `4,4,4` |
| **Offset** | Studs in front of the fighter's root part |
| **Active** | Seconds the hitbox stays live |

The **Damage** and **Knockback** boxes in the Combat Stats card are defaults for *new* hitbox events. Use **Apply to all hitboxes** to push them onto existing ones.

---

## 💻 Usage Example

Once you've exported a move, call it from a **server** Script:

```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local move = require(ReplicatedStorage.MotionForge_Moves.GlitchKing_LightPunch)

local handle = move.Execute(character, {
    OnHit = function(hit)
        hit.Damage = hit.Damage * 2   -- edit values, or return false to apply damage yourself
    end,
    CanHit = function(model)
        return model ~= myTeammate    -- return false to ignore a target
    end,
})

if handle then
    handle.HitConnected:Connect(function(hit) end)
    handle.Finished:Connect(function(wasCancelled) end)
    -- handle:Cancel() when the fighter is stunned
end
```

`Execute` returns `nil` if the move couldn't start (on cooldown, dead, or called from a client).

The move handles:

- ✅ Animation playback
- ✅ Hitbox detection (one hit per target per hitbox)
- ✅ Damage and knockback
- ✅ Sound effects
- ✅ Placeholder visual effects
- ✅ Cutscene effects, sent to the player who used the move
- ✅ Cooldown management

**`hit` fields:** `Attacker`, `Character`, `Humanoid`, `RootPart`, `Position`, `Direction`, `Damage`, `Knockback`, `HitIndex`, `Move`

**`move.Data`** holds real numbers from the first Hitbox event for your own combat code: `Startup`, `Active`, `Damage`, `Knockback`, `HitboxSize`, `HitboxOffset`, `Hits`, `Duration`, `Cooldown`, `AnimationId`.

---

## 🎬 Animation Preview

Test your move on a dummy character right inside Studio — no need to run the game.

| Control | Description |
| :--- | :--- |
| **Create Dummy** | Spawns an R15 dummy in your workspace, turned sideways so you can see hitbox reach |
| **Load Animation** | Loads your move's Animation ID onto the dummy |
| **Play Preview** | Plays the animation and flashes each hitbox at its event time. Works without an animation too |
| **Stop** | Stops playback |
| **Speed** | Cycles playback speed: 0.25x, 0.5x, 1x, 1.5x, 2x |

> 💡 **Tip:** Use **0.25x** or **0.5x** to fine-tune hitbox timing against your animation.

The dummy is removed automatically when you close the panel.

---

## 🎥 Cutscene Controls

Turn on **Cutscene Effects**, then enable the effects you want:

| Control | Description |
| :--- | :--- |
| **Duration** | How long shake and zoom last |
| **Slow Motion** + factor | Slows the move's animation (factor 0.05–1) |
| **Camera Shake** + intensity | Shake that fades out over the duration |
| **Zoom Effect** + amount | Field of view zooms in and back out |
| **Camera Rotate** + angle, speed, direction | Camera swings around the fighter by the angle at the given degrees/second, then returns smoothly. Clockwise or counter-clockwise |

> 💡 **Tip:** Click **🎬 Preview Cutscene** to see all effects live inside Studio. They start at the first hitbox, just like in game.

---

## 💾 Save / Load

MotionForge saves your moves persistently across Studio sessions using plugin storage — no external files needed.

- **Save Current Move** — saves your move by name
- **Load** — click any saved move in the list to load it instantly
- **Delete** — click the 🗑️ next to a saved move
- **New Move** — resets the editor to a blank move

> 💡 **Tip:** Move names are used as save keys, so renaming a move before saving creates a separate save entry.

---

## 📦 Export Options

| Method | Description |
| :--- | :--- |
| **Export to ReplicatedStorage** | Creates or updates your move and the shared runtime in your game |
| **Copy Code** | Shows the move code and the three runtime scripts to copy by hand |

Export creates:

| Instance | Location |
| :--- | :--- |
| Your move (ModuleScript) | `ReplicatedStorage.MotionForge_Moves` |
| `HitboxSystem` | `ReplicatedStorage` |
| `MotionForge_Cutscene` | `ReplicatedStorage` |
| `MotionForge_CutsceneRemote` (RemoteEvent) | `ReplicatedStorage` |
| `MotionForge_Client` (LocalScript) | `StarterPlayer.StarterPlayerScripts` |

Re-exporting overwrites these in place and removes duplicates. A same-named script that isn't MotionForge's is never touched.

---

## 🛠️ Built-in Templates

| Template | Description |
| :--- | :--- |
| 👊 **Quick Jab** | Fast light attack, a good base for a light punch |
| 🐉 **Dragon Punch** | A powerful uppercut with a fire burst |
| 🌊 **Kamehameha** | A long, narrow energy beam that reaches far |
| 🌀 **Spin Kick** | A rapid three-hit spinning kick |
| 💥 **Ground Slam** | A wide slam that hits everything around the fighter |

---

## ⚠️ Notes and Limits

- **Animation ownership:** Roblox only plays animations owned by the experience owner or group, or by Roblox. Other animations fail to load.
- **Knockback** is most reliable when the target's physics is owned by the server (`SetNetworkOwner(nil)`).
- **Slow motion** slows the move's animation only. Hit timing stays in real time.
- **Effects** are simple placeholder visuals (Basic Explosion, Fire Explosion, Energy Beam, Ground Crack, Shockwave). Swap in your own VFX later.
- **Sounds** with the placeholder ID `rbxassetid://123456789` stay silent.
- Call `Execute` from the **server**. Cutscenes need the exported `MotionForge_Client` LocalScript.

---

## ❓ Why MotionForge?

| Traditional Workflow | With MotionForge |
| :--- | :--- |
| Write hitbox detection code from scratch | Click "+ Add Event" → Hitbox |
| Manually calculate timing and knockback | Set time (0.3s) and knockback (50) |
| Test, tweak, re-test repeatedly | See hitbox preview in real-time |
| Write animation loading code | Just paste Animation ID |
| Run the full game just to test an animation | Preview on a dummy at any speed, inside Studio |
| Code sound effects and VFX | Add Sound/Effect events visually |
| Hours of work | Minutes of work |

---

## 💖 Support Development

> 💡 There's a **❤️ Support** button built right into the plugin's status bar at the bottom of the panel — click it anytime to see all the ways to support MotionForge without leaving Studio.

- 💵 **PayPal:** [paypal.me/Gorrilla567h](https://paypal.me/Gorrilla567h)
- ☕ **Ko-fi:** [ko-fi.com/gamegeektech_hope](https://ko-fi.com/gamegeektech_hope)
- 🤖 **Roblox:** Send Robux to [Gorrilla567_h](https://www.roblox.com/users/5241414167/profile)

> If you want to send Robux, you'll need Roblox Premium.

### ⭐ Show Your Support

If you like MotionForge, please:

- ⭐ Star this repository
- 📦 Install the plugin on Roblox
- 💬 Share it with other developers
- 👤 Follow me on Roblox as well (just for me to be happy a little 😄)

Thank you! 🚀

---

## 📋 Changelog

### v1.6.1 — Combat Hooks Release
- ✅ **Valid exports** — the cutscene is now written as a real Lua table instead of raw JSON
- ✅ **Combat hooks** — `Execute` returns a handle with `Cancel()` and `Started` / `HitConnected` / `Finished` signals, plus `OnHit` and `CanHit` options
- ✅ **Real `Move.Data`** — startup, active time, damage, knockback, hitbox size and offset from the first hitbox
- ✅ **Hitbox dialog** — Knockback, Offset, and Active fields added, with validation
- ✅ **Sane knockback** — 0–300 scale applied with `ApplyImpulse`. Older saves and templates are converted automatically
- ✅ **Safe re-export** — overwrites in place, removes duplicates, never touches scripts that aren't MotionForge's
- ✅ **Client-side cutscenes** — new controls for duration, slow factor, shake, zoom, rotation angle, speed and direction, plus Preview Cutscene
- ✅ **Better preview** — hitbox drawn on the dummy, timed hitbox playback, playback speed button
- ✅ Placeholder effects, New Move button, delete buttons for saved moves, template descriptions
- 🐛 Fixed template toggles not refreshing after loading, and status messages blocking the UI

### v1.6.0
- ✅ Copy and paste events
- ✅ Hitbox size and offset fields
- ✅ Bug fixes from the v1.5.0 audit

### v1.4.3 — Stability Release
- ✅ **Exporter completely fixed** — exported moves now generate valid, error-free Lua code
- ✅ **Correct HitboxSystem path** — exports now use `game:GetService("ReplicatedStorage").HitboxSystem` instead of the broken `script.Parent.HitboxSystem`
- ✅ **All export syntax bugs resolved** — exported moves load and run correctly without errors
- ✅ Plugin is now fully stable and production-ready

---

## 📄 License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT) — free to use, modify, and distribute, including in commercial projects.
