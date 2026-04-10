# Quick Start

Get your first extracted mesh in under a minute.

---

## Step 1 — Open the Tool

Navigate to **Tools → Skinned Mesh Separator** in Unity's menu bar.

---

## Step 2 — Assign a SkinnedMeshRenderer

Drag a character's `SkinnedMeshRenderer` component from the Hierarchy or Inspector into the **Skinned Mesh Renderer** field.

---

## Step 3 — Find Bones

Click **🔍 Auto-Find Bones** to automatically detect the head and shoulder bones from your rig.

!!! tip
    Auto-Find works with most standard humanoid naming conventions (e.g. `Head`, `Shoulder_L`, `UpperArm_R`). If your rig uses non-standard names, assign the bones manually by dragging them from the Hierarchy.

---

## Step 4 — Enable Read/Write (if needed)

If the mesh is not yet readable, click **🔧 Enable Read/Write on Source Mesh**. This updates the model's import settings automatically — no need to dig through the Inspector.

!!! note
    The source mesh must have **Read/Write Enabled** before any extraction can proceed. The tool will log an error in the Console if this step is skipped.

---

## Step 5 — Extract

Click one of the preset extraction buttons:

| Button | Result |
|---|---|
| **Keep ONLY Head** | Extracts just the head region |
| **Remove Head** | Keeps the body and arms, removes the head |
| **Keep ONLY Arms** | Extracts both arms |
| **Remove Arms** | Keeps the body and head, removes arms |
| **Keep ONLY Other Part** | Extracts the bone set in the *Other Bone* field |
| **Remove Other Part** | Removes the bone in the *Other Bone* field, keeps the rest |

---

## Step 6 — Save

A save dialog will appear. Choose a location inside your `Assets` folder and give the mesh a name. The new `.asset` file will be created there.

Your original character mesh is unchanged.

---

## Next Steps

- [Tool Overview](../usage/tool-overview.md) — full breakdown of every field and button
- [Common Workflows](../usage/common-workflows.md) — real-world use case examples
