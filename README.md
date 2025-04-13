# HWM Microstructure Modeling Toolkit

![Blender](https://img.shields.io/badge/Blender-3.6%2B-orange) ![License](https://img.shields.io/badge/License-MIT-blue)

A Blender Geometry Nodes tool for generating meshes of axon fiber bundles, neurons, and glial cells in human white matter for diffusion-weighted MRI simulation.

## 1. Overview

### Purpose
Generate realistic 3D meshes of human white matter microstructures (axons, neurons, glia) with customizable morphology parameters for diffusion-weighted MRI (dwMRI) simulation.

### Core Features
- **Procedural Modeling**: Uses Blender's Geometry Nodes for dynamic, non-destructive adjustments.
- **Adjustable Parameters**:
  - Axon radius, angular dispersion, branch generation, tortuosity, density, and cell morphology.
- **Export Compatibility**: Save models as `.ply` files for use in [MCMR simulator]([https://github.com/your-repo-link](https://open.win.ox.ac.uk/pages/ndcn0236/mcmrsimulator.jl/stable/)).

## 2. Installation

### Requirements
- [Blender 3.6+](https://www.blender.org/download/)
- No additional Python packages required.

### Setup
1. **Download Files**:
   - Clone this repository or download the `.blend` files for your target structure:
     - `Axon.blend` (axon fiber bundles)
     - `Confinement_box.blend` (confinement geometry)
     - `Neuron_cellbody.blend` (neuronal somata)
     - `Microglial_cell.blend` (microglia)
   - Store them in an organized project folder.

2. **Launch Blender**:
   - Open files via `File > Open` or by double-clicking (if associated with Blender).

---

## 3. Quick Start Guide

### 3.1 Axon Bundles

#### 3.1.1 Setup
1. Open `Axon.blend` in Blender.
2. Locate the Axon Bundle:
   - In the **Outliner** (top-right), expand the `Collection` and select `Fibre unit`.
   - Click the **Modifiers tab** (wrench icon 🛠️) in the **Properties panel** (bottom-right).

#### 3.1.2 Adjust Parameters
- **Key Parameters**:
  - `Radius` (default: 0.5 µm, range: 0.1–2.0 µm)
  - `Angular Dispersion` (default: 0.1 rad, range: 0–0.5 rad)
  - `Branch Position` (default: 0.3, range: 0–1)
- **Edit Values**:
  - Drag sliders or type directly into parameter boxes. Press `Enter` to apply.
- **Bundle-Level Adjustments**:
  - Select `Fibre bundle` in the **Outliner** to modify global settings (e.g., density, alignment).

#### 3.1.3 Export Unconfined Mesh
1. Go to `File > Export > Stanford PLY (.ply)`.
2. **Settings**:
   - Enable `Triangulated Mesh`.
   - Set `Vertex Colors` to `None`.
3. Save and name your file (e.g., `Axon_Unconfined.ply`).

#### 3.1.4 Apply Confinement Box
1. Open `Confinement_box.blend`.
2. **Import Your Mesh**:
   - `File > Import > PLY` and select `Axon_Unconfined.ply`.
3. **Copy Geometry Nodes**:
   - In the **Geometry Nodes Editor** (bottom panel):
     - Select all nodes under `Cube`, press `Ctrl+C` to copy.
     - Select your axon mesh, create a new Geometry Nodes group (`+ New`), delete default nodes, and paste (`Ctrl+V`).
4. Delete the original `Cube` object.
5. Adjust confinement properties (size, rotation) via the **Modifiers tab**.

#### 3.1.5 Export Final Mesh
- Repeat **Section 3.1.3** to save the confined axon bundle.

---

### 3.2 Individual Cells (Neurons, Astrocytes, Microglia)

#### 3.2.1 Setup
1. Open the desired `.blend` file (e.g., `Neuron_cellbody.blend`).
2. In the **Outliner**, locate the cell object (e.g., `Neuron`) and expand its `Collection`.
3. Access parameters via the **Modifiers tab** (wrench icon).

#### 3.2.2 Adjust Parameters
- Modify morphology settings (e.g., dendritic branching, soma size).
- See **Section 4** for parameter ranges and descriptions.

#### 3.2.3 Export
- Follow **Section 3.1.3** to save as `.ply`.

---

### 3.3 Build Complex Cell Collections
1. **Create a New Scene**:
   - `File > New > General`, then delete default objects (`Cube`, `Light`, `Camera`).
2. **Import Models**:
   - Use `File > Import` to add cells or axons.
3. **Duplicate and Arrange**:
   - Before duplicating: Apply modifiers (click `▼` next to the modifier > `Apply`).
   - Right-click objects > `Duplicate` and place them freely.
4. **Export**: Save the entire collection as `.ply` (see **Section 3.1.3**).

---

## 4. Parameter Reference
| Parameter           | Default Value | Range          | Description                          |
|---------------------|--------------|----------------|--------------------------------------|
| Fibre Radius         | 0.53 µm       | 0.17–9.00 µm     | Cross-sectional radius of axons.     |
| Global Angular Dispersion min | x=0.75 y=0.56 z=1.00     | 0–1      | Fiber orientation variability.       |
| Polygon resolution     | 32          | 3-32          | Number of sides of the cross-section of the fibre.      |
| Tortuosity level        | 0.5          | 0.0–3.0        | Curviness of fiber paths.            |

*(Full table available in the documentation.)*

---

## 5. Troubleshooting
- **Missing Modifiers Tab**:
  - Ensure the correct object is selected in the **Outliner**.
  - Press `N` to toggle the sidebar if panels are hidden.
- **Export Errors**:
  - Verify `Triangulated Mesh` is enabled in the PLY export settings.
  - Ensure no non-manifold geometry exists (use `Mesh > Clean Up` tools).

---

## 7. Citation
If you use this toolkit in your research, please cite:
```bibtex
@software{BrainMicrostructureToolkit,
  author = {Jie Ren},
  title = {HWM Modeling Toolkit},
  year = {2025},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/jrhanaba}}
}
