---
title: Blender Tutorial
published: 2025-08-07
description: Blender Basics & Floor Plan
tags: [Blender, 3D Modeling, Floor Plan]
category: Tutorial
draft: false 
---

# My Blender Tutorial Experience
Recently, I decided to dive into the world of 3D modeling using Blender, a powerful and free 3D creation tool for my future Unity content. I followed two great Blender tutorials I found on YouTube.  
- [Blender Beginner Tutorial](https://www.youtube.com/watch?v=Ci3Has4L5W4)  
- [Blender Floor Plan Tutorial](https://www.youtube.com/watch?v=94kAIpRnhcY)  

# Understanding the Basics
Before diving into Blender, I clarified the essential concepts of 3D modeling.    

| Words     | Description |
| --------- | ----------- |
| `Mesh`    | A composition of vertices (points), edges (lines), faces (polygons), or combinations of these. |
| `Geometry`| Any object in 3D space with position data, including meshes, curves, instances, volumes, and more. |
| `Instance`| A duplicate of an object that shares the same data as the original. |
| `Shader`  | A program that defines how light interacts with surfaces or volumes, controlling properties like color, reflection, transparency, and emission. Often used interchangeably with `material` in Blender’s Shader Node system. |

💡 *Why this matters*: Without a mental model, Blender feels overwhelming. Once I grasped the logic of mesh editing and modifiers, things started to click.

# Tools
- [**Blender**](https://www.blender.org/download/releases/4-4/) (I used v.4.4)
- Youtube Links
    - [Blender Beginner Tutorial](https://www.youtube.com/watch?v=Ci3Has4L5W4)  
    - [Blender Floor Plan Tutorial](https://www.youtube.com/watch?v=94kAIpRnhcY)  

---

# Step-by-Step Experience
## Tutorial 1: [Blender Beginner Tutorial](https://www.youtube.com/watch?v=Ci3Has4L5W4)
This one focused on the fundametals:
- Navigating Blender’s viewport
- Blender shortcut for efficiency
- Using edit mode vs. object mode
- Building a simple object step by step

### Shortcuts
| Shortcut | Action |
| -------- | ------ |
| `Middle Mouse` | Orbit around scene |
| `Shift + Middle Mouse` | Pan view |
| `Mouse Wheel Scroll` | Zoom in/out |
| `Tab` | Switch between Object/Edit Mode |
| `N` | Toggle Sidebar |

The below shortcuts are for object mode.
| Shortcut | Action |
| -------- | ------ |
| `T` | Toggle Toolbar |
| `G` | Move selected items |
| `R` | Rotate selected items |
| `S` | Scale (resize) selected items |
| `Shift + A` | Add object |
| `Alt (while adding)` | Add object in its regular form (ex: perfect cube, regular triangle) |
| Ctrl + L | Link Properties |

💡 If you want to learn more, check out Blender’s [Common Shortcuts](https://docs.blender.org/manual/en/latest/interface/keymap/introduction.html).

### Setup (Recommended)
- Go `Edit > Preferences` for your settings
- Adjust the interface scale in `Interface > Display > Resolution Scale`.
  💡 *Why*: If the interface feels too small or large on your screen, this makes Blender easier to work with.  

- Check your GPU under `System > Cycles Render Devices > CUDA`.
  💡 *Why*: Ensuring the correct GPU is enabled allows Blender to use hardware acceleration for faster rendering.  

-  Increase **Undo Steps** to **100** in `System > Memory & Limits`.
  💡 *Why*: The default is often too low, meaning you can’t go back far enough if you make a mistake. Increasing it gives you more flexibility.  

### Making Cookie
#### 1. Adding the Cookie Base
- **Add a Cylinder**: Press **Shift + A** and choose `Mesh > Cylinder`.
- **Shape It**: Use the **Scale** tool (shortcut **S**) to flatten the cylinder into a cookie shape.
- **Smooth the Surface**: Right-click on the cylinder and select `Shade Smooth` to give it a nice, soft look.
- **Rename**: In the Outliner panel, double-click the object's name and change it to **Cookie**.

#### 2. Adding Chocolate Chips
- **Add a UV Sphere**: Press **Shift + A** and select `Mesh > UV Sphere`.
- **Scale It Down**: Press **S** to make the sphere small, like a chocolate chip.
- **Position It**: Use the **Move** tool (**G**) to place it on the surface of your cookie.
- **Duplicate**: Press **Shift + D** to duplicate the chip, then place the new ones around the cookie.

#### 3. Building a Tray
- **Add a Cube**: Press **Shift + A** and choose `Mesh > Cube`.
- **Position and Scale**: Use **S** to resize the cube and **G** to move it so it sits under the cookie.
- **Create the Inside**: Press **Tab** to enter Edit Mode. Select the top face of the cube and use the **Inset Faces** tool (**I**) to create a smaller inner face.
- **Make It a Tray**: Use the **Extrude Region** tool (**E**) to push the inner face down, creating the tray's depth.

#### 4. Adding Materials and Colors
- **Add a New Material**: Go to the **Material Properties** tab (the red sphere icon) and click `New`.
- **Set the Color**: Under **Base Color**, choose a color for your cookie. Repeat this step for the chocolate chips and the tray, giving each its own material.
- **Link Materials**: To quickly color all the chips, select them, then select one chip that already has the material. Press **Ctrl + L** and choose `Make Links > Materials`.

#### 5. Lighting & Rendering
- **Delete the Default Light**: Click on the **default light** in your scene and press **Delete**.
- **Add an Area Light**: Press **Shift + A** and select `Light > Area`.
- **Position the Camera**: Press the **0** key on your number pad to switch to the camera view. Press **N** to open the sidebar, then in the **View** tab, check **Camera to View**. Now you can move your camera by simply navigating your scene.
- **Set the Engine**: In the **Render Properties** tab (the camera icon), change the **Render Engine** to **Cycles** for a more realistic look.
- **Render the Image**: Press **F12** to render your final image. Once it's done, go to `Image > Save As` to save your work.

---

## Tutorial 2: Intermediate Project
The second tutorial raised the bar:
- Combining multiple objects into a single scene.  
- Applying textures and basic lighting.  
- Playing with render settings for a final polished look.  

### **3D Floor Plan Creation Guide in Blender**
#### 1. Setting Up the Floor Plan
* **1. Download a Floor Plan:** Find and download a floor plan image from a site like floorplans.com or houseplans.com.
* **2. Prepare Blender:** Open Blender, press **A** to select everything (the default cube, camera, and light), and then press **X** to delete them.
* **3. Import the Image:** Drag and drop your downloaded floor plan image directly into the Blender viewport. This will create an Empty object.
* **4. Position the Image:** With the Empty selected, press **Alt + R** to clear its rotation and **Alt + G** to clear its location, placing it at the center of the scene. Press **7** on the number pad to switch to Top Orthographic View.
* **5. Set Scene Units:** Go to the **Scene Properties** tab (the icon of two cones), and under the **Units** section, change the `Unit System` to `Metric` and the `Length` to `Meters`.

### 2. Creating the Floor and Walls
* **1. Create the Floor:** Press **Shift + A**, and choose `Mesh > Plane`. Rename this new object to **Floor** by pressing **F2**.
* **2. Match Dimensions:** In the **Item** sidebar (press **N** to open it), enter the dimensions of your floor plan (e.g., 7m x 7.6m). Then, press **Ctrl + A** and select `Scale` to apply the changes.
* **3. Draw the Walls:**
    * Switch to **Edit Mode** by pressing **Tab**. Delete the plane's face by pressing **X** and selecting `Only Faces`.
    * Select one of the remaining vertices and press **E** to extrude. As you extrude, press **X** or **Y** to constrain the movement along an axis.
    * Continue this process, extruding and moving vertices to trace the entire outer outline of your floor plan.
    * To create inner walls, extrude from the outer wall vertices and trace the internal room layouts.

### Part 3: Finalizing and Rendering
* **1. Create the Background:** In **Object Mode**, select your **Floor** object and duplicate it with **Shift + D**. Rename the duplicate to **Background**. Enter **Edit Mode**, press **A** to select all vertices, and press **X** to delete `Only Faces`. Now, with the outline selected, press **E** to extrude and **S** to scale, creating a frame.
* **2. Extrude the Walls:** Hide the **Floor** and **Background** objects. Select your **Walls** object, enter **Edit Mode**, press **A** to select all vertices, and press **E** to extrude them upwards along the Z-axis (**Z**). Enter a height (e.g., 2.3m) and press **Enter**.
* **3. Solidify the Walls:** With the **Walls** object selected, go to the **Modifier Properties** tab (the wrench icon) and add a `Solidify` modifier. Set the `Mode` to `Complex` and adjust the `Thickness` to your desired wall thickness (e.g., 0.15m).
* **4. Check Face Orientation:** In the viewport's **Overlays** menu, turn on `Face Orientation`. Blue faces are correct; red faces are flipped. In **Face Select** mode (**3** key), select any red faces on the outer walls and press **Shift + N** to fix their orientation.
* **5. Save Your Work:** Press **Ctrl + S** to save your project.
