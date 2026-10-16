# Saddle Vendor Fix

**Automatically restores missing invisible vending machines for stable shopkeepers on Rust servers.**

Saddle Vendor Fix is a lightweight Oxide/uMod plugin designed to repair stable shopkeepers that have lost their invisible vending machine references.

Certain Rust updates or custom-map configurations can result in stable shopkeepers appearing without the vending machine entity required for their trading functionality.

This plugin identifies affected shopkeepers and creates the missing vending machine connection automatically when the server initializes.

## Features

- **Automatic Stable Vendor Detection** — Identifies stable shopkeepers missing valid vending machine references.
- **Missing Vending Machine Repair** — Creates and links an invisible vending machine when necessary.
- **Native Rust Prefabs** — Uses Rust's existing stable shopkeeper and NPC vending machine prefabs.
- **Automatic Shop Configuration** — Initializes the vending machine using its configured vending orders.
- **Map Marker Updates** — Updates the vending machine's map marker after creation.
- **Reference Restoration** — Associates the vending machine with the correct stable shopkeeper.
- **Temporary Entity Management** — Disables persistence for newly created vending machine entities.
- **Automatic Initialization** — Runs after the server finishes initializing.
- **No Commands or Permissions** — Requires no player or administrator interaction after installation.

## How It Works

When the server finishes initializing, Saddle Vendor Fix scans existing server entities for stable shopkeepers.

For each shopkeeper, the plugin performs the following checks and repairs.

### 1. Identify Stable Shopkeepers

The plugin searches for NPC shopkeepers using Rust's stable shopkeeper prefab.

Shopkeepers with valid invisible vending machine references are skipped.

### 2. Create the Missing Vending Machine

If a stable shopkeeper has no valid vending machine reference, the plugin creates Rust's native invisible NPC vending machine prefab.

The vending machine is positioned relative to the shopkeeper:

- 1.5 meters below the shopkeeper
- 1.5 meters forward from the shopkeeper
- Using the shopkeeper's rotation

### 3. Initialize the Vending Machine

The plugin then:

1. Spawns the new vending machine.
2. Disables entity saving.
3. Configures the required vending machine flags.
4. Enables broadcasting.
5. Updates the map marker.
6. Loads the designated vending orders.
7. Initializes the vending machine inventory and offers.

### 4. Restore the Shopkeeper Connection

Finally, the plugin attaches the vending machine to its associated NPC and updates the shopkeeper's vending machine reference.

The repair is logged in the server console.

## Installation

1. Download `SaddleVendorFix.cs`.
2. Upload it to your server's `oxide/plugins` directory.
3. Allow Oxide/uMod to compile and load the plugin.
4. Restart the server or reload the plugin after the relevant entities are initialized.
5. Check the console for repair messages.

No additional setup is required.

## Configuration

Saddle Vendor Fix does not use a configuration file.

The plugin uses predefined Rust prefab paths and vending machine settings.

## Commands and Permissions

**Commands:** None

**Permissions:** None

The plugin operates automatically during server initialization.

## Console Logging

When a broken stable vendor is detected, the plugin logs a message identifying the affected shopkeeper's position.

If the vending machine cannot be created, it generates a warning.

These messages can help server administrators identify stable vendor problems on custom maps.

## Compatibility and Dependencies

| Requirement | Details |
|---|---|
| **Game** | Rust (PC) |
| **Framework** | Oxide/uMod |
| **Additional Plugin Dependencies** | None |
| **Configuration File** | Not required |
| **External Database** | Not required |
| **Player Commands** | None |
| **Custom UI** | None |

The plugin relies on Rust's native stable shopkeeper and invisible vending machine systems.

Compatibility may depend on changes to the relevant prefabs and vending machine APIs in future Rust updates.

## Important Notes

- This plugin is intended as a temporary repair for missing stable vendor references.
- Shopkeepers with valid vending machine references are skipped.
- The plugin creates a new vending machine rather than searching for an existing unlinked one nearby.
- If an unlinked vending machine already exists, a duplicate may be created.
- It uses a predefined vending-order manifest index.
- The repair runs when the server finishes initializing.
- Permanent prefab corrections should be made in the original map whenever possible.

**Developer recommendation:** Fixing incorrectly configured prefabs in the map editor is preferable to relying indefinitely on a runtime workaround.

## Credits

**Original developers:** RustMaps & Jexs

**Version:** 1.0.1

**Additional acknowledgment:** The source code credits lencorp for assistance restoring vending machine functionality following a Rust update.

---

**Saddle Vendor Fix** provides a simple, automatic workaround for stable shopkeepers that have lost their vending machine connections, helping restore normal trading functionality on affected Rust maps.
