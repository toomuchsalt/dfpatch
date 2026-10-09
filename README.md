# Daggerfall 30 year anniversary edition

### Some bug fixes and QoL features. Almost like Daggerfall didn't turn 30 this year.

## Installation

Drop `DFPATCH.EXE`, `PLAY.BAT` and `_dfpatch` into Daggerfall installation directory.
Edit `_dfpatch/DFPATCH.CFG` to enable/disable patches you want. Supports both `;` and `#` to comment out entries.
By default `DFPATCH.CFG` comes with all patches enabled. Everything but `QUICK` and `SPELLKEY` are completely independent and can be disabled.

All patching is applied in-memory, no game files are changed. Removing patcher (or simply running `DAGGER.EXE` instead) works as usual.

All patches for now are compatible with original saves both ways (so loading a save from modded game in original is fine too).

DFPatch replaces dos extender on FALL.EXE with dos32a (patcher is based on it). If you don't know what that means - don't worry.

"This product uses DOS/32 Advanced DOS Extender technology."

### HIRES.DPM

The one that started all this. I was a little sick with Daggerfall using 320x200 resolution while VBE extension modes are just sitting there doing nothing.

Renders the game world and dungeon automap at 640×400. Menus, movies and the HUD are scaled x2 in all their pixel gorgeous.

Has horrendous performance hit (what else did you expect, it's pushing 4 times number of pixels). In DosBox I need 140k-160k cycles to keep reasonable fps (up from 48000 at 320x200).

### WATER.DPM

Patches water using surface ripple effect for far cutoff. Now water fades to its opaque color nicely.

### FOG.DPM

Starts distance fog at roughly half its original starting distance, keeping the same maximum draw distance. Fades toward the current sky/weather background, making buildings and terrain blend into it before they are cut off.

Fixes rounding that prevented fog from reaching its maximum at some draw distances. 

Has a noticable performance cost due to fog ramp recalculation on every palette change. May cause stutter during morning/evening rapid sun color changes.

### SKY.DPM

Uses perspective mapping for skybox, making it less trippy. 

Somewhat slower than original, cause it can't copy whole rows of pixels at a time.

### BOUNDS.DPM

Fixes bright coloured dots or strips beneath trees and other world sprites caused by reading outside their texture dimensions. 
Invalid pixels are skipped instead of drawing unrelated texture data. Applies to all sprites, not just trees (though I haven't seen this issue with anything but trees).

### CLIP.DPM

Fixes trees and other sprites being incorrectly covered by nearby sloping geometry, such as a roof cutting across a tree even where the tree should be in front. 
Has negligible performance cost.

### MOVE.DPM

Allows forward or backward movement together with strafing left or right. Previously, one direction overrode the other. Tries to avoid gaining extra speed when moving diagonally. 

### AIRLOOK.DPM

Allows mouse look while jumping or falling, where original engine locks the camera. 
Your jump/fall direction is tied to your camera so if you do a 720 with a camera so will your char. See next patch for a fix.

### JUMP.DPM

Keeps your horizontal movement in the same world direction during a jump or fall, even if you turn the camera. 

### CLIMB.DPM

Make climbing skill actually useful. Now theres no delay before first climbing check kicks in, and every slip check has a 50%(up from 5%) chance to require a skill check. So at 10% skill you have 45% chance to slip every 3 seconds.

### WALL.DPM

Ninja mode - you can climb up/sideways/down stay on the wall until you fail your climbing check. Look away from the wall and jump (gotta have a good climbing skill to do that, with 0% skill chance to fail is 75%)

### CLICK.DPM

Fixes a short right click hiding several layered dungeon blocks in rapid succession. Adds a 200 ms delay between hiding blocks, so a brief click hides only the topmost one. Holding the button still hides further blocks at the slower rate.
No longer your mouse drills a hole through the map every click.

### SLIDERS.DPM

Expands the sound, music and detail sliders to 0–255, with matching bar positions. Detail can reach its full value directly in the game instead of requiring a save-file edit.

### QUICK.DPM

Press F9 during gameplay to save to slot 0 (the top-left slot), with the name “Quicksave”. Uses the game's existing save system so all your precious bugs are intact.

Overwrites slot 0 without confirmation. Requires HOTKEYS.

### SPELLORD.DPM

Fixes spellbook order getting garbled after each save/load. Now spell ordering is persistent.

### SPELLFOC.DPM

Fixes Move Up and Move Down resetting selection to the first spell when sorting spellbook. Selected spell stays, as does the scroll position.

### SPELLKEY.DPM

Press top-row 1–9 to select the first through ninth spells in your current spellbook order. Shows a message “<Spell name> selected”. Use the normal Recast key to cast the selected spell.

Requires HOTKEYS.

Existing game bindings still run, so conflicting number-key actions should be unbound. The cheat remap below removes the built-in cheat conflict on 1.

### CHEATKEY.DPM

Moves the MaxSpeed cheat originally activated by top-row 1 to Ctrl+F2, freeing 1 for spell selection when cheat mode is enabled

### HOTKEYS.DPM

Provides the common keyboard handling used by quicksave and number-key spell selection. Adds no player action by itself. Load it before QUICK and SPELLKEY.
