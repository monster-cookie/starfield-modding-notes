# Blender to Starfield Static Asset Pipeline

This guide covers the practical workflow for taking a custom static asset from Blender to a Starfield `Data` folder:

```text
Blender
  -> NIF and external geometry
  -> MAT materials
  -> DDS textures
  -> NifSkope validation
  -> SFCK integration
  -> in-game validation
```

The workflow was validated in game with the Venworks Boost Services terminal on July 29, 2026. It is intended for static props, furniture, and terminal-like assets. Skeletal meshes, animation, morphs, dynamic rigid bodies, and complex Havok setups require additional work.

## Validated Toolchain

- Blender 5.2
- [Starfield Blender Extension](https://github.com/MrTrilB/StarfieldBlenderExtension) 1.6.0
- [FO76utils NifSkope](https://github.com/fo76utils/nifskope)
- [Starfield Material Exporter](https://www.nexusmods.com/starfield/mods/7830) (SFME)
- Starfield Creation Kit and Material Editor
- Substance 3D Painter, NVIDIA Texture Tools Exporter, DirectXTex/Texconv, or another DDS exporter that supports the required formats
- Extracted Starfield assets for reference and material resolution

The Starfield Blender Extension changes quickly. Its current documentation targets Blender 5.0 or newer and includes NIF, external mesh, material, and collision workflows. Verify the requirements for the version you install.

PyNifly's Starfield support was not reliable enough for the validated terminal export. It wrote an incomplete or incorrect set of external geometry references even though it reported success. The final working asset was exported with the Starfield-specific extension.

## Creation Kit Material Configuration

Loose materials must be enabled for the Material Editor to show and edit their layers. Confirm this setting exists in `CreationKit.ini` or `CreationKitCustom.ini`:

```ini
[Materials]
bUseCompiledDB=0
```

Without this setting, a loose `.mat` may open but appear to have no editable layers.

## Final Data Layout

Build and validate the asset in an isolated `Data` directory before copying it into a live mod:

```text
Starfield Export\
└── Data\
    ├── Meshes\
    │   └── YourName\
    │       └── YourMod\
    │           └── Asset.nif
    ├── geometries\
    │   └── <hashed-directory>\
    │       └── <hashed-name>.mesh
    ├── Materials\
    │   └── YourName\
    │       └── YourMod\
    │           └── Asset.mat
    └── Textures\
        └── YourName\
            └── YourMod\
                └── Asset_color.dds
```

The NIF contains references to the generated files under `Data\geometries`. Treat the NIF and the complete generated geometry set as one versioned unit. When an export changes the hashed geometry paths, replace the NIF and the entire related `geometries` output together.

Do not use an extracted game-asset cache as an export destination. Keep extracted meshes, materials, and textures read-only.

## 1. Prepare the Blender Scene

### Configure the Extension

In the Starfield Blender Extension preferences:

1. Set the Starfield `Data` or asset path to the actual installation or extracted asset root.
2. Set the export folder to an isolated working directory.
3. Run the extension's recommended scale/units action.
4. Confirm the extension can resolve the loose assets it needs.

Do not assume a copied path is correct. A valid-looking path to the wrong Steam library can cause confusing export failures.

### Organize the Export Hierarchy

Use one Empty as the export root and parent every exported mesh beneath it:

```text
Asset_ExportRoot
├── Asset_Body
├── Asset_Screen
├── Asset_Logo_Front
├── Asset_Logo_Left
└── Asset_Logo_Right
```

The validated exporter used only the first material assigned to each mesh. Split geometry by material so every exported mesh has one intended Starfield material.

For example:

| Mesh | Material purpose |
| --- | --- |
| Body | Opaque PBR body |
| Screen | Static or emissive screen |
| Front logo | Alpha-tested logo |
| Left logo | Alpha-tested logo |
| Right logo | Alpha-tested logo |

Keep keyboard, screen, body, and decorative label materials separate when they have different rendering behavior. Do not merge a working keyboard or interaction surface into an unrelated decal mesh merely to reduce the mesh count.

### Apply Transforms

Before export:

1. Confirm the asset's dimensions against a known Starfield reference.
2. Apply object scale and rotation where appropriate.
3. Confirm each exported mesh reports an object scale of `1, 1, 1`.
4. Keep the pivot and export root at a sensible placement origin.

Do not immediately scale geometry when only the artwork looks too small. Blender material-node Mapping transforms are not exported into Starfield `.mat` files. A logo may be the correct physical size while occupying only a small corner of its DDS atlas.

### Set the Material Paths

Set each exported mesh's Starfield material path to the loose `.mat` it should use:

```text
Materials\YourName\YourMod\Asset_Body.mat
Materials\YourName\YourMod\Asset_Screen.mat
Materials\YourName\YourMod\Asset_Logo.mat
```

Use game-relative paths. Do not use an absolute Windows path inside the NIF.

### Prepare UVs for the Game

Starfield receives the mesh UVs and DDS image, not Blender's entire shader graph.

- Bake or apply any Mapping-node crop, scale, or offset into the UVs or final DDS.
- Use the complete DDS canvas when the material expects full-range UVs.
- Leave padding or bleed around visible texture regions.
- Inspect bevels, edge polygons, and backfaces. A thin side polygon can stretch one edge of a colorful screen texture into a large bright band.
- Avoid collapsing unrelated UV loops to one point as a quick fix. Export-time triangulation or vertex deduplication may reuse that UV on a visible triangle.

For the Boost Services screen, preserving the original display UVs and correcting the DDS border was safer than collapsing the screen-bevel UVs.

### Check Orientation

Verify front, back, up, and activation-facing direction in NifSkope and SFCK.

The validated terminal required an export-only rotation of 180 degrees around the vertical Z axis. This was asset-specific; do not apply it blindly to every model. Record any export-only rotation in the source scene or build script so later exports remain consistent.

## 2. Export the NIF and External Geometry

Use these settings as the starting point for a static prop:

| Setting | Value |
| --- | --- |
| Export type | Static |
| Active export object | Empty root |
| External geometry | Enabled |
| External geometry names | Hashed/generated |
| Export Material | Disabled when using prepared external `.mat` files |
| NIF Template | As Is |

Export the NIF beneath the isolated `Data\Meshes` folder:

```text
Starfield Export\Data\Meshes\YourName\YourMod\Asset.nif
```

The extension should write the external files beneath:

```text
Starfield Export\Data\geometries\
```

### Clean Export Rule

The exporter may generate new hashed geometry paths on every export and leave old files behind. Before regenerating:

1. Resolve the absolute isolated export path.
2. Confirm the target is the intended `Starfield Export\Data\geometries` directory.
3. Remove only that isolated generated geometry directory.
4. Export a fresh NIF and geometry set.

Never recursively clean the live Starfield `Data` directory, a repository root, or the extracted asset cache.

### Expected Result

For one Empty with five child meshes, expect:

- One NIF
- Five `BSGeometry` blocks
- Five current external `.mesh` files
- One material path per geometry block

Do not trust the exporter's success message by itself. Validate the actual NIF and every referenced external geometry file.

## 3. Create the DDS Textures

Use sRGB formats for color data and raw/linear formats for scalar data.

| Texture | Suffix | Layout | Substance Export Option | 3DS Export Option | Blender Image Color Space | Source Format | DX Format |
| --- | --- | ---: | --- | --- | --- | --- | --- |
| Albedo/Color | `_color` | 1–3 channels | `SRGB8` | `SRGB` | `sRGB` | `R8G8B8A8_UNORM_SRGB` | 1-bit alpha - `BC1_UNORM_SRGB` |
| Height | `_height` | 1 channel | `L16` | `Raw` | `Non-Color` | `R16_UNORM` | `BC4_UNORM` |
| Roughness | `_rough` | 1 channel | `L16` | `Raw` | `Non-Color` | `R16_UNORM` | `BC4_UNORM` |
| Metalness | `_metal` | 1 channel | `L16` | `Raw` | `Non-Color` | `R16_UNORM` | `BC4_UNORM` |
| Normal | `_normal` | 3 channels | `RGB16F` | `Raw` | `Non-Color` | `R16G16B16A16_FLOAT` | `BC5_SNORM` |
| Ambient Occlusion | `_ao` | 1 channel | `L16` | `Raw` | `Non-Color` | `R16_UNORM` | `BC4_UNORM` |
| Emissive | `_emissive` | 3 channels | `SRGB8` | `SRGB` | `sRGB` | `R8G8B8A8_UNORM_SRGB` | `BC1_UNORM_SRGB` |
| Opacity | `_opacity` | 1 channel | `L16` | `Raw` | `Non-Color` | `R16_UNORM` | `BC4_UNORM` |

Blender's image color-space setting controls how a texture is interpreted while authoring and baking. It does not select the final DDS compression. Export an intermediate PNG, TIFF, or EXR from Blender, then create the DDS with NVIDIA Texture Tools, DirectXTex/Texconv, or another converter using the Source Format and DX Format columns.

When baking or saving an intermediate texture from Blender:

- Save color and emissive maps as sRGB, normally using an 8-bit PNG or TIFF.
- Treat height, roughness, metalness, normal, ambient-occlusion, and opacity maps as `Non-Color` data.
- Use 16-bit output for scalar maps when retaining additional precision matters.
- Keep normal-map output raw and unmodified by the scene's view transform.
- Do not use **Save as Render** for data maps because it can apply the scene's color-management transform.

### DDS Checklist

- Match the intended texture dimensions.
- Generate a complete mip chain.
- Confirm color and emissive maps are marked sRGB.
- Confirm scalar maps are exported as raw/linear data.
- Inspect every mip level when diagnosing distant black or missing textures.
- Keep color and opacity UV layouts identical when they are separate files.

The validated terminal logo used:

```text
1024 x 1024
11 mip levels
BC1 sRGB color
BC4 opacity
```

## 4. Create the MAT Materials

Starfield `.mat` files are JSON. Start from a Bethesda material that already has the rendering behavior you need, then change the material name and texture paths.

### Pick the Correct Shader Type

Use the material's actual job, not its filename, to choose a template.

| Surface | Recommended material behavior |
| --- | --- |
| Opaque body | Standard layered PBR material |
| Screen | Static, emissive, or effect material as required |
| Standalone logo/card plane | Standard material with alpha testing |
| Deferred decal applied to a receiver surface | Standard decal material |

Do not assume `1LayerStandardDecal.mat` is appropriate for every mesh called a decal. It is a deferred decal shader. On the terminal's standalone logo planes, the opacity silhouette rendered but the color appeared black in game even though SFCK and NifSkope looked correct.

The proven fix was to use the structure from:

```text
Materials\Architecture\City\NewAtlantis\NATerminalSignage01c.mat
```

That material uses:

```text
Data\MATERIALS\Layered\ShaderModels\1LayerStandard.mat
```

with:

- `BSMaterial::AlphaSettingsComponent`
- `HasOpacity = true`
- an alpha-test threshold
- a color texture at index `0`
- an opacity texture at index `2`

This rendered the standalone Venworks logo planes correctly in game.

### Preserve the Internal Resource Graph

The `res:` values inside a material are related IDs. Do not replace individual IDs with random values.

When a copied material produces an ID-collision warning in SFCK:

1. Open the copied material in the Material Editor.
2. Click **Fix IDs**.
3. Save the material.
4. Close and reopen it.
5. Confirm the collision warning is gone.

**Fix IDs** regenerates the internal layer, material, texture-set, and UV-stream IDs while preserving their relationships.

Prefer duplicating and saving a material through SFCK when possible. If editing JSON manually:

- Use a known-good template.
- Change as little as possible.
- Keep every `ID`, `Parent`, `To`, and component reference internally consistent.
- Validate the JSON before opening the game.

### Static Screens

Some screen materials include UV controllers. A stationary screen mesh can appear to rotate or scroll if the material animates its UV coordinates.

If a screen moves in game:

1. Confirm the geometry itself is stationary.
2. Inspect the screen material's controller mappings and curves.
3. Disable or flatten the specific UV animation rather than rotating or rebuilding the mesh.
4. Fully restart Starfield before retesting because materials can remain cached.

## 5. Assign Material Paths and Material IDs in the NIF

Starfield stores both a material path and a large integer material ID for each material-bearing geometry.

Newer Starfield-capable NifSkope builds may calculate the material ID automatically, but always verify it. [Starfield Material Exporter](https://www.nexusmods.com/starfield/mods/7830) provides an authoritative material-path ID for a loose `.mat`.

### Get the Material ID with SFME

1. Open `SFME.exe`.
2. Drag the custom `.mat` file into SFME's material-ID input.
3. Record the relative material path shown by SFME.
4. Record the large integer shown beside it.

Example values from the Boost Services terminal:

```text
materials\Venworks\Core\Terminals\BoostServices\VWKS_BSTerminal_Body.mat
1609384639

materials\Venworks\Core\Terminals\BoostServices\VWKS_BSTerminal_Logo.mat
592658433

materials\Venworks\Core\Terminals\BoostServices\VWKS_BSTerminal_Screen.mat
374121946
```

These IDs are path-specific examples. Generate new values for your own paths.

### Update the NIF in NifSkope

For every material-bearing `BSGeometry`:

1. Expand the geometry until you find its `BSLightingShaderProperty`.
2. Note the string-table ID shown in the shader property's **Name** field, such as `[##]`.
3. Open NifSkope's **Header** tab.
4. Expand the header's string entries.
5. Find the string entry with the same ID.
6. Replace it with the game-relative path reported by SFME:

   ```text
   materials\YourName\YourMod\Asset.mat
   ```

7. Click the green refresh/recycle icon on the string record to update the string-table offsets.
8. Return to the geometry block.
9. Select the associated `NiIntegerExtraData`.
10. Set **Integer Data** to the large SFME value.
11. Repeat this for every geometry using that material.

If three logo meshes share one material, all three geometry blocks need the same verified path and integer.

Save the NIF, close it, reopen it, and confirm:

- Every material path survived serialization.
- Every `NiIntegerExtraData` value is correct.
- Every external `.mesh` resolves.
- NifSkope reports no broken material or geometry references.

## 6. Add Collision and Interaction Support

A model can look correct in Starfield but remain impossible to activate when its NIF has no collision. The player's activation ray needs a collision shape to hit.

For a static interactive asset, verify:

- The NIF root has a collision object.
- A valid `bhkNPCollisionObject` and `bhkPhysicsSystem` are present when using the vanilla-style collision route.
- The root `BSXFlags` has the Havok bit enabled.
- The SFCK base record still supplies the correct furniture, activator, terminal, and script behavior.

### Validated Mission-Board Fallback

The custom terminal initially had:

```text
Collision Object = None
BSXFlags = 65536
```

The working fallback copied the complete collision branch from the vanilla mission-board terminal:

```text
bhkNPCollisionObject
└── bhkPhysicsSystem
```

The existing export flag was preserved and the Havok bit was added:

```text
65536 OR 2 = 65538
```

This supplies a collision target for the activation ray, but it still needs an in-game interaction test.

Copying collision from a similar vanilla asset is useful for diagnosis, but its shape may be too large, too small, or offset for a custom model. The preferred production result is a collision shape authored for the new geometry using a supported Starfield collision workflow.

A NIF does not independently turn a static mesh into a working terminal. The SFCK record must still provide the terminal interaction and scripts.

## 7. Validate in NifSkope

Open the exported NIF with the export `Data` directory available as a resource root.

Check:

- The expected number of `BSGeometry` blocks exists.
- Every external `.mesh` loads.
- Each geometry uses the intended `.mat`.
- Texture paths resolve.
- Front, up, and orientation are correct.
- Bounds look reasonable.
- Collision appears when **Show Collision** is enabled.
- No geometry is unexpectedly missing or duplicated.

A gray model can mean NifSkope does not have the temporary `Data` folder in its resource paths. That is different from a missing external `.mesh`.

NifSkope and SFCK previews are necessary but not authoritative. Materials, deferred decals, caching, collision raycasts, and interaction behavior can differ in the running game.

## 8. Install and Test as Loose Files

Copy the complete validated `Data` tree into the mod's staging directory:

```text
Meshes\
geometries\
Materials\
Textures\
```

Then:

1. Assign the NIF to the intended SFCK base object.
2. Keep or add the appropriate furniture/terminal behavior.
3. Place a fresh test reference.
4. Fully close and restart Starfield.
5. Test appearance, activation, collision, and interaction.
6. Test under multiple lighting conditions and viewing distances.

When testing a new export, replace the NIF and its entire generated geometry set together. Do not combine a new NIF with geometry from an older export.

## 9. Package the Asset

Typical archive placement:

| Asset | Archive |
| --- | --- |
| `.nif` | Main/general BA2 |
| External `.mesh` files under `geometries` | Main/general BA2 |
| `.mat` | Main/general BA2 |
| `.dds` | Textures BA2 |

Preserve the exact game-relative roots:

```text
meshes\
geometries\
materials\
textures\
```

Regenerate the archives whenever the packaged NIF, geometry, material, or texture inputs change.

## Troubleshooting

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| Export writes only one usable mesh | Multiple materials share one Blender mesh, the wrong export root is active, or external geometry is disabled | Use one Empty root, one mesh per material, and enable external geometry |
| NIF points to missing external geometry | Export was not built relative to a `Data` root, or the NIF and geometry folders came from different runs | Re-export into an isolated `Data` tree and replace the NIF and geometry set together |
| Old geometry remains after export | Hashed files from earlier runs remain in the isolated export folder | Safely clear only the isolated `Data\geometries` folder before export |
| Artwork is tiny but the plane is correctly sized | Blender Mapping-node crop/scale was not exported | Bake the mapping into the UVs or create a full-frame DDS |
| Bright strip appears beside a screen | A bevel or edge polygon samples and stretches the texture border | Add safe texture bleed or correct the edge UVs without collapsing visible UV loops |
| Screen appears to rotate or scroll | The `.mat` contains an animated UV controller | Disable or flatten the specific controller |
| Logo opacity works but color is black in game | A deferred decal shader is being used on a standalone plane | Use a regular alpha-tested `1LayerStandard.mat` template such as `NATerminalSignage01c.mat` |
| Material works in NifSkope/SFCK but not in game | Material path or `NiIntegerExtraData` ID is wrong, or the game cached an older material | Verify the path and ID with SFME, save/reopen the NIF, then fully restart Starfield |
| SFCK reports material ID collisions | A copied `.mat` retained the source material's internal `res:` IDs | Use **Fix IDs** and resave |
| Material opens with no layers in SFCK | Loose-material editing is disabled | Set `[Materials] bUseCompiledDB=0` |
| Model is visible but cannot be activated | The NIF has no usable collision or the SFCK record lacks terminal behavior | Add valid collision and verify the base record and scripts |
| Model faces the wrong direction | Coordinate-system or asset orientation mismatch | Apply a documented export-only rotation and regenerate all geometry |
| Model is gray in NifSkope | Temporary `Data` directory is not configured as a resource root | Add or browse to the export `Data` root |

## Final Checklist

### Blender

- [ ] Correct physical dimensions
- [ ] One Empty export root
- [ ] One mesh per material
- [ ] Child meshes parented to the root
- [ ] Object transforms applied
- [ ] UV mapping baked into the mesh or DDS
- [ ] Game-relative material paths assigned
- [ ] Orientation verified

### Export

- [ ] Static export
- [ ] External geometry enabled
- [ ] Prepared material export disabled
- [ ] Isolated `Data` root used
- [ ] Old isolated geometry safely removed
- [ ] Expected number of `.mesh` files written

### Materials and Textures

- [ ] `.mat` JSON validates
- [ ] Correct shader type selected
- [ ] Internal material IDs fixed through SFCK when required
- [ ] Color/emissive textures use sRGB
- [ ] Scalar textures use raw/linear formats
- [ ] Full mip chains generated
- [ ] Color and opacity UV layouts match

### NIF

- [ ] Every external geometry path resolves
- [ ] Every material path is correct
- [ ] Every SFME material ID is correct
- [ ] NIF was saved, closed, and reopened
- [ ] Bounds and orientation are correct
- [ ] Collision is present
- [ ] Required BSX flags are enabled

### Runtime

- [ ] Tested after a full game restart
- [ ] Appearance verified in multiple lighting conditions
- [ ] Mip behavior verified at distance
- [ ] Collision and activation verified
- [ ] Terminal/furniture behavior verified
- [ ] Final NIF and complete geometry set packaged together

## References

- [Starfield Blender Extension](https://github.com/MrTrilB/StarfieldBlenderExtension)
- [FO76utils NifSkope](https://github.com/fo76utils/nifskope)
- [Starfield Material Exporter](https://www.nexusmods.com/starfield/mods/7830)
- [Microsoft DirectXTex](https://github.com/microsoft/DirectXTex)
