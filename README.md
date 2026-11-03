# BonkAuras

WeakAuras-style buff tracking for [Hordes of Azeroth](https://github.com/jonhaldors/hordes-of-azeroth) (1.12.1 / benilla client).

BonkAuras puts native 1.12.1 buffs and Hordes of Azeroth state buffs on compact, movable icons. It is a standalone addon: no libraries, no launcher changes, no server changes.

[中文说明](README_zh.md)

## Two kinds of buffs

Hordes of Azeroth uses two separate buff systems, and BonkAuras tracks both:

- **Native 1.12.1 buffs**: auras managed by the original client, such as Power Word: Fortitude, Enrage, or Blade Flurry. BonkAuras reads them with the 1.12.1 buff API. Add them by clicking a row in the current-buff list or by entering their spell ID.
- **Hordes of Azeroth state buffs**: talent and system states managed by Hordes of Azeroth, such as Shield, Dash, Determination, Necrotic, and Wounded. These are not ordinary client auras. BonkAuras reads them from the `BONK~` messages that the `HordesOfAzeroth` addon receives from the server, so that addon must be installed and enabled.

## Features

- Tracks native 1.12.1 player buffs and Hordes of Azeroth state buffs: Shield, Dash, Determination, Necrotic, and Wounded.
- Hordes of Azeroth state names and descriptions follow the language chosen in Hordes of Azeroth itself.
- Stacks are shown in the center of the icon, values above it, and remaining time below it.
- Inactive trackers stay in place: greyed out by default, or fully hidden if preferred.
- Manual tracking by spell ID for game buffs such as Enrage or Blade Flurry.
- Profiles: create multiple pages and make each one account-wide or character-specific.
- Import and export the whole active profile as a short encoded string.
- UI language dropdown: follow Hordes of Azeroth, Simplified Chinese, or English.
- `/wa` opens the configuration window; drag icons to move them, right-click to remove them.

## Requirements

- [Hordes of Azeroth](https://github.com/jonhaldors/hordes-of-azeroth) with the benilla client.
- The `HordesOfAzeroth` addon for the Hordes of Azeroth state buffs. Native 1.12.1 buff tracking works without it.

## Installation

1. Download `BonkAuras-<version>.zip` from the repository's Releases page.
2. Extract the `BonkAuras` folder into the game's addon directory:

   ```
   <Hordes of Azeroth>/benilla-config/AddOns/BonkAuras
   ```

   The folder should contain `BonkAuras.toc`, `BonkAuras.lua`, and `BonkAurasSpells.lua` directly.

3. Restart the game. If BonkAuras was already installed, `/reload` is enough.
4. Type `/wa` to open the configuration window.

## Usage

### Main window

- **Current buffs**: click a row to start tracking that buff.
- **Tracked**: lists every tracked entry. Right-click a row to stop tracking it.
- **Add buff by ID**: enter a spell ID and press Add. Examples: `13046` (Enrage), `13877` (Blade Flurry), `1243` (Power Word: Fortitude).
- **Show buff IDs**: shows spell IDs in the current-buff list and appends them to buff tooltips.
- **Tracker tooltips**: turn the tooltip on or off for tracked icons.
- **Inactive**: choose greyed-out or fully transparent for buffs that are not active.
- **Language**: follow Hordes of Azeroth, or force Simplified Chinese / English.
- **Unlock**: after unlocking, drag icons to move them. Right-click a tracked icon to stop tracking it.
- **Clear all**: removes every tracked entry on the current profile page.

### Profiles

Open **Profiles** from the first row of the main window.

- Click a profile to switch to it.
- **New** creates an empty profile using the current page's settings.
- **Save** stores the current name and all settings, including icon positions.
- **Rename** changes the active profile's name.
- **Delete** removes the active profile; at least one usable profile is always kept.
- **Toggle scope** switches the active profile between **Account** and **Character**:
  - Account profiles are shared by every character.
  - Character profiles are visible only to the character that created them.
- Switching profiles also saves the current one automatically.

### Import and export

- **Export** opens a window with the active profile encoded as a short string starting with `BKA1`. The text is selected automatically; press `Ctrl+C` to copy it.
- **Import** accepts such a string and replaces the current profile's settings and trackers.
- Whitespace and line breaks are ignored when importing.

### Default profile

On a fresh installation BonkAuras creates an account-wide profile named `Default` (`默认` when Hordes of Azeroth is in Chinese) with five Hordes of Azeroth state buffs: Shield, Dash, Necrotic, Wounded, and Determination.

The UI language follows Hordes of Azeroth by default, and tracker tooltips are disabled. Both can be changed from the main window.

## Notes

- The 1.12.1 client does not expose the spell ID of an active buff to addons. BonkAuras therefore identifies tracked buffs by their icon. The ID shown for a game buff comes from a bundled 1.12.1 spell index and is a representative ID when several spells share an icon; adding that ID still tracks the correct icon.
- Hordes of Azeroth state buffs depend on the `BONK~` messages sent by the Hordes of Azeroth server, so the `HordesOfAzeroth` addon must be installed and enabled.
- The addon tracks the player's own buffs only.

## Development

- `BonkAurasSpells.lua` is generated from the 1.12.1 client's `Spell.dbc` and `SpellIcon.dbc`. Do not edit it by hand.
- Pull requests to `main` run a basic Lua syntax check and a TOC file check.
- Pushing a tag such as `v0.1.0` builds and publishes a release zip containing the complete `BonkAuras` addon folder.

## License

MIT. See [LICENSE](LICENSE).
