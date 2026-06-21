# ⚡ MotionForge

**A free, open-source Roblox Studio plugin for building custom combat moves visually.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Roblox](https://img.shields.io/badge/Roblox-Creator%20Store-blue)](https://create.roblox.com/store/asset/80433496048831/MotionForge-Beta)
[![Made with Lua](https://img.shields.io/badge/Made%20with-Lua-2C2D72?logo=lua&logoColor=white)](https://www.lua.org/)

## 📖 Table of Contents

- [Features](#-features)
- [Installation](#-installation)
- [Quick Start](#-quick-start)
- [Usage Example](#-usage-example)
- [Animation Preview](#-animation-preview)
- [Export Options](#-export-options)
- [Built-in Templates](#-built-in-templates)
- [Why MotionForge?](#-why-motionforge)
- [Support Development](#-support-development)
- [License](#-license)

---

## 🎮 Features

| Feature | Description |
| :--- | :--- |
| **Visual Timeline Editor** | Add hitboxes, sounds, and effects at specific times with a simple click |
| **Hitbox Visualizer** | See your hitbox in real-time with color-coded damage (green → yellow → red) |
| **Cutscene System** | Camera shake, zoom, and rotation effects for epic super moves |
| **One-Click Export** | Generate clean, professional Lua code instantly |
| **Save/Load** | Persistent move storage across Studio sessions |
| **Template Library** | Built-in templates (Dragon Punch, Kamehameha, etc.) + save your own |
| **Animation Preview** | Spawn a dummy, load your Animation ID, and play/pause/stop with adjustable speed |
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

---

## ⚡ Quick Start

1. Open the **MotionForge** panel from the Plugins tab
2. Click **+ New Move** and give it a name
3. Use **+ Add Event** to drop hitboxes, sounds, and effects onto the timeline
4. Use **Animation Preview** to spawn a dummy, load your Animation ID, and test playback before exporting
5. Preview the hitbox in real time and adjust timing/knockback as needed
6. Click **Export** to generate the Lua module for your move

---

## 💻 Usage Example

Once you've exported a move, use it in your game like this:

```lua
-- In your game script
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local DragonPunch = require(ReplicatedStorage.MotionForge_Moves.DragonPunch)

-- When the player attacks
DragonPunch.Execute(character)

-- The move handles:
-- ✅ Animation playback
-- ✅ Hitbox detection
-- ✅ Damage application
-- ✅ Knockback
-- ✅ Sound effects
-- ✅ Visual effects
-- ✅ Cutscene effects (camera shake, zoom, rotation)
-- ✅ Cooldown management
```

---

## 🎬 Animation Preview

Want to see exactly how your move looks before exporting? The built-in Animation Preview lets you test your animation on a dummy character right inside Studio — no need to run the game.

| Control | Description |
| :--- | :--- |
| **Create Dummy** | Spawns a custom dummy character in your Studio workspace |
| **Load Animation** | Loads your move's Animation ID onto the dummy |
| **Play Preview** | Plays the animation on the dummy |
| **Pause** | Pauses playback at the current frame |
| **Stop** | Stops and resets the animation back to the start |
| **Speed** | Adjusts playback speed — choose from 0.25x, 0.5x, 0.75x, 1.0x, 1.5x, or 2.0x |

> 💡 **Tip:** Use slow speeds like **0.25x** or **0.5x** to fine-tune hitbox timing — you can see exactly which frame each event fires on.

---

## 📦 Export Options

| Method | Description |
| :--- | :--- |
| **Copy to Clipboard** | Copies the Lua code directly to your clipboard |
| **Export to ReplicatedStorage** | Automatically creates the HitboxSystem module and your move module in your game |

---

## 🛠️ Built-in Templates

| Template | Description |
| :--- | :--- |
| 🐉 **Dragon Punch** | A powerful uppercut that launches enemies skyward |
| 🌊 **Kamehameha** | Charge up and release a devastating energy beam |
| 🌀 **Spin Kick** | A rapid spinning kick that hits multiple times |
| 💥 **Ground Slam** | Slam the ground, damaging and knocking back nearby enemies |

---

## ❓ Why MotionForge?

| Traditional Workflow | With MotionForge |
| :--- | :--- |
| Write hitbox detection code from scratch | Click "+ Add Event" → Hitbox |
| Manually calculate timing and knockback | Set time (0.3s) and knockback (500) |
| Test, tweak, re-test repeatedly | See hitbox preview in real-time |
| Write animation loading code | Just paste Animation ID |
| Run the full game just to test an animation | Preview on a dummy at any speed, inside Studio |
| Code sound effects and VFX | Add Sound/Effect events visually |
| Hours of work | Minutes of work |

---

## 💖 Support Development

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

## 📄 License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT) — free to use, modify, and distribute, including in commercial projects.
