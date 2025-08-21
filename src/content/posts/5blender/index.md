---
title: Blender Tutorial
published: 2025-08-07
description: Blender Basics & Floor Plan
image: "./images/0cover.png"
tags: [Blender, 3D Modeling, Floor Plan]
category: Tutorial
draft: false 
---

# My Blender Tutorial Experience
I recently dove into 3D modeling with **Blender**, a free yet insanely powerful tool. My goal? Prepare for future **Unity** projects and finally get comfortable creating things from scratch in 3D. To kick things off, I followed two YouTube tutorials:
- [Blender Beginner Tutorial](https://www.youtube.com/watch?v=Ci3Has4L5W4)  
- [Blender Floor Plan Tutorial](https://www.youtube.com/watch?v=94kAIpRnhcY)  

---

# Understanding the Basics
Before starting, I clarified essential 3D modeling concepts.  

| Term       | Description |
| ---------- | ----------- |
| `Mesh`     | A combination of vertices (points), edges (lines), faces (polygons), or any combination of these. |
| `Geometry` | Any 3D object with position data, including meshes, curves, instances, volumes, etc. |
| `Instance` | A duplicate of an object sharing the same underlying data as the original. |
| `Shader`   | A program controlling how light interacts with a surface, affecting color, reflection, transparency, and emission. In Blender, it’s often used interchangeably with `material`. |

💡 *Why it matters*: Blender can feel like a maze at first. Understanding meshes, modifiers, and basic geometry gave me a clear roadmap—I suddenly knew what to click, move, and tweak.

---

# Tools & Resources
- **Blender**: [Download v4.4](https://www.blender.org/download/releases/4-4/)  
- YouTube Tutorials:  
    - [Beginner Tutorial](https://www.youtube.com/watch?v=Ci3Has4L5W4)  
    - [Floor Plan Tutorial](https://www.youtube.com/watch?v=94kAIpRnhcY)  

---

# Essential Shortcuts
| Shortcut | Action |
| -------- | ------ |
| `Middle Mouse` | Orbit around scene |
| `Shift + Middle Mouse` | Pan view |
| `Mouse Wheel Scroll` | Zoom in/out |
| `Tab` | Switch between Object/Edit Mode |
| `N` | Toggle Sidebar |

For **Object Mode**:
| Shortcut | Action |
| -------- | ------ |
| `T` | Toggle Toolbar |
| `G` | Move objects |
| `R` | Rotate objects |
| `S` | Scale (resize) objects |
| `Shift + A` | Add object |
| `Alt` (when adding) | Add object in perfect form (e.g., perfect cube or triangle) |
| `Ctrl + L` | Link properties between objects |

💡 *Tip:* For more shortcuts, check Blender’s [Keymap Documentation](https://docs.blender.org/manual/en/latest/interface/keymap/introduction.html).

### Recommended Setup
- Go to `Edit > Preferences > Interface` and adjust the **Resolution Scale**  
💡 *Why:* Makes Blender easier to work with depending on your screen size.  

- Check your GPU under `System > Cycles Render Devices > CUDA`  
💡 *Why:* Ensures hardware acceleration for faster rendering.  

- Increase **Undo Steps** to **100** in `System > Memory & Limits`  
💡 *Why:* Allows more flexibility when correcting mistakes.  

---

# Step-by-Step Experience

## Tutorial 1: [Blender Beginner Tutorial](https://www.youtube.com/watch?v=Ci3Has4L5W4)
This tutorial covered the fundamentals:  
- Navigating Blender’s viewport  
- Differences between **Edit Mode** and **Object Mode**  
- Building a simple object step by step  

---

#### 1. Cookie Base
![cookieBase](./images/1Blender1-1.png)
- Add a **Cylinder** (`Shift + A > Mesh > Cylinder`).
- Scale (`S`) to flatten into a cookie shape.
- Right-click → `Shade Smooth` for a softer look.
![rename](./images/2Blender1-2.png)
- Rename it Cookie in the Outliner to stay organized.

#### 2. Chocolate Chips
![uvSphere](./images/3Blender1-3.png)
- Add a **UV Sphere** (`Shift + A > Mesh > UV Sphere`)  
- Scale down (`S`) to chip size  
- Position using **Move** (`G`)  
![duplicate](./images/4Blender1-4.png)
- Duplicate chips (`Shift + D`) and place around the cookie  

#### 3. Tray
- Add a **Cube** (`Shift + A > Mesh > Cube`)  
- Scale and move to sit under cookie
1[insetFace](./images/5Blender1-5.png)
- Enter **Edit Mode** (`Tab`), select top face, use **Inset Faces** (`I`)  
![extrude](./images/6Blender1-6.png)
![extrude2](./images/7Blender1-7.png)
- Extrude inner face down (`E`) to create tray depth
![move](./images/8Blender1-8.png)
- Move the tray under the cookie.

#### 4. Materials & Colors
![color](./images/9Blender1-9.png)
- Add material in **Material Properties** → `New`  
- Choose **Base Color** for cookie, chips, and tray  
![link](./images/10Blender1-10.png)
- To quickly assign the same material, select chips → last chip with material → `Ctrl + L > Materials`  

#### 5. Lighting & Rendering
![renderview](./images/11Blender1-11.png)
- Click **Viewport Shading: Rendered**
- Delete default light → Add **Area Light** (`Shift + A > Light > Area`)  
![camera](./images/12Blender1-12.png)
- Position camera (`0` on numpad, enable **Camera to View**)  
- Set render engine to **Cycles** for realism  
![image](./images/13Blender1-13.png)
- Render with `F12` → Save via `Image > Save As`  

---

## Tutorial 2: [Blender Floor Plan Tutorial](https://www.youtube.com/watch?v=94kAIpRnhcY)
This tutorial focused on combining objects and creating a full scene:  
- Importing and scaling floor plan images  
- Modeling floors and walls  
- Applying materials, lighting, and render settings  

#### 1. Setup
- Download a floor plan image  
- Open Blender, select all (`A`) and delete (`X`) default objects  
- `Import image → Creates an Empty object`  
![img](./images/15Blender2-1.png)
- Reset location & rotation: `Alt + G`, `Alt + R`  
- Switch to Top Orthographic View (`7` on numpad or click z in xyz)  
- Set **Units** to Metric (Scene Properties → Units → Metric → Meters)  

#### 2. Floor & Walls
![plane](./images/16Blender2-2.png)
- Add **Plane** (`Shift + A > Mesh > Plane`)
![scale](./images/17Blender2-3.png)
- Rename to **Walls** and set dimensions in Item Sidebar → Apply scale (`Ctrl + A > Scale`) 
![wallsOrigin](./images/18Blender2-4.png)
- Click `walls` and set origin (`Shift + S > Cursor to Selected` & `Right Click > Set Origin > Origin to 3D Cursor`) and clear any translation by `Alt + G`
![onlyface](./images/19Blender2-5.png)
- In **Edit Mode**, delete face (`X > Only Faces`)
- In **Object Mode**, move the **floor plan image** fit right in the **Wall** line
- Delete three vertices in Walls (`X > Vertices`)
![extrudevertices]
![vertices](./images/20Blender2-6.png)
- **In Edit Mode**, extrude vertices (`E`) along X/Y to match outer walls
- Extrude inner walls for rooms too
![floor](./images/21Blender2-7.png)
- Duplicate Walls and rename the duplicated one as **Floor** and hide the **Walls** by clicking eye icon
- For the same floor, delete some overlap unnecessary vertices
- For each room, select all of the vertices and make a face(`F`).

#### 3. Finalizing & Rendering
![background](./images/22Blender2-8.png)
- Duplicate floor (`Shift + D > Right Click`) and rename **Background**
- Hide Floor and Walls
- In Background, delete all inner vertices  
- Extrude everything and scale (`A > E > S`)
![zextrude](./images/23Blender2-10.png)
- Hide Floor and Background. Select Walls → Extrude upwards along Z-axis (`E > Z`)  
![ori](./images/24Blender2-11.png)
- See walls' orientation (`Overlays menu > Face Orientation`)
Modifier. 
![sol](./images/25Blender2-12.png)
![mod](./images/26Blender2-13.png)
- Add **Solidify Modifier** (`Modifier > Add Modifier > Solidify`) and change some settings (Mode Complex, Thickness) 
- Click Monitor Icon in Modifier
![flip](./images/27Blender2-14.png)
- Fix flipped faces (`Shift + N`) (Blue = outter, Red = inner)
- Click monitor icon again
- Orientation overlay off (`Overlays menu > Face Orientation`)
![end](./images/28Blender2-15.png)
- Save your work (`Ctrl + S`)

---

# Summary
At the end of the day, it wasn’t just about a cookie or a floor plan. These tutorials taught me how to bring any idea to life in 3D. Modeling, texturing, lighting—once you get the hang of these, you’re ready for bigger projects, whether it’s games, architectural visualization, or AR. Honestly, seeing something I imagined appear on screen made me even more excited to dive into Unity. In 3D, the only limit really is your imagination.

💡 *Final Tip:* Always organize objects, name them clearly, and save iterations frequently. This keeps projects manageable as scenes get complex.

---