# Common Workflows

Practical step-by-step guides for the most common use cases.

---

## First-Person Body Setup

Generate a headless body mesh for a first-person game where the camera would clip through the character's head.

1. Open **Tools → Skinned Mesh Separator**
2. Assign the full-body `SkinnedMeshRenderer`
3. Click **🔍 Auto-Find Bones** (or assign the Head bone manually)
4. Ensure **Include Child Bones** is enabled (to capture jaw, eyes, etc.)
5. Click **Remove Head (Keep Body & Arms)**
6. Save the mesh as `Character_BodyNoHead`
7. Assign `Character_BodyNoHead` to the `SkinnedMeshRenderer` used in your first-person camera setup

The body will animate correctly on the original skeleton without rendering a head in the player's view.

---

## Modular Character System

Create separate mesh assets per body region for a character customisation system where players can swap body parts or hide regions under clothing.

1. Run the tool multiple times on the same source `SkinnedMeshRenderer`:
    - **Keep ONLY Head** → `Character_Head`
    - **Remove Head** → `Character_Body`
    - **Keep ONLY Arms** → `Character_Arms`
2. Assign each mesh to its own `SkinnedMeshRenderer`, all sharing the same skeleton/rig
3. Toggle `SkinnedMeshRenderer.enabled` at runtime to show/hide each region

!!! tip
    This approach avoids duplicate animated characters — all `SkinnedMeshRenderers` can share the same `Animator` and bone hierarchy.

---

## Extracting a Custom Body Region

Use the **Other Bone** field to extract any part of the mesh — a leg, a tail, a backpack, or any accessory.

1. In the **Other Bone** field, drag the root bone of the region you want (e.g. the `Thigh_L` bone for the left leg)
2. Enable **Include Child Bones** to capture the full leg (shin, foot, toes)
3. Click **Keep ONLY Other Part** or **Remove Other Part** depending on what you need
4. Save the result

---

## LOD Mesh Generation

Reduce draw call complexity by creating a simplified lower-body or upper-body mesh for distant LOD levels.

1. Extract the lower body using the **Other Bone** field (assign `Hips` or `Spine` as the root)
2. After saving, import the mesh back and apply a Unity **Mesh Simplifier** or similar to reduce poly count
3. Assign the simplified mesh as a lower LOD level in a `LODGroup` component

---

## Gameplay Dismemberment Setup

Pre-separate body parts for a damage system where arms, legs, or the head can detach.

1. Extract each body region as a separate mesh asset (Head, Arms, LeftLeg, RightLeg, Torso)
2. At runtime, disable the original `SkinnedMeshRenderer` on hit
3. Spawn the appropriate pre-extracted mesh as a `MeshRenderer` (no longer needing to be skinned) with physics applied

!!! note "Editor-only tool"
    Skinned Mesh Separator runs in the Unity Editor only. The mesh splitting happens at author time — the extracted `.asset` files are what you use at runtime. See [Limitations](../reference/limitations.md) for details.
