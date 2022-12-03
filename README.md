# Roblox-2016-Shadow-Engine

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


## Getting Started:
  ### Installing the engine
    1. First, copy the Shadow_Modules.rbxmx file.
    2. If you plan on using the engine locally, *right click*