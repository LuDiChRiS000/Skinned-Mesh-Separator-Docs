# Extracting Meshes

This page covers how mesh extraction works under the hood and what to expect from the output.

---

## How Extraction Works

The tool reads the `BoneWeight` data on each vertex of your mesh. Every vertex in a `SkinnedMeshRenderer` stores up to four bone influences (indices and weights). When you select a bone and click extract:

1. The tool collects the bone index for your selected bone (and optionally its children)
2. It scans every vertex and marks those influenced by any of those indices
3. It then iterates over every triangle — if any vertex in a triangle is influenced by the selected bone, the whole triangle is kept or removed (depending on whether you're keeping or removing that region)
4. A new `Mesh` asset is created from the filtered triangle data and saved to disk

The source mesh is **never modified**. The new mesh is a copy with a subset of the original triangles.

---

## What the Output Looks Like

The extracted mesh:

- Retains all original vertex data (positions, UVs, normals, tangents, blend shapes, bone weights)
- Retains the same submesh structure as the source
- Is saved as a `.asset` file in your project

!!! note "Open edges"
    Because the tool simply removes triangles, the cut boundary will have open (non-watertight) edges. This is expected — see [Limitations](../reference/limitations.md) for details on when this matters and when it doesn't.

---

## Assigning the Extracted Mesh

After saving, assign the new mesh to a `SkinnedMeshRenderer` on your character:

1. Select a `SkinnedMeshRenderer` component in the Inspector
2. In the **Mesh** field, assign your new `.asset` file
3. Make sure the `SkinnedMeshRenderer`'s **Bones** array still points to the original rig — the new mesh shares the same bone indices

!!! tip
    Because the extracted mesh shares bone indices with the original, it will animate correctly when bound to the same skeleton.

---

## Child Bone Inclusion

The **Include Child Bones** toggle controls whether child bones of the selected bone are included in the extraction query.

=== "Include Child Bones ON (default)"

    Selecting the Head bone also captures geometry influenced by:

    - Jaw / chin bones
    - Eye bones
    - Eyebrow bones
    - Ear bones
    - Any accessory bones parented to the head

=== "Include Child Bones OFF"

    Only vertices directly influenced by the selected bone are extracted. Useful when you want a precise, minimal extraction without pulling in adjacent geometry.

---

## Read/Write Requirement

Unity's `Mesh` API requires a mesh to have **Read/Write Enabled** before vertex and triangle data can be accessed at edit time. If your mesh doesn't have this flag set:

- Use the **🔧 Enable Read/Write on Source Mesh** button in the tool
- Or enable it manually: select the FBX/model asset → Inspector → **Model** tab → check **Read/Write Enabled** → Apply
