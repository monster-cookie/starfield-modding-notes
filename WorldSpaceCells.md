# World space Cells

**THIS IS PRE SFCK Research** PLEASE take this with a grain of salt while I update it with the SFCK information.

## Terrain Files

Terrain data is stored in 3 specific paths:

- Data\\lodsettings
- Data\\meshes\\terrain\[WorldSpaceEditorID\]\\objects
- Data\\terrain

The game engine uses the Editor ID of the World space and those 3 specific paths to load the terrain files so the terrain can be mapped.

[!NOTE]

- PCM might have a fallback system were it uses the remaining data so a Pack-In as the Ghost Cave worked just fine before I found this. Though trying to FT to the cell for layout failed horribly.
