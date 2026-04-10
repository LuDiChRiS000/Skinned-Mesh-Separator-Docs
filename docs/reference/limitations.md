# Limitations

Understanding these limitations will help you decide whether Skinned Mesh Separator fits your use case — and how to work around them when needed.

---

## Open Geometry at Cut Boundaries

**What happens:** When a region is removed from a mesh, the boundary edges where triangles were deleted are left open (non-watertight). The tool does not automatically cap or close these holes.

**Why:** Closing open mesh geometry requires predicting the intended shape at the cut, which is highly topology-dependent and cannot be reliably automated for arbitrary character meshes.

**When this matters:**

- Real-time rendering of the cut edge at close range (visible seams)
- Physics simulations that require a closed mesh collider

**When this does not matter (most use cases):**

- The extracted mesh is hidden under clothing, armour, or another mesh
- You are masking or toggling the region at runtime (clothing swap systems)
- The extracted mesh is used as a `MeshRenderer` prop (dismemberment, LODs)
- The open edge faces away from the camera

!!! tip "Workaround"
    For cases where closed geometry is required, the extracted mesh can be brought into Blender or another DCC tool to fill the open edge loop manually. The time saving from automated extraction still applies — you only need to close the boundary, not re-split the mesh.

---

## Editor-Only

Skinned Mesh Separator is a Unity Editor tool. It cannot be used at runtime (during Play mode or in a build).

**The intended workflow is:**

1. Extract meshes in the Editor using the tool
2. Save the extracted `.asset` files to your project
3. Use those mesh assets at runtime via `SkinnedMeshRenderer` components or `MeshRenderer` props

If you need to split meshes procedurally at runtime (e.g. dynamically dismember any character, not just pre-prepared ones), this tool is not the right solution. A runtime mesh splitting library would be required for that use case.

---

## Read/Write Requirement

The source mesh must have **Read/Write Enabled** in its import settings. This is a Unity API requirement for accessing vertex data at edit time, not a limitation of this tool. The tool provides a one-click button to enable this setting.

---

## Bone Weight Threshold

Extraction is based on whether a vertex has *any* weight assigned to the target bone (including very small weights). There is no minimum weight threshold. In practice this is rarely an issue, but on meshes with heavy weight painting bleed between regions, a small number of boundary triangles may be captured in or excluded from the extraction unexpectedly.
