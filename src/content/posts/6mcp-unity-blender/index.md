---
title: MCP with Blender & Unity
published: 2025-08-11
description: MCP with Blender & Unity
tags: [MCP, Blender, Unity, Claude AI, 3D Modeling]
category: Tutorial
draft: false 
---

# MCP in Blender & Unity with Claude AI

Recently, I experimented with **MCP (Model Context Protocol)** to connect 3D tools like Blender and Unity with Claude AI. My goal was straightforward: see if AI could directly manipulate or inspect my 3D environments in real time. This post is less of a polished how-to and more of a developer log — what worked, what broke, and what I learned.

# Understanding MCP
**MCP (Model Context Protocol)** is an open protocol that standardizes how applications talk to large language models (LLMs).  

Key ideas I had to wrap my head around:
- Two-way communication between AI and programs.
- Ability to **create, modify, or delete 3D objects**.
- Editing materials, inspecting entire scenes, and even executing code through the AI.

💡 *Why this matters*: Instead of AI being a “detached helper,” MCP turns it into an active collaborator inside your workflow. That was the hook for me.

# Tools & Sources
- **Blender** 3.0+
- **Unity** 6+
- **Python** 3.10+ (Blender MCP), 3.12+ (Unity MCP)
- [Blender MCP GitHub](https://github.com/ahujasid/blender-mcp)  
- [Unity MCP GitHub](https://github.com/CoplayDev/unity-mcp)  
- Claude AI App
- UV Package Manager

---

# Step-by-Step Setup

## Setup
### 1. UV Package Manager
This is required for both Blender and Unity MCP.  
- Open terminal and install UV Package Manager.  
- If the first command failed, switch to the alternative one provided in the docs.

💡 *Why*: 
MCP depends on the package manager for dependency handling. Without this, nothing connects properly.


## Blender MCP Setup
### 1. Addon Installation
- Download **addon.py** from [Blender-MCP GitHub](https://github.com/ahujasid/blender-mcp).
- In Blender, go to `Edit → Preferences → Add-ons`.
- Click **Install from Disk** and select the addon.py file.
- Enable the addon by checking the box next to "Interface: Blender MCP".

💡 *Why*: 
This gives Blender a sidebar tab for MCP. Without the addon, Blender doesn’t know how to “talk” to Claude.


### 2. Blender MCP Tab
- Open the **3D View sidebar** (press `N`).  
- Find the **BlenderMCP** tab.  
- Check *Poly Haven* if you want asset streaming.  
- Click **Connect to Claude**.

💡 *Why*: 
This is where you actually link Blender’s context to Claude. It felt surreal seeing AI recognize what was in my scene.

### 3. Claude AI Config
- Open **Claude AI App** and go `Settings → Developer → Edit Config`.  
- Copy and paste the below code in **claude_desktop_config** file.
```json
{
  "mcpServers": {
    "blender": {
      "command": "uvx",
      "args": ["blender-mcp"]
    }
  }
}
```
- Restart the computer.

💡 *Why*: 
This step gives Claude the bridge it needs to process MCP requests. Took me a few tries before it clicked.

### Video


---

## Unity MCP Setup
### 1. Python Path Setup (Windows)
- Open Python file and click “Open File Location”.
- Copy the file path.
- Open “Edit the system environment variables”.
- Click Environment Variables.
- Click Path in System variables and Edit.
- Paste the file path.

### 2. Package Installation
- In Unity, open `Window → Package Manager`.  
- `Click + → Add package from Git URL...`.  
- Paste the link: https://github.com/CoplayDev/unity-mcp.git?path=/UnityMcpBridge.
- Click Add.

💡 *Why*: MCP for Unity isn’t built-in — GitHub package installation is the only way to get it.

## 3. MCP Auto-Setup
- Go `Window → Unity MCP`.
- Click Auto-Setup.
- Look for a green status indicator🟢 and "Connected ✓". (This attempts to modify the MCP Client's config file automatically).
- Restart the computer.

💡 *Why*: Auto-setup edits the MCP client config automatically. Saves time and avoids manually editing JSON files.

## Video

---

# Discussion & Reflections
- **Challenges**: MCP requires detailed context to be useful. If you don’t feed enough scene info, the AI’s edits are random or incomplete.  
- **What worked**: Once connected, I could spawn and modify objects in Blender directly through Claude — faster than manual modeling tweaks.  
- **Limitations**: MCP helps speed up repetitive tasks. But currently it doesn’t replace a human designer at all. You still need to think critically about scene composition.

---

# Future Outlook
- **Game Development**: AI-assisted real-time prototyping inside Unity.  
- **Simulation**: Rapid environment adjustments for training data.  
- **VR/AR Content Creation**: AI could manage assets or materials while you focus on immersion.  
- **Labor Impact**: Might reduce grunt work, but creative direction still belongs to humans.

---