# Vanity

Vanity is a Paper/Purpur character creator plugin with a browser editor, store,
closet, lore, profile switching, themed UI shells, and MineSkin application.
Players open it with `/vanity`, build a look in the web UI, save outfits, buy
items, and apply the final skin back in-game.

Current release: **1.9.2**

## Updates in 1.9.2

- Refresh skins through Paper's public profile API. Skin changes no longer reset maximum health or briefly reduce a player's health.
- Look up the original Mojang skin asynchronously when resetting a skin, so a network lookup does not block the server tick.
- Update the setup and upgrade instructions for Paper 26.3 and Java 25.

## Updates In 1.9.1

- Fixed the intermittent `Failed to fetch dynamically imported module:
  /js/ui/toolbar.js` error that could leave a selected character on the loading
  screen.
- Changed editor startup to load its viewer, creator panel, and toolbar in a
  controlled sequence with three bounded, cache-busted recovery attempts.
  Rejected startup state is cleared so reopening a character can recover instead
  of permanently reusing the first failed request.
- Reduced the toolbar's initial dependency graph. Settings, store, closet, lore,
  inventory, and Overlay Library modules now load only when their controls are
  opened, with the same bounded retry behavior.
- Made bundled web-file extraction atomic, preventing a failed write or server
  interruption from leaving a zero-byte or partially written JavaScript file.
- Added a packaged-resource fallback to the embedded web server. If an extracted
  core web asset is missing, empty, or temporarily unreadable, Vanity serves the
  verified copy inside the JAR instead of returning a startup-breaking 404.
- Added a browser regression that deliberately fails the first toolbar request
  and verifies that the complete editor still opens successfully.

## Updates In 1.9.0

- Added **68 complete character-creator presets** to the administrator panel.
  Each curated option pairs a visual theme, a materially different workspace
  structure, and a matching loading animation; admins can search the library or
  fine-tune the three layers independently.
- Added a dedicated loading-screen studio with **16 animation systems**: orbit,
  dual orbit, brand progress, crafting blocks, pulse beacon, character scanner,
  wardrobe doors, mannequin, pixel rain, constellation, rune, tailor stitch,
  outfit carousel, portal, colour wave, and logo reveal.
- Made loading-screen branding fully configurable from the browser: title,
  caption, scale, background colour, primary colour, secondary colour, caption
  visibility, and live-status visibility all have an immediate preview.
- Published theme, layout, preset, and loading-screen changes now persist to
  `config.yml` and propagate to connected editors through the live-update
  stream without requiring a website refresh.
- Fixed the shared panel cascade that could replace a theme's dedicated viewer
  surface and produce white-on-white screens. Viewer headings now use bounded,
  responsive typography, and the Dressing Room shell no longer clips wide
  titles or creates horizontal overflow.
- Fixed the Wardrobe Doors loader so both animated panels retain their intended
  width, and made the original orbit trail follow the selected primary colour.
- Added server-side allowlists, length limits, strict `#RRGGBB` validation, and
  safe fallback values for every loading-screen setting, plus new browser and
  regression coverage for the option count, loader contract, contrast, and
  responsive bounds.

## Updates In 1.8.0

- Added a browser-based administrator control room at `admin.html`. Server
  owners can preview every theme and structural layout, pair them, and publish
  the result without editing YAML or running an in-game command.
- Added a protected administrator login-marker exchange. The marker becomes a
  short-lived server-side session carried by an HttpOnly, SameSite cookie;
  mutations also require a CSRF token and failed logins are rate limited.
- Added an individual overlay workbench for every supported section. Admins can
  drag in one 64x64 PNG, choose its model/gender group, and let Vanity sanitize
  the filename, select the canonical folder, rebuild the manifest, and refresh
  connected editors.
- Added four materially different character-creator experiences: **Avatar
  Studio** (editorial boutique), **Pop Catalog** (dense storefront), **Dressing
  Room** (touch-first vertical creator), and **Pixel Wardrobe** (compact game
  library). These use new structural layouts, not palette-only variants.
- Added a public, read-only live-update stream. Theme/layout changes apply to
  open editors immediately, and catalog mutations trigger an automatic manifest
  refresh without forcing players to reopen the site.
- Hardened the new administration surface with bounded requests, strict PNG
  validation, collision-safe atomic writes, path containment, malformed-input
  handling, CSP/frame protections, pack-ownership safeguards, and regression
  coverage for authentication, importer security, live refresh, and theme
  structure.

## Updates In 1.7.1

- Added automatic overlay-system detection for website ZIP uploads. Supported
  assets can now be nested anywhere in a pack or identified by a flat filename.
- Added category and model aliases for common pack conventions, including
  singular folders, spaces, underscores, mixed casing, Steve/classic,
  Alex/slim, gender names, and unisex assets.
- Added automatic folder correction, including `skin_colours`, `skin-colors`,
  and related spellings to Vanity's canonical `skin-colours` base-skin system.
- Added collision-safe renaming for duplicate asset filenames and skips unrelated
  preview PNGs without rejecting an otherwise valid pack.
- Added import feedback showing corrected and skipped files, plus regression tests
  for deeply nested, aliased, flat-file, model, and skin-colour pack layouts.

## Updates In 1.7.0

- Added authenticated ZIP asset-pack uploads to the website **Overlay Library**.
- Added upload/remove management with immediate catalog refresh and automatic
  ownership grants for imported overlays.
- Added strict upload validation: zip-slip protection, compressed/expanded size
  limits, file-count limits, filename sanitisation, and readable 64x64 PNG checks.
- Added saved per-outfit overlay priority. Use **Layer order** in the Creator to
  move pants below long shirts/tunics or change any other equipped layer order.
- Fixed `profiles.enabled: false`: the web editor now opens directly, profile
  controls are hidden, stale profile sessions are cleared, and profile CRUD APIs
  reject mutations while the feature is disabled.
- Hardened static and overlay file path containment and bounded JSON request bodies.
- Made profile and owned-item persistence operations thread-safe for concurrent
  requests from the embedded web server.
- Added Java archive-security tests and browser layer/profile regression tests.

## What It Does

- Web character editor with no frontend build step
- Login-marker-protected browser administrator panel
- Multiple character profiles per player
- User-uploadable overlay asset packs
- Per-outfit overlay layer priority
- Creator, Store, Closet, lore, and outfit application
- Admin-selectable themes and desktop layouts
- 68 searchable theme/layout/loading presets
- 16 customizable loading-screen systems
- Separate character, customisation, skin-colour, and hair-colour token pools
- Vault economy with PlaceholderAPI + command fallback
- Permission-based or ownership-based item access
- Height scaling through Bukkit's player scale attribute
- Per-server colour palette restrictions
- Optional aging skin-tone overlays and web hooks

## Requirements

- Paper/Purpur 1.21.x; Paper 26.3 server startup checked
- Java 21 on 1.21.x; Java 25 on 26.3
- MineSkin API key if you want web saves to apply skins
- Optional: Vault, PlaceholderAPI, LuckPerms

## Install

1. Put `Vanity.jar` in `plugins/`.
2. Start the server once.
3. Edit `plugins/Vanity/config.yml`.
4. Set `web.public-url` to the public domain or IP players will open.
5. Restart or run `/vanity reload`.
6. Give players `vanity.use`.
7. Run `/vanity` in-game to confirm the editor link works.
8. Open `<web.public-url>/admin.html` and use the marker generated at
   `admin-panel.login-marker` to enter the administrator control room.

If `plugins/WardrobePanel/` exists, Vanity copies missing data from it into
`plugins/Vanity/` on first boot. It does not delete the old folder.

## Updating to 1.9.2

Back up `plugins/Vanity` and any remaining `plugins/WardrobePanel` directory.
Stop the server, replace the old JAR with `Vanity-1.9.2.jar`, and start it again.
Keep only one Vanity/WardrobePanel JAR installed. Existing profiles, owned items,
overlays, themes, and configuration stay in the data directory.

For Paper 26.3, run Java 25. Test opening a character, applying a skin, restoring
the original skin, and switching a profile on your staging server. Confirm that
current and maximum health stay unchanged by a skin refresh. MineSkin needs a
working API key, and the player-facing site should use HTTPS. Server startup
and regression tests do not establish live MineSkin delivery or every browser
and Minecraft client combination.

## First Configuration Pass

These are the settings to get right first:

- `web.public-url`: required for valid clickable links
- `mineskin.api-key`: required for applying finished looks
- `themes.default`: active theme
- `layout.default`: active desktop layout
- `loading-screen.*`: loading motion, copy, colours, visibility, and scale
- `owned-items.enabled`: whether store ownership gates creator items
- `permissions.enabled`: whether permission nodes gate items
- `economy.*`: Vault / placeholder economy settings
- `scale.steps`: explicit allowed height values
- `background.*`: site background source and dim/blur
- `admin-panel.login-marker`: private browser administrator credential

## Administrator Control Room

Open:

```text
https://your-vanity-domain.example/admin.html
```

When `admin-panel.login-marker` is blank, Vanity generates a random marker on
the first boot, writes it to `plugins/Vanity/config.yml`, and prints it once to
the server console. Treat it like a password and serve the panel over HTTPS.

```yaml
admin-panel:
  enabled: true
  login-marker: "replace-with-a-long-random-secret"
  session-minutes: 60
  max-login-attempts: 5
  lockout-minutes: 15
  trust-proxy-headers: false
  bind-session-to-ip: false
  max-overlay-size-kb: 512
```

The marker is submitted only to `/api/admin/login`; it is not placed in the URL,
browser storage, or JavaScript after login. The returned cookie is HttpOnly,
SameSite Strict, limited to `/api/admin`, and marked Secure when Vanity is
published through HTTPS. Admin mutations require the session's CSRF token.
Set `trust-proxy-headers: true` only when a trusted reverse proxy strips
client-supplied forwarding headers; this lets login rate limits use the original
client IP and recognizes proxy-terminated HTTPS.

From the panel an administrator can:

- choose from 68 complete creator presets;
- preview and publish any theme/layout pairing;
- choose one of 16 loading animations and customize its title, caption, size,
  background, two accent colours, caption visibility, and status visibility;
- upload one validated 64x64 PNG to any supported overlay section;
- choose the model or gender variant while Vanity creates the canonical folder;
- remove individually managed assets; and
- see catalog totals and live refresh status.

Assets owned by a user-uploaded ZIP pack must still be removed through **Overlay
Library** so the pack registry and ownership grants stay consistent.

## Commands

```text
/vanity
/vanity help
/vanity reload
/vanity theme [list|current|set <theme>|<theme>]
/vanity layout [list|current|set <layout>|<layout>]
/vanity token <amount> <player> [character|cust|skin|hair]
/vanity <player> lore
/vanity <player> lore set <text...>
/vanity <player> lore delete

/webchar ...        legacy compatibility command
```

`theme` and `layout` are admin-only. Players can no longer switch themes from
the website.

## Permissions

```text
vanity.use
vanity.admin
vanity.lore.others
vanity.bypass
vanity.skin.<skin-id>
vanity.skin.*
vanity.overlay.<category>.<overlay-id>
vanity.overlay.<category>.*
vanity.overlay.*
vanity.overlay.upload
vanity.*
```

Legacy `webchar.*` and `wardrobepanel.*` checks still exist for older servers.

## Folder Layout

```text
plugins/Vanity/
  config.yml
  messages.yml
  palettes.yml
  shop.yml
  heights.yml
  overlays/
    hairs/
    eyes/
    eyebrows/
    beards/
    shirts/
    jackets/
    pants/
    shoes/
    accessories/
    hats/
    markings/
  skins/
  skin-tones/
  playerdata/
  profiles/
  overlay-packs.json
  web/
```

`plugins/Vanity/web/` is the live website. Edit that folder on the server if
you want to customise HTML, CSS, JS, assets, or bundled themes.

## Themes

Bundled themes:

```text
avatar-studio
pop-catalog
dressing-room
pixel-wardrobe
modern-dark
modern-light
mmorpg
medieval
fantasy
sci-fi
obsidian
executive
ember
neon-noir
nordic
royal
terminal
```

Each bundled theme has its own:

- `themes/<theme>.css`
- `assets/bg/<theme>/bg.png`
- `assets/cursor/<theme>/default.png`
- `assets/cursor/<theme>/active.png`
- `assets/cursor/<theme>/drag.png`
- icon pack / font mapping in `web/js/lib/themeAssets.js`

Change the active theme:

```text
/vanity theme list
/vanity theme current
/vanity theme sci-fi
```

Or edit `config.yml`:

```yaml
themes:
  default: sci-fi
  allow-player-switch: false
```

## Layouts

Bundled admin-selectable desktop layouts:

```text
boutique
marketplace
dressing-room
pixel-wardrobe
command
showcase
atelier
split
compact
catalog
```

Change the active layout:

```text
/vanity layout list
/vanity layout current
/vanity layout showcase
```

Or edit `config.yml`:

```yaml
layout:
  default: showcase
```

## Loading Screen

The protected administrator panel includes a live loading-screen studio. Its
preview is private until **Publish loader** is pressed; publication persists the
choice and updates already-open editors in real time.

The same settings can be managed in `config.yml`:

```yaml
loading-screen:
  style: orbit
  title: "VANITY"
  caption: "Character creator"
  accent: "#65a7ff"
  secondary: "#ff66b8"
  background: "#000000"
  show-caption: true
  show-status: true
  size: standard       # compact | standard | large
```

Available styles are `orbit`, `dual-orbit`, `progress`, `blocks`, `pulse`,
`scanner`, `wardrobe`, `mannequin`, `pixel-rain`, `constellation`, `rune`,
`stitch`, `carousel`, `portal`, `wave`, and `logo`.

## Backgrounds

Global background config lives in `config.yml`:

```yaml
background:
  type: room3d   # static | gif | video | room3d
  source: ""     # path under web/assets/ when using static/gif/video
  blur: 0
  dim: 0.3
```

Theme-specific background images live under:

```text
plugins/Vanity/web/assets/bg/<theme>/bg.png
```

Swap those files when you want different per-theme stage art.

## Viewer Lighting

Main preview lighting is server-configured:

```yaml
viewer-lighting:
  enabled: true
  mode: studio     # studio | uniform
  intensity: 1.0
  azimuth: 35.0
  elevation: 55.0
  ambient: 0.58
  exposure: 1.48
```

- `studio` keeps directional lighting
- `uniform` flattens the light for cleaner colour checking

The website lighting button edits the preview values for that session. The
configured defaults still come from `config.yml`.

## Categories And Tabs

The creator tab order is driven by `config.yml`:

```yaml
categories:
  order:
    - base
    - eyes
    - eyebrows
    - hairs
    - beards
    - shirts
    - jackets
    - pants
    - shoes
    - accessories
    - hats
    - markings
```

Labels are also configurable there.

## Adding Base Skins

Base skins live in:

```text
plugins/Vanity/skins/
```

Typical ids follow the shipped model/gender variants:

- `base-steve-male`
- `base-alex-male`
- `base-alex-female`

If you add or remove base skins, run:

```text
/vanity reload
```

## Adding Overlays

Overlay PNGs live in:

```text
plugins/Vanity/overlays/<category>/
```

Supported categories:

```text
hairs
eyes
eyebrows
beards
shirts
jackets
pants
shoes
accessories
hats
markings
```

Naming matters because Vanity filters by gender/model:

- `hairs`, `eyes`, `eyebrows`, `pants`, `shoes`, `hats`, `markings`
  - use `male-...`, `female-...`, or `any-...`
- `beards`
  - use `male-...` or `any-...`
- `shirts`, `jackets`, `accessories`
  - use `steve-male-...`, `alex-male-...`, `female-...`, or `any-...`

Examples:

```text
plugins/Vanity/overlays/hairs/male-curly.png
plugins/Vanity/overlays/eyebrows/any-clean_brows.png
plugins/Vanity/overlays/shirts/steve-male-basic_tee.png
plugins/Vanity/overlays/jackets/female-cropped_jacket.png
```

After changing overlays, run `/vanity reload` so Vanity rescans and regenerates
`web/assets/manifest.json`.

Alternatively, use `admin.html` to install individual overlays. Panel uploads
are scanned and pushed to open editors automatically, so no manual reload is
needed.

## Website Overlay Library

Authenticated players can open **Overlay Library** in the editor sidebar and
upload a ZIP from their computer. Vanity searches the whole archive, so supported
PNGs can be inside any number of wrapper folders. It recognizes category/model
folders and can also infer both from flat filenames.

```text
anything/.../<category>/.../<variant>/.../<file>.png
anything/.../<category>_<variant>_<file>.png
```

Examples:

```text
overlays/shirts/alex-male/linen_tunic.png
exports/Shirt/Alex_Male/linen_tunic.png
download/pants_unisex_travel_belt.png
assets/skin_colours/Alex Female/warm.png
```

Folder spelling is normalized automatically. Spaces, underscores, hyphens,
singular/plural names, and mixed casing are accepted. Common aliases include
`top` -> `shirts`, `trousers` -> `pants`, `slim` -> `alex-male`, `classic` ->
`steve-male`, `unisex` -> `any`, and `skin_colours` -> `skin-colours`. Uploaded
skin-colour assets are installed as base skins in `plugins/Vanity/skins/`.

Every PNG must be exactly 64x64. Supported variants are:

- Gender categories: `male`, `female`, `any`
- Model categories (`shirts`, `jackets`, `accessories`): `steve-male`,
  `alex-male`, `female`, `any`
- Beards: `male`, `any`

Upload policy and safety limits are configured in `config.yml`:

```yaml
overlay-library:
  uploads:
    enabled: true
    admin-only: false
    require-permission: false
    max-pack-size-mb: 5
    max-expanded-size-mb: 10
    max-file-size-kb: 512
    max-files-per-pack: 100
    max-packs-per-user: 20
```

When `require-permission` is enabled, players need
`vanity.overlay.upload`. Uploaded filenames are namespaced by uploader and pack,
the uploader receives ownership of every imported item, and pack metadata is
stored in `plugins/Vanity/overlay-packs.json`.

## Overlay Layer Priority

Open any Creator category and select **Layer order**. Equipped overlays are shown
from bottom to top. Moving a layer higher draws it later and places it in front.
The order is stored with the active outfit and with saved Closet outfits.

For a long tunic, move `pants` lower than `shirts` so the shirt is composited in
front of the pants. Existing outfits without a saved order keep the legacy
default automatically.

## Disabling Profiles

```yaml
profiles:
  enabled: false
```

With profiles disabled, `/vanity` opens the single-player outfit directly. The
character picker, New Character action, lore/profile controls, and character
token display are removed from the web flow. The server also blocks profile
create, delete, rename, and select API calls, including calls made from an older
open browser session.

## Shop And Ownership

`shop.yml` controls store pricing. `owned-items` in `config.yml` controls
whether creator access depends on ownership.

Example ownership setup:

```yaml
owned-items:
  enabled: true
  starter-categories:
    - eyes
    - eyebrows
    - hairs
    - beards
    - base
  store-categories:
    - shirts
    - pants
    - jackets
    - shoes
    - accessories
    - hats
```

Example shop defaults:

```yaml
pricing:
  defaults:
    hairs: 0
    eyebrows: 0
    beards: 0
    eyes: 0
    shirts: 200
    jackets: 350
```

Vanity can auto-generate `shop.yml` entries from discovered overlays without
overwriting existing manual edits.

## Economy

Vault is preferred. PlaceholderAPI + console commands are the fallback.

```yaml
economy:
  use-vault: true
  use-placeholder: true
  currency-name: Coins
  placeholder: "%vault_eco_balance%"
  withdraw-command: "eco take {player} {amount}"
  deposit-command: "eco give {player} {amount}"
```

## Tokens

There are four separate token pools:

- `character`: extra profile creation slots
- `cust`: general customisation changes like eye colour or height
- `skin`: skin-colour changes
- `hair`: hair/beard/eyebrow colour changes

Admin grant examples:

```text
/vanity token 1 PlayerName character
/vanity token 5 PlayerName cust
/vanity token 2 PlayerName skin
/vanity token 2 PlayerName hair
```

Config:

```yaml
customisation-tokens:
  enabled: true
  free-per-profile: 1

character-tokens:
  enabled: true
  free-slots: 1
```

## Colour Palettes

Restrict colours in `palettes.yml`. Vanity enforces these rules in both the web
UI and the server API.

Categories include:

- `skin`
- `hair`
- `eyes`
- `shirts`
- `pants`
- `jackets`
- `shoes`
- `accessories`
- `hats`

Example:

```yaml
categories:
  skin:
    allowed-hex:
      - "#f5d5b8"
      - "#d4a373"
    allowed-hue-range: [0, 50]
    allowed-saturation-range: [10, 70]
    allowed-lightness-range: [15, 90]
```

## Scales / Heights

Preferred setup is explicit values in `config.yml`:

```yaml
scale:
  steps: [0.85, 0.90, 0.95, 1.00, 1.05, 1.10, 1.15, 1.20]
```

The website slider snaps to these values, and the server snaps incoming changes
again before applying the player scale attribute in-game.

## Aging System

The system is scaffolded and disabled by default.

Enable it:

```yaml
aging:
  enabled: true
  tone-folder: skin-tones
  tick-interval-minutes: 60
  age-options: [child, teen, adult, elder]
  hair-grey-at-age: elder
```

Then place tone overlays in:

```text
plugins/Vanity/skin-tones/
```

File format:

```text
<tone>_age<NN>.png
```

Examples:

```text
fair_age15.png
fair_age25.png
fair_age40.png
```

## Profile Switch Behaviour

These settings control what changes when a player switches profile in the web
UI:

```yaml
profile-switch:
  inventory: true
  height: true
  permissions: false
  clear-potion-effects: false
  reset-hunger: false
  reset-health: false
```

If `permissions: true`, Vanity expects LuckPerms when applying profile group
changes.

## Lore

Players can write lore per profile in the website. In-game:

```text
/vanity <player> lore
/vanity <player> lore set <text...>
/vanity <player> lore delete
```

## Web Hooks

Vanity can run console commands from website events:

- `outfit-apply`
- `outfit-save`
- `profile-create`
- `profile-select`
- `profile-delete`
- `item-purchase`
- `lore-set`

Config:

```yaml
web-hooks:
  enabled: true
  events:
    outfit-apply: []
    outfit-save: []
    profile-create: []
    profile-select: []
    profile-delete: []
    item-purchase: []
    lore-set: []
```

## Editing The Website

Live website files extract to:

```text
plugins/Vanity/web/
```

Most useful files:

- `index.html`: shell markup
- `admin.html`, `admin.css`, `admin.js`: administrator control room
- `style.css`: shared layout and common component styling
- `themes/*.css`: per-theme visuals
- `js/icons.js`: icon packs
- `js/lib/themeAssets.js`: theme -> bg/cursor/icon/font binding
- `js/render/viewer3d.js`: player viewer and lighting
- `js/render/itemPreview.js`: store/closet card render framing
- `js/ui/*.js`: editor, store, closet, settings, and profile UI

There is no web build pipeline. Edit the extracted files directly, refresh the
page, and test.

## Saved Outfits / Closet

Players can:

- save outfits
- equip outfits
- rename outfits
- delete outfits
- edit a saved preset by loading it into the creator and saving back over it

The edit flow now works from Closet into Creator instead of editing inside the
modal.

## Developer Build

```powershell
C:\Users\caner\.codex\tools\apache-maven-3.9.9\bin\mvn.cmd clean package
node --test src\test\web\catalog.test.mjs
```

Output jar:

```text
target/Vanity.jar
```
