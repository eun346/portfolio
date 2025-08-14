---
title: MR Meta Quest Tutorial
published: 2025-08-12
description: MR with Meta Quest 3
tags: [MR, Unity, Meta Quest, Tutorial]
category: Tutorial
draft: false 
---

# Building a Mixed Reality Passthrough Experience on Meta Quest 3 (Unity)

*By Eunha Choi*

I've been experimenting with **Mixed Reality (MR)** lately, and decided to build a simple Passthrough prototype on my **Meta Quest 3**. The goal was straightforward but satisfying: see my real room through the headset, spawn virtual balls, and watch them bounce off walls and floors. Honestly, I was both excited and a little nervous — I wasn't sure if the physics would behave properly on the first try.

This post is my personal developer log — not a polished tutorial. I'll walk through what I did, why, what broke, and what I learned along the way.

---

## Versions & Setup (for reproducibility)

* **Unity:** 2023.1.0f1 (LTS recommended for stability)
* **Oculus Integration:** v64.0
* **Quest 3 Firmware:** v60.0.0.341.123
* **Build Target:** Android (ARM64)

💡 *Why this matters:*
Passthrough and OVRManager behaviors can vary across versions. Specifying this ensures anyone trying to replicate my steps hits the same quirks and solutions I did. I learned this the hard way after one build mysteriously refused to detect the Quest.

---

## 1. Understanding the Basics

Before jumping into Unity, I clarified the essential concepts:

* **Mixed Reality (MR):** blends virtual content with the physical world.
* **Extended Reality (XR):** umbrella term for VR, AR, and MR.
* **Passthrough:** lets you see the real world through the Quest's cameras, layered with virtual objects.

💡 *Why:*
MR isn't just "turn on a camera." I realized quickly that without understanding these basics, I'd spend hours fiddling with cameras, layers, and interactions trying to make sense of weird visuals.

---

## 2. Enabling Developer Mode

1. Create a **Meta Developer Account**.
2. Turn on *Developer Mode* in the Meta Horizon app.

💡 *Why:*
Without it, Unity builds won't run on the Quest. Trust me, I wasted 20 minutes wondering why nothing was showing up before I remembered this step. It's like telling the headset, "I'm making something, not just playing games."

---

## 3. Setting Up Unity for Oculus Development

1. Enable **Oculus** in **Edit → Project Settings → XR Plug-in Management** for both Windows and Android.
2. Install **Oculus Integration** from the Asset Store.
3. Run **Tools → Project Setup Tool → Fix All & Apply All**.
4. Switch platform to **Android** in **File → Build Settings**.

💡 *Why:*
Quest 3 runs Android, and Unity needs the XR plugin + Oculus package to talk to the headset. Skipping these leads to invisible cameras, broken tracking, or Passthrough errors. I definitely learned that the hard way — nothing worse than thinking your code is broken when it's just a setup issue.

---

## 4. Connecting the Headset

* **AirLink (Wireless):** easier setup, slightly blurry, longer builds.
* **USB-C (Wired):** more stable, faster builds — my default choice.

💡 *Why:*
Iteration speed matters. A 10-minute build vs a 2-minute build multiplies quickly if you're testing interactions all day. I got a little impatient waiting on AirLink once — nothing like staring at a frozen loading screen wondering if it will ever finish.

---

## 5. Setting Up Passthrough in Unity

**A. Camera Configuration**

1. Delete the default **Main Camera**.
2. Add **OVRCameraRig** prefab.
3. Configure **OVRManager**:

   * Hand Tracking → "Controllers and Hands"
   * Passthrough Support → "Supported"
   * Enable Passthrough → Checked

💡 *Why:*
OVRCameraRig handles VR rendering, tracking, and input. Passthrough only works when enabled here. I remember thinking, "Finally, a camera that actually shows my messy desk."

**B. Adding the Passthrough Layer**

1. Create an empty GameObject `Passthrough`.
2. Add **OVR Passthrough Layer** component.
3. Placement → "Underlay."
4. Set `CenterEyeAnchor` Clear Flags → Solid Color, background → Black.

💡 *Why:*
Underlay ensures the real world sits behind virtual objects. Otherwise, you get weird blending or block the real view. I spent a few minutes wondering why my balls were floating in black nothingness — turns out Underlay was the missing piece.

---

## 6. Scanning the Real Space

1. Add **OVRSceneManager** to the scene.
2. Assign **Plane** and **Volume** prefabs for surface detection.

💡 *Why:*
Passthrough alone shows your room, but objects can't interact with it. Scene scanning creates a digital mesh so virtual balls actually collide with walls and floors. Honestly, watching my first ball bounce off the real desk had me grinning like a kid.

---

## 7. Adding Ball Interaction

**A. Spawn Script**

* Attach a `SpawnBall` script to `RightHandAnchor`.

**B. Physics**

1. Create a **Physic Material** `Bounce` (Bounciness = 1).
2. Create a small sphere (scale 0.1), add Rigidbody + Bounce material.
3. Link the sphere prefab to the spawn script.

💡 *Why:*
Throwing balls into your room turns Passthrough from "cool view" into interactive MR. Physics makes it feel tangible. I spent a good 10 minutes tossing balls at my chair just to watch the collisions — totally worth it.

---

## 8. What Broke / Lessons Learned

* AirLink → blurry visuals, slower loads.
* USB builds → still \~10 min sometimes.
* Unity sometimes didn't detect Quest if Wi-Fi was misconfigured.

💡 *Developer note:*
Always check networking first before blaming Unity or the headset. I cursed the build process more than once before realizing it was just my Wi-Fi.

---

## 9. Lessons & Extensions

Instead of listing generic MR ideas, here's what I realized **from actually building this project**:

1. **Interactive Navigation Cues** – Seeing balls collide with scanned walls made me think: if virtual objects can interact reliably with meshes, the same logic can overlay arrows or indicators indoors.

2. **Spatial Data Visualization** – Aligning balls with real-world surfaces highlighted the importance of accurate mesh placement. This can directly extend to real-time safety or maintenance overlays on equipment.

3. **Room-Aware Game Mechanics** – Physics interactions with scanned walls suggest gameplay mechanics: using your real room as a level.

4. **Furniture / Object Placement** – Adjusting spawn positions to avoid clipping with walls/furniture revealed the potential to preview objects realistically in real space.

💡 *Takeaway:*
These "future uses" aren't just wishlist items. They are **direct extensions of the problems I solved** while getting Passthrough, physics, and mesh scanning to work. Honestly, it was really satisfying seeing a messy, real-world desk become a playground for MR balls.