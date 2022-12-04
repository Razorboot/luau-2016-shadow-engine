# Roblox-2016-Multi-Surface-Shadow-Engine

## Description:
Built off of Egomooses Shadow Silhouttes Tutorial: https://scriptinghelpers.org/guides/silhouettes-and-shadows
Created By: Razorboot
Description: 
* An attempt at an optimized raycasted shadow-polygon implementation. 
* This is a complex set of object oriented mini-classes and polygonal algorithms for:
  * accurate n-gon to triangle conversion,
  * clipped polygons,
  * multiple light sources,
  * optimized vertex grabbing,
  * ray to plane intersection,
  * rotated shadow occluders and canvases,
  * world position shadows to 2d space, clipped, triangle-based shadows,
  * surface-based real-time lighting calculations:
    an attempt to make the system appear more well-integrated with shadow engine.
* Inspired by early 2000's Shadow Volumes in games like Thief: Deadly Shadows and Doom III.
* Manifold data-structure system was inspired by collision manifolds in AABB physics.
    This implementation is classless and includes nested arrays as a form of orginization.

## New Changes as of 12/3/22:
* I can confidently say that, in the realm of cube-shapes parts, the current engine is complete!
* Complex multi-surface shadows supported.
* Rotated parts (occluders and canvases) now supported.
* A mini lighting engine for rendering part surfaces is now added and functional in real-time!
  * This supports multiple lighting options you now have control over in Shadow script!
* Shadows are now Surface-Gui based for more optimal results.

## Demos:
* Here is a visual of a fully-rendered scene and it's corresponding parts:
![Group 1](https://user-images.githubusercontent.com/103084464/205473222-2a12b90c-f2e0-41b8-bf54-d5a7161b5eba.png)
* Videos showcasing the engine:
![ezgif com-gif-maker (2)](https://user-images.githubusercontent.com/103084464/205485358-7d54b807-034b-492c-b648-823228a8d3fa.gif)
![ezgif com-gif-maker (3)](https://user-images.githubusercontent.com/103084464/205485469-d6303061-9256-471b-8908-d844c90755e0.gif)



## Getting Started:
### Installing the engine:
1. First, download the ``Shadow_Modules.rbxmx`` file.
2. If you plan on using the engine client-sided, right click on ``StarterGui``, select ``Insert From File``, and select the ``Shadow_Modules.rbxmx`` file.
  * Keep in mind FilteringEnabled will have to be enabled in order to use the client-sided engine.
3. If you plan on using the engine server-sided, right click on ``Workspace``, select ``Insert From File``, and select the ``Shadow_Modules.rbxmx`` file.

### Include the Shadow module:
1. For client-sided, insert a ``LocalScript`` in ``StarterGui``.
2. For server-sided, insert a new ``Script`` in ``Workspace``.
3. To finally include the module, type:
```lua
--# Include
local Modules = --Location of the inserted Shadow_Modules.rbxmx file
local Shadow = require(Modules:WaitForChild("Shadow"))
```

## Creating Light and Shadow Instances:
### Shadow Canvases:
* Shadow Canvases are SurfaceGui's that are mapped onto parts!
* They are the surfaces of a part that can have shadows projected onto them.
* Shadow Canvases are flat planes that can be applied to any face of a Part.
* Shadow Canvases can be added to a part or model using:
 ```lua
 -- Add canvas to all surfaces of a part
 Shadow.setModelProperty(Part, "isShadowCanvasAll", true)
 -- Add canvas to all surfaces of a model
 Shadow.setPartProperty(Part, "isShadowCanvasAll", true)
 ```
* Setting the final parameter to ``false`` will delete a pre-existing canvas.
* ``"isShadowCanvasAll"`` is one out of 6 surfaces. You can replace ``All`` in ``isShadowCanvasAll`` with either Top, Bottom, Right, Left, Front, or Back in order to add a Shadow Canvas to a single surface.

### Occluders:
* Occluders are the Parts that block light sources, and thus cast shadows onto shadow canvases.
* All occluders are treated as cubes, so any other shaped-part will be treated as such.
* I'm currently working on adding more Part-types, so this won't be permanent!
* A part or model can be set to an Occluder using:
```lua
-- Set a part to an Occluder
Shadow.setModelProperty(Part, "isShadowOccluder", true)
-- Set a model to an Occluder
Shadow.setPartProperty(Part, "isShadowOccluder", true)
```
* Exactly as the previous function, setting the final parameter to ``false`` will ensure the part won't cast shadows.

### Lit Surfaces:
* This is an optional category that isn't essential for shadow creation.
* A Lit Surfaces Part allows the brightness of the surfaces of a part to be rendered more accurately to light sources.
* This is my attempt at making part surfaces look less jarring when compared to dark shadows.
* The settings that control the color of part surfaces can be found inside of the ``Shadow`` module inside of the inserted ``Shadow_Modules.rbxmx`` file.
* You can make a part or model have Lit Surfaces using:
```lua
-- Allow the surfaces of a part to be lit
Shadow.setPartProperty(Part, "hasLitSurfaces", true)
-- Allow the surfaces of a model to be lit
Shadow.setModelProperty(Part, "hasLitSurfaces", true)
```
* Lit Surfaces are stored into containers called ``LitPartManifolds``, this allows the script to easily work with them:
```lua
local litPartManifolds = Shadow.getLitPartManifolds()
```
* Lit Surfaces need to be updated each frame in order to account for changes in position relevant to Light Sources:
```lua
litPartManifolds = Shadow.updateLitPartManifolds(litPartManifolds)
```

### Light Sources:
* Light Sources is a list of Lights in your scene that you want to cast shadows and influence Lit Surfaces.
* You can insert all light sources in a container using:
```lua
Shadow.getAllLightSources(workspace)
```
* You can insert and remove a specific light source into your scene using:
```lua
Shadow.insertLightSource(light)
Shadow.removeLightSource(light)
```
* Light Sources need to be updated to account for changes in position and range, you can also update all light sources using:
```lua
Shadow.updateAllLightSources()
```

### Root/Canvas Manifolds:
* When creating shadows, each Shadow Canvas is passed into a function that generates arrays with relevant information for the Occluders and Light Sources that will be taken into account.
* To create a root manifold for all Shadow Canvases, use:
```lua
local rootManifolds = Shadow.getRootManifolds()
```
* Root manifolds need to be updated each frame in order to account for changes in Position of the Shadow Canvas itself, Occluders, and Light Sources:
```lua
rootManifolds = Shadow.updateRootManifolds(rootManifolds)
```
