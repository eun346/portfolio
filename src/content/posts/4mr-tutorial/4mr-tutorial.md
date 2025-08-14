---
title: MR Meta Quest Step-by-Step Tutorial
published: 2025-08-12
description: MR with Meta Quest 3
tags: [MR (Mixed Reality), Unity, Meta Quest, Tutorial]
category: Tutorial
draft: false 
---

## Mixed Reality on Meta Quest 3

I've been diving into Mixed Reality (MR) recently, and I wanted to experiment with a simple Passthrough prototype on my Meta Quest 3. The goal was simple but oddly satisfying: see my real room through the headset, spawn virtual balls, and watch them bounce off walls and floors. Honestly, it felt a bit like playing catch with my own furniture. This post is my personal developer log — not a polished tutorial. I’ll walk through what I did, why I did it, what broke (and it did), and what I learned along the way.

## Tools
- Unity: v.2020.3+
- Meta Quest 3
- USB-c Cable (for Building)
- [Oculus Integration Package from Unity Asset Store](https://assetstore.unity.com/packages/tools/integration/oculus-integration-deprecated-82022?srsltid=AfmBOoqs3VykViopb9qVxMb3gFcYp88tIxOFRBEoxyUs_zHPXRYparKT)

I used 2020.3.1f Unity version. Passthrough and OVRManager behaves slightly differently depending on Unity version. Specifying this ensures anyone trying to replicate my steps hits the same quirks and solutions I did.

## Understanding the Basics
Before jumping into Unity, I clarified the essential concepts.
- Mixed Reality (MR): blends virtual content with the real world.
- Extended Reality (XR): umbrella term for VR, AR, and MR.
- Passthrough: lets you see the real world through the Quest's cameras, layered with virtual objects.

💡Focus: MR is not just "turn on a camera." Understanding this early saves time when configuring cameras, layers, and interactions in Unity.

## Step-by-Step Tutorials

# Setup
1. Enable Developer Mode

- Create a Meta Developer Account in [Meta].(https://developers.meta.com/horizon/sign-up/)
- Turn on Developer Mode in the Meta Horizon app.

