<p align="center">
  <img src="https://img.shields.io/badge/Version-1.3.1-blue?style=for-the-badge" alt="Version">
  <img src="https://img.shields.io/badge/MC-1.21+-green?style=for-the-badge" alt="Minecraft">
  <img src="https://img.shields.io/badge/Java-21+-orange?style=for-the-badge" alt="Java">
  <img src="https://img.shields.io/badge/Paper-Supported-blueviolet?style=for-the-badge" alt="Paper">
</p>

# 🎨 WardrobePanel — Full Character Creator for Minecraft

**WardrobePanel** is a premium Minecraft plugin that lets players customise their skin through a web-based character editor. Players mix and match base skins, hairstyles, eye colours, clothing, accessories, and more — all rendered live in a 3D viewer, then applied to their in-game skin automatically.

---

## 📋 Table of Contents

- [Features](#-features)
- [Requirements](#-requirements)
- [Quick Setup](#-quick-setup)
- [Configuration Guide](#-configuration-guide)
- [Commands](#-commands)
- [Permissions](#-permissions)
- [PlaceholderAPI](#-placeholderapi)
- [Website Layouts](#-website-layouts)
- [Themes](#-themes)
- [Customising Assets](#-customising-website-assets)
- [Adding / Changing Overlays & Skins](#-adding--changing-overlays--skins)
- [Profiles & Saved Outfits](#-profiles--saved-outfits)
- [Owned Items System](#-owned-items-system)
- [Permission-Based Filtering](#-permission-based-filtering)
- [Troubleshooting](#-troubleshooting)
- [Support](#-support)

---

## ✨ Features

- 🌐 **Web-Based Character Editor** — players open a link in their browser, no mods needed
- 🧍 **Live 3D Preview** — powered by skinview3d with idle animation & zoom
- 👕 **Layered Overlay System** — hair, eyes, shirts, pants, jackets, shoes, accessories, beards, markings
- 🎨 **Full Colour Customisation** — skin tone palettes, eye colour, hair colour, per-item clothing colours with darkness/saturation/contrast sliders
- 👤 **Multiple Profiles** — each player can have up to N character profiles (configurable)
- 💾 **Saved Outfits** — name and save multiple outfit presets per profile, load them from sidebar or via commands
- 🔐 **Permission-Based Items** — control which items players can see/use per category or individually
- 🛒 **Owned Items System** — give/revoke items per player for shop integration
- 🏷️ **PlaceholderAPI** — 25+ placeholders for scoreboards, holograms, NPCs, etc.
- 🎭 **12 Colour Themes** — dark charcoal, midnight, ocean, forest, sunset, cherry, nether, end, royal, steampunk, pastel, arctic
- 📐 **6 Website Layouts** — classic, centered, compact, stacked, theater, minimal
- 🔄 **Auto Skin Apply** — skins are applied automatically when saved, and on join
- ⌨️ **Full Command Suite** — editor, load, loadfor, create, delete, rename, copy, setskin, resetskin, give, revoke, and more
- 🖼️ **Customisable Assets** — swap background, cursor, icons, and fonts easily

---

## 📦 Requirements

| Requirement | Version |
|---|---|
| Minecraft Server | **Paper/Purpur 1.21+** |
| Java | **21+** |
| MineSkin API Key | Free at [mineskin.org/apikey](https://mineskin.org/apikey) |
| SkinsRestorer | **Recommended** (for skin application) |
| PlaceholderAPI | **Optional** (for placeholders) |

---

## 🚀 Quick Setup

### Step 1: Install the Plugin
1. Drop `WardrobePanel-V1.3.1.jar` into your server's `plugins/` folder
2. Start your server once — the plugin will generate its config files and `web/` folder
3. Stop the server

### Step 2: Configure `config.yml`
Open `plugins/WardrobePanel/config.yml` and set these critical values:

```yaml
web:
  host: "0.0.0.0"           # ← ALWAYS leave this as 0.0.0.0
  port: 50424                # ← Pick an open port
  public-url: "http://YOUR_SERVER_IP:50424"  # ← Your real IP goes here!
  theme: "default"           # ← Any of the 12 themes
  layout: "classic"          # ← Any of the 6 layouts

mineskin:
  api-key: "YOUR_MINESKIN_API_KEY"  # ← Get from mineskin.org/apikey
```

> ⚠️ **Critical:** `host` must be `0.0.0.0`. Your public IP goes in `public-url` only!

### Step 3: Install the Setup Files
1. Unzip **`setup.zip`** — this contains the `web/assets/overlays/` and `web/assets/skins/` folders
2. Copy the extracted `web/` folder contents into `plugins/WardrobePanel/web/` (merge with existing)

### Step 4: Install the Assets
1. Unzip **`assets.zip`** — this contains icons, backgrounds, cursors, fonts
2. Copy the `assets/` folder into `plugins/WardrobePanel/web/` (merge with existing `assets/`)

### Step 5: Choose Your Layout
1. Unzip **`layouts.zip`** to see all 6 layout options
2. Copy `index.html` and `style.css` from your chosen layout folder into `plugins/WardrobePanel/web/`
3. Or simply set `web.layout: "theater"` (or any layout name) in `config.yml`

### Step 6: Open the Port
Make sure the port you chose (e.g. `50424`) is open in your hosting firewall.

### Step 7: Start & Test
1. Start the server
2. Run `/webchar editor` in-game — you'll receive a clickable link
3. Open the link in your browser — the character editor should load

---

## ⚙️ Configuration Guide

### `config.yml` — Full Breakdown

<details>
<summary><b>Web Server Settings</b></summary>

```yaml
web:
  enabled: true
  port: 50424
  host: "0.0.0.0"       # ALWAYS 0.0.0.0 — binds to all interfaces
  public-url: "http://YOUR_IP:50424"
  theme: "default"       # See Themes section
  layout: "classic"      # See Layouts section
```

| Key | Description |
|---|---|
| `enabled` | Enable/disable the web server |
| `port` | Port to listen on — make sure it's open in your firewall |
| `host` | **Always `0.0.0.0`** — do NOT put your IP here |
| `public-url` | The URL players use to access the editor. Must include `http://` |
| `theme` | Colour theme for the website |
| `layout` | Website layout template |

</details>

<details>
<summary><b>Profile Settings</b></summary>

```yaml
profiles:
  enabled: true
  max-per-player: 5
```

</details>

<details>
<summary><b>Feature Toggles</b></summary>

```yaml
features:
  skin-change: true
  skin-colour: true
  eye-colour: true
  eye-style: true
  hair-colour: true
  hair-style: true
  beard-style: true
```

Disable any feature to hide it from the web editor.

</details>

<details>
<summary><b>Skin Application</b></summary>

```yaml
skin-apply:
  auto-apply: true       # Apply skin when player saves in wardrobe
  apply-on-join: true    # Apply saved skin on player join
  apply-message: "&aYour custom skin has been applied!"
  apply-failed: "&cFailed to apply skin. Please try again later."
```

</details>

<details>
<summary><b>Session & Cooldown</b></summary>

```yaml
session:
  expiry-minutes: 1440   # 24 hours
  max-per-player: 1

cooldown:
  enabled: true
  seconds: 30
```

</details>

<details>
<summary><b>Messages</b></summary>

All messages support `&` colour codes:

```yaml
messages:
  prefix: "&8[&6WebChar&8] "
  link-message: "&aClick here to open your character editor: &n%link%"
  link-hover: "&7Click to open the character creator"
  session-created: "&aYour character editor link has been created!"
  session-expired: "&cYour session has expired. Use /webchar editor for a new link."
  no-permission: "&cYou don't have permission to do that."
  reload-success: "&aConfiguration reloaded! Overlays rescanned."
  server-not-running: "&cThe web server is not running. Contact an administrator."
  cooldown-message: "&cPlease wait %time% before requesting a new link."
```

</details>

---

## 💬 Commands

| Command | Description | Permission |
|---|---|---|
| `/webchar` | Open editor for default profile | `webchar.use` |
| `/webchar editor [profile]` | Open editor for a specific profile | `webchar.use` |
| `/webchar create <name>` | Create a new character profile | `webchar.use` |
| `/webchar delete <name>` | Delete a character profile | `webchar.use` |
| `/webchar list` | List all your profiles | `webchar.use` |
| `/webchar load <profile>` | Load/apply a profile's skin in-game | `webchar.use` |
| `/webchar apply <profile>` | Alias for `load` | `webchar.use` |
| `/webchar rename <old> <new>` | Rename a profile | `webchar.use` |
| `/webchar copy <source> <new>` | Duplicate a profile | `webchar.use` |
| `/webchar setskin <profile>` | Set a profile as your active skin | `webchar.use` |
| `/webchar resetskin` | Reset to your original Minecraft skin | `webchar.use` |
| `/webchar loadfor <player> <profile>` | Apply another player's profile to them | `webchar.admin` |
| `/webchar link <player> [profile]` | Generate editor link for another player | `webchar.link.others` |
| `/webchar give <player> <type> <id>` | Give an owned item to a player | `webchar.admin` |
| `/webchar revoke <player> <type> <id>` | Revoke an owned item | `webchar.admin` |
| `/webchar reload` | Reload config and rescan overlays | `webchar.reload` |
| `/webchar status` | Show plugin & web server status | `webchar.admin` |
| `/webchar sessions` | List all active sessions | `webchar.admin` |
| `/webchar help` | Show command help | `webchar.use` |

**Aliases:** `/wc`, `/character`

---

## 🔑 Permissions

| Permission | Description | Default |
|---|---|---|
| `webchar.use` | Use the character editor and basic commands | `true` |
| `webchar.admin` | Admin commands: loadfor, give, revoke, status, sessions | `op` |
| `webchar.reload` | Reload plugin configuration | `op` |
| `webchar.link.others` | Generate editor links for other players | `op` |
| `wardrobepanel.bypass` | Bypass all permission filtering (see all items) | — |
| `wardrobepanel.skin.<id>` | Access a specific base skin | — |
| `wardrobepanel.overlay.<category>.<id>` | Access a specific overlay | — |
| `wardrobepanel.overlay.<category>.*` | Access all overlays in a category | — |
| `wardrobepanel.overlay.*` | Access all overlays | — |

---

## 📊 PlaceholderAPI

> Requires [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/)

All placeholders use the prefix `%wardrobepanel_<placeholder>%`

### Profile Placeholders

| Placeholder | Description |
|---|---|
| `%wardrobepanel_profile_count%` | Number of profiles the player has |
| `%wardrobepanel_profile_current%` | Currently active profile name |
| `%wardrobepanel_profile_list%` | Comma-separated list of all profile names |
| `%wardrobepanel_profile_max%` | Maximum profiles allowed (from config) |
| `%wardrobepanel_profile_name_0%` | Profile name by index (0, 1, 2...) |
| `%wardrobepanel_last_profile%` | Last used profile name |

### Outfit Placeholders

| Placeholder | Description |
|---|---|
| `%wardrobepanel_outfit_skin%` | Current base skin ID |
| `%wardrobepanel_outfit_skin_color%` | Current skin palette |
| `%wardrobepanel_outfit_hair%` | Current hairstyle overlay ID |
| `%wardrobepanel_outfit_hair_color%` | Current hair colour palette |
| `%wardrobepanel_outfit_eye%` | Current eye overlay ID |
| `%wardrobepanel_outfit_eye_color%` | Current eye colour palette |
| `%wardrobepanel_outfit_shirt%` | Current shirt overlay ID |
| `%wardrobepanel_outfit_pants%` | Current pants overlay ID |
| `%wardrobepanel_outfit_shoes%` | Current shoes overlay ID |
| `%wardrobepanel_outfit_jacket%` | Current jacket overlay ID |
| `%wardrobepanel_outfit_accessory%` | Current accessory overlay ID |
| `%wardrobepanel_outfit_beard%` | Current beard overlay ID |
| `%wardrobepanel_outfit_marking%` | Current marking overlay ID |

### Web & Session Placeholders

| Placeholder | Description |
|---|---|
| `%wardrobepanel_web_url%` | Public URL of the web editor |
| `%wardrobepanel_skin_url%` | URL to the player's saved skin image |
| `%wardrobepanel_theme%` | Current theme name |
| `%wardrobepanel_session_active%` | `true`/`false` if player has active session |
| `%wardrobepanel_session_expires%` | Minutes until session expires |
| `%wardrobepanel_cooldown_remaining%` | Seconds left on link cooldown |

### Ownership & Stats Placeholders

| Placeholder | Description |
|---|---|
| `%wardrobepanel_owned_count%` | Total number of owned items |
| `%wardrobepanel_owned_<category>%` | Number of owned items in a category |
| `%wardrobepanel_owns_all%` | `true`/`false` if player owns everything |
| `%wardrobepanel_total_skins_applied%` | Total skin applications by this player |
| `%wardrobepanel_last_skin_change%` | Timestamp of last skin change |

---

## 📐 Website Layouts

WardrobePanel ships with **6 different website layouts**. Switch between them easily.

| Layout | Description |
|---|---|
| **`classic`** ⭐ | 3-column: Left sidebar \| Center viewer \| Right panel |
| **`centered`** | Full-screen viewer with floating glassmorphism panels |
| **`compact`** | Slim top bar + two-column (Viewer \| Panel) |
| **`stacked`** | Thin sidebar + vertical split (viewer top, panel bottom) |
| **`theater`** | Full-screen viewer with slide-out drawer panels |
| **`minimal`** | Full viewer + bottom bar + slide-out customiser |

### Switching Layouts

**Method 1 — Via config.yml (recommended):**
```yaml
web:
  layout: "theater"    # classic, centered, compact, stacked, theater, minimal
```
Then `/webchar reload`

**Method 2 — Manual copy:**
1. Navigate to `plugins/WardrobePanel/web/layouts/`
2. Open your chosen layout folder (e.g. `layout-theater/`)
3. Copy `index.html` and `style.css` into `plugins/WardrobePanel/web/` (overwrite existing)
4. Set `layout: "custom"` in config.yml to prevent overwrite on reload
5. Run `/webchar reload`

**Method 3 — Linux command:**
```bash
cp plugins/WardrobePanel/web/layouts/layout-theater/index.html plugins/WardrobePanel/web/index.html
cp plugins/WardrobePanel/web/layouts/layout-theater/style.css plugins/WardrobePanel/web/style.css
```

---

## 🎨 Themes

Set your theme in `config.yml`:

```yaml
web:
  theme: "midnight"
```

| Theme | Description |
|---|---|
| `default` | Dark charcoal with teal accents |
| `midnight` | Deep navy blue |
| `ocean` | Ocean blue tones |
| `forest` | Dark green woodland |
| `sunset` | Warm amber and orange |
| `cherry` | Deep magenta / cherry blossom |
| `nether` | Fiery red and dark crimson |
| `end` | Purple and dark void |
| `royal` | Deep purple and gold |
| `steampunk` | Bronze and copper tones |
| `pastel` | Soft pastel colours |
| `arctic` | Icy blue and white |

Themes are applied globally — all 6 layouts support all 12 themes.

---

## 🖼️ Customising Website Assets

You can swap out the visual assets without touching any code.

Navigate to `plugins/WardrobePanel/web/assets/` and replace these files:

| Path | What it is | Size to keep |
|---|---|---|
| `bg/bg.png` | Background image for the editor | Any resolution |
| `cursor/mouse.png` | Default cursor | 32×32 or similar |
| `cursor/mouse_click.png` | Cursor when clicking | 32×32 |
| `cursor/mousedraghover.png` | Cursor when hovering the 3D viewer | 32×32 |
| `cursor/mouse_drag.png` | Cursor when dragging the 3D viewer | 32×32 |
| `font/minecraft.woff2` | The font used throughout the UI | `.woff2` format |
| `icons/*.png` | Category icons in the panel (eyes.png, hairs.png, shirts.png, etc.) | 64×64 recommended |

> **Keep the same filenames and sizes** — just replace the PNGs.

After replacing, `/webchar reload` or restart the server.

---

## 👕 Adding / Changing Overlays & Skins

### Folder Structure

```
web/assets/
├── overlays/
│   ├── accessories/     ← Accessory overlays
│   ├── beards/          ← Beard overlays
│   ├── eyes/            ← Eye overlays
│   ├── hairs/           ← Hair overlays
│   ├── jackets/         ← Jacket overlays
│   ├── markings/        ← Marking overlays
│   ├── pants/           ← Pants overlays
│   ├── shirts/          ← Shirt overlays
│   ├── shoes/           ← Shoe overlays
│   └── skin-colours/    ← Base skin PNG files
├── skins/               ← Base skin files (used for preview rendering)
├── manifest.json        ← Auto-generated index of all overlays
└── catalog.json         ← Category definitions, palettes, colours
```

### Adding New Overlays

1. Create your overlay as a **64×64 PNG** (standard Minecraft skin format)
2. Only draw on the 2nd layer (overlay layer) of the skin template
3. Drop the PNG file into the appropriate category folder (e.g. `overlays/hairs/`)
4. Run `/webchar reload` in-game — the manifest is regenerated automatically
5. The new overlay will appear in the editor immediately

### Changing Base Skins

1. Replace or add PNGs in `overlays/skin-colours/`
2. Keep the naming convention: `base-steve-male.png`, `base-alex-female.png`, etc.
3. Run `/webchar reload`

> ⚠️ **Important:** When the plugin reloads or starts, it auto-scans all overlay folders and regenerates `manifest.json`. You never need to edit manifest.json manually.

---

## 👤 Profiles & Saved Outfits

### Profiles

Each player can have multiple character profiles (like RPG character slots):

- **Create:** `/webchar create MyWarrior`
- **List:** `/webchar list`
- **Edit:** `/webchar editor MyWarrior` — opens the web editor for that profile
- **Load/Apply:** `/webchar load MyWarrior` — applies that profile's skin in-game
- **Rename:** `/webchar rename MyWarrior MyKnight`
- **Copy:** `/webchar copy MyWarrior MyBackup`
- **Delete:** `/webchar delete MyWarrior`

### Saved Outfits

Within each profile, players can save multiple named outfits in the web editor:

1. Customise your character in the editor
2. Click the **+** button in the sidebar
3. Enter a name for the outfit
4. The outfit appears in the sidebar — click to load it anytime
5. Hover and click **✕** to delete

---

## 🛒 Owned Items System

Enable a shop-like system where players must "own" items before they can use them:

```yaml
owned-items:
  enabled: true
  starter-categories:
    - "eyes"               # Everyone gets all eyes for free
  starter-overlays: []     # Specific free overlays: ["hairs/short_hair"]
  combine-with-permissions: true
```

### Admin Commands

```
/webchar give <player> all                    — Give all items
/webchar give <player> category <name>        — Give all items in a category
/webchar give <player> overlay <category/id>  — Give a specific overlay

/webchar revoke <player> all                  — Revoke all items
/webchar revoke <player> category <name>      — Revoke items in a category
/webchar revoke <player> overlay <category/id>— Revoke a specific overlay
```

---

## 🔐 Permission-Based Filtering

Control which items players can see in the editor:

```yaml
permissions:
  enabled: true
  default-allowed: true    # true = see everything unless denied
  bypass-permission: "wardrobepanel.bypass"
```

### Permission Nodes

| Pattern | Example | Description |
|---|---|---|
| `wardrobepanel.skin.<id>` | `wardrobepanel.skin.base-steve-male` | Access to a specific base skin |
| `wardrobepanel.overlay.<cat>.<id>` | `wardrobepanel.overlay.hairs.male-90s_Side_Part` | Access to a specific overlay |
| `wardrobepanel.overlay.<cat>.*` | `wardrobepanel.overlay.hairs.*` | Access to all overlays in a category |
| `wardrobepanel.overlay.*` | — | Access to all overlays |
| `wardrobepanel.bypass` | — | See all items (bypass filtering) |

---

## 🔧 Troubleshooting

### "ERR_CONNECTION_REFUSED" / Site can't be reached

1. ✅ Make sure `host` is `"0.0.0.0"` in config.yml — NOT your IP
2. ✅ Make sure the port is open in your hosting firewall
3. ✅ Make sure `public-url` has `http://` prefix
4. ✅ Check the console — look for `Web server started on 0.0.0.0:PORT`

### "BindException: Cannot assign requested address"

You put your server IP in the `host` field. Change it to `"0.0.0.0"`.

### Skin not applying in-game

1. ✅ Check your MineSkin API key is valid
2. ✅ Make sure SkinsRestorer is installed
3. ✅ Try `/webchar load <profile>` manually
4. ✅ Check console for MineSkin API errors

### Web editor loads but shows "Session invalid"

1. ✅ Make sure `public-url` matches the URL you're visiting
2. ✅ Use a fresh link from `/webchar editor`
3. ✅ Sessions expire after the configured time (default: 24h)

### Overlays not showing after adding new files

1. ✅ Run `/webchar reload` to regenerate the manifest
2. ✅ Make sure overlays are 64×64 PNG files
3. ✅ Check the overlay is in the correct category folder

---

## 💬 Support

- **Discord:** [https://discord.gg/SG8jvb9WU5](https://discord.gg/SG8jvb9WU5)
- **GitHub Wiki:** [https://github.com/Anonventions/WardrobePanel-Wiki-V2](https://github.com/Anonventions/WardrobePanel-Wiki-V2)
- **Issues:** Report bugs on the Discord or GitHub

---

<p align="center">
  <b>Made by Anonventions</b><br>
  <sub>© 2025-2026 Anonventions. All rights reserved.</sub>
</p>
