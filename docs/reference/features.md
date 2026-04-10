# All Features

A complete reference of everything included in Skinned Mesh Separator.

---

## Editor Window

Accessible via **Tools → Skinned Mesh Separator**. Dockable anywhere in the Unity editor layout.

---

## Bone Assignment

| Field | Purpose |
|---|---|
| Skinned Mesh Renderer | The source character mesh to extract from |
| Head Bone | Root bone for the head region |
| Left Shoulder Bone | Root bone for the left arm |
| Right Shoulder Bone | Root bone for the right arm |
| Other Bone | Any additional custom bone region |
| Include Child Bones | Whether to include all child bones in extraction |

---

## Auto-Find Bones

Scans the rig's full bone array and matches common naming patterns for head and shoulder bones. Supports:

- Whitespace, underscore, and hyphen separators
- Case-insensitive matching
- Common conventions: `Bip01`, `mixamo`, standard humanoid, and more

Console output confirms which bones were found and which were not.

---

## One-Click Read/Write Toggle

Enables `isReadable` on the source mesh's `ModelImporter` and triggers an asset reimport — all from within the tool window. No need to navigate to the FBX import settings manually.

---

## Preset Extraction Buttons

Six preset buttons covering the most common workflows:

- Keep ONLY Head
- Remove Head (Keep Body & Arms)
- Keep ONLY Arms
- Remove Arms (Keep Body & Head)
- Keep ONLY Other Part
- Remove Other Part

---

## Mesh Processing

- Reads `BoneWeight` data per vertex to identify influenced vertices
- Filters triangles per submesh — preserves submesh structure
- Outputs a new `Mesh` asset via `AssetDatabase.CreateAsset`
- Logs removed triangle count to the Console

---

## Supported Mesh Types

- Any `SkinnedMeshRenderer` with Read/Write enabled
- Humanoid, Generic, and Custom rigs
- Meshes imported from FBX, OBJ, Blender, Maya, 3ds Max, and any standard format
- Any vertex count
- Multi-submesh meshes

---

## Package Contents

- `SkinnedMeshSeparator.cs` — full C# source, commented
- Documentation / usage guide
- All source code is included and editable
