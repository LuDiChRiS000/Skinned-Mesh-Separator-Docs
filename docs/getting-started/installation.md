# Installation

## Requirements

- Unity **2020.3 LTS or above** (tested through Unity 6.x)
- Any render pipeline (Built-in, URP, HDRP)

---

## Option 1: Unity Package Manager (Recommended)

Install directly through the Unity Package Manager from the Asset Store.

1. Open Unity and navigate to **Window → Package Manager**
2. Select **My Assets** from the dropdown
3. Find **Skinned Mesh Separator** and click **Download**, then **Import**

---

## Option 2: Manual Installation

If you have the `.cs` file directly:

1. In your Unity project, create an `Editor` folder inside `Assets` if one doesn't exist
2. Place `SkinnedMeshSeparator.cs` inside the `Editor` folder

```
Assets/
└── SkinnedMeshSeparator/
    └── Editor/
        └── SkinnedMeshSeparator.cs
```

!!! warning "Editor folder required"
    The script **must** be placed inside a folder named `Editor`. Unity will throw compile errors if it is placed in a non-editor folder, because the script references `UnityEditor` APIs that are not available in builds.

---

## Verify Installation

Once installed, the tool will appear in Unity's menu bar:

**Tools → Skinned Mesh Separator**

Click it to open the editor window. If you don't see the menu item, check the Console for compile errors and ensure the script is inside an `Editor` folder.
