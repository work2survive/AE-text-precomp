# AE Text Precomp (v2.0.0)

[![Live Browser Simulator](https://img.shields.io/badge/Live%20Demo-AE%20ScriptUI%20Simulator-2c8cff?style=for-the-badge&logo=javascript)](https://work2survive.github.io/AE_JS_builder/?jsx=AE_Text_Precomp.jsx&autobuild=true)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)
[![Adobe After Effects](https://img.shields.io/badge/Adobe%20After%20Effects-CS6%20--%20CC%202026%2B-9999FF?style=for-the-badge&logo=adobeaftereffects)](https://www.adobe.com/products/aftereffects.html)
[![Built with Antigravity](https://img.shields.io/badge/Built%20With-Antigravity-4285F4?style=for-the-badge&logo=google)](https://deepmind.google/)

> **Interactive Web Simulator**: Test, customize, and preview this tool directly in your browser without launching After Effects via the [AE JS & ScriptUI Simulator](https://work2survive.github.io/AE_JS_builder/?jsx=AE_Text_Precomp.jsx&autobuild=true).

---

## 📖 Overview

**AE Text Precomp** is an Adobe After Effects ScriptUI panel and ExtendScript engine that encapsulates Paragraph (Box) and Point Text layers into perfectly formatted precompositions with **100% zero visual shift or jump** on screen.

Whenever an anchor point is placed or changed by this script, the precomposition's position is automatically and mathematically compensated using the layer's complete rotation, scale, and parent transform matrix so that the text box on screen never moves a single pixel from its original position.

---

## 🌟 What's New in v2.0.0 (Ground-Up Architectural Rewrite)

1. **Streamlined Single-Panel UI**:
   - Replaced multi-tab clutter with a clean, ergonomic, all-in-one panel matching [AE-Text-Highlight](https://github.com/work2survive/AE-Text-Highlight) and [AE-Align-AnchorPoint](https://github.com/work2survive/AE-Align-AnchorPoint).
   - All vital parameters (Target layer status, Auto/Manual dimensions, Exterior Padding slider, 3x3 interactive Anchor Matrix, Background Card controls, and Actions) are visible and editable at a glance.

2. **True Exterior Padding Geometry (Default: 0px)**:
   - Padding logic moved to exterior canvas expansion: padding is added to the **exterior** of the text box rather than shrinking the internal typesetting frame.
   - Precomp dimensions: $W_{\text{precomp}} = \lceil W_{\text{box}} + 2 \times P \rceil$, $H_{\text{precomp}} = \lceil H_{\text{box}} + 2 \times P \rceil$.
   - Text layer sits inside precomp at $[P, P]$, perfectly framed on all sides without breaking line wrapping or hyphenation.
   - Defaults to **0px** padding for tight bounding box encapsulation.

3. **High-Contrast Fuchsia Background Card (#FF00FF)**:
   - Defaults to vibrant Fuchsia (`#FF00FF`, RGB `[1.0, 0.0, 1.0]`) at 100% opacity for instant bounding visual feedback.
   - Features procedural 4-corner rounded rectangle curves ($K = 0.5522847$) with quick corner presets (`All 4`, `Top Only`, `Bubble`, `Sharp 0`).

4. **Zero-Shift 9-Point Anchor Matrix**:
   - Interactive 3x3 button grid (`[TL][TC][TR] / [ML][ C][MR] / [BL][BC][BR]`) synced bidirectionally with a dropdown selector.
   - Scale-safe and rotation-safe parent comp position compensation:
     $$\vec{P}_{\text{precomp}} = \vec{P}_{\text{orig}} + \mathbf{R}(\theta) \cdot \mathbf{S} \cdot \begin{pmatrix} \text{boxLeft} - P - A_{\text{orig}, x} + A_{\text{precomp}, x} \\ \text{boxTop} - P - A_{\text{orig}, y} + A_{\text{precomp}, y} \end{pmatrix}$$

5. **Direct-Cloning Line & Word Segmentation (Fixes the "W" Bug)**:
   - Completely resolved the issue where dividing by lines/words only showed the letter "W".
   - Text is pre-extracted upfront before duplicating layers.
   - Uses native `origLayer.duplicate()` inside the precomp and sets `Source Text` per-layer without mutating shared documents or inserting throwaway measurement layers that alter layer indices.
   - Preserves 100% of font family, weight, PostScript name, faux styles, fills, strokes, and kerning.

6. **Removed All Legacy Dummy Text Code**:
   - Clean, lightweight, professional codebase focused entirely on user typography.

---

## 📐 Mathematical & Architectural Deep Dive

For complete engine specifications, coordinate transformation proofs, and typography differences between native After Effects and Web Canvas/SVG, see:
- [AE vs. JS Text Rendering Differences Guide](https://github.com/work2survive/AE_JS_builder/blob/main/AE_VS_JS_TEXT_RENDERING_DIFFERENCES.md)

---

## 📄 License

MIT License. Co-authored & architected with Google DeepMind Antigravity for `work2survive`.
