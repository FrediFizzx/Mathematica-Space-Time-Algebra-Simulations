# Local QM Singlet Prediction Using SpaceTime Algebra — 2D Detector Sweep

## Overview
This notebook implements a 2D detector‑sweep version of the Local Quantum Mechanical (LQM) prediction for the singlet state using **SpaceTime Algebra (STA)**. It is based on Joy Christian’s 3‑sphere model but uses a clean STA rotor‑sandwich formulation instead of Pauli matrices. The simulation evaluates the STA analogue of the quantum‑mechanical correlation



\[
E(\theta) = -\cos\theta
\]



over a full **720° sweep** of detector angle differences.

Detector directions are restricted to a **single measurement plane**, while particle spins remain **full 3D bivectors**. This matches the geometry of real correlation‑vs‑angle experiments and produces the clean, publication‑grade correlation curve.

---

## Purpose of This Simulation
This 2D sweep serves a specific role in the overall STA singlet project:

- It provides an **experiment‑style correlation plot** as a function of a single angle \(\theta\).
- It demonstrates that the STA rotor‑sandwich model reproduces the expected  
  

\[
  E(\theta) = -\cos\theta
  \]


  over the full \(-360^\circ\) to \(+360^\circ\) domain.
- It complements the **analytic STA singlet derivation** and the **full 3D STA simulation** by showing the correlation curve in the same form used in Bell‑type experiments.

This notebook is the one that produces the figure suitable for inclusion in the paper.

---

## Method Summary
- Spins \(s_1\) and \(s_2\) are sampled as **uniform 3D unit bivectors** on the sphere, with \(s_2 = -s_1\) enforcing angular momentum conservation.
- Detector directions \(a\) and \(b\) are chosen as **2D vectors** in a fixed plane and embedded into STA.
- Each trial computes the STA rotor‑sandwich interaction:
  

\[
  g_A = \phi^\dagger\, a\, s_1\, \phi,\qquad
  g_B = \chi^\dagger\, s_2\, b\, \chi.
  \]


- The scalar part of \(g_A g_B\) is accumulated into 1° bins over a 720° range.
- After averaging, the correlation array is corrected with:
  ```wl
  Eavg = RotateLeft[Eavg, 1];
  ```
  to compensate for the +361 indexing offset.
- The final plot overlays:
  - the blue STA correlation data,
  - the magenta \(-\cos\theta\) curve,
  - the gray triangular envelope lines,
  - and angle ticks from \(-360^\circ\) to \(+360^\circ\).

---

## Running the Simulation
1. Install or load the **Clifford.m** package (included in the repository).
2. Open the notebook `localQMaveragingSTA-2D.nb`.
3. Evaluate the notebook from top to bottom.
4. The final output is a 720° correlation plot showing the STA prediction.

The simulation uses \(m = 100{,}000\) trials by default. You may increase or decrease this depending on performance.

---

## Expected Output
The notebook produces a figure titled:

**“Blue is the Product Correlation Data; Magenta is the Negative Cosine Curve.”**

You should see:

- a smooth blue correlation curve,
- perfectly aligned with the magenta \(-\cos\theta\) curve,
- symmetric around 0°,
- with no endpoint artifacts (thanks to `PlotRange` clipping and the one‑bin rotation fix).

This plot is suitable for inclusion in the supplemental material of the paper.

---

## Relation to the Other Simulations
This 2D sweep is **one of three** components in the full STA singlet project:

- **Analytic STA singlet calculation**  
  Direct STA analogue of the QM expression  
  \(\langle\psi|(\mathbf a\cdot\sigma)(\mathbf b\cdot\sigma)|\psi\rangle\).  
  No sampling, no spins \(s_1, s_2\).

- **3D STA simulation**  
  Full 3D spins and 3D detectors.  
  Numerical confirmation that the STA rotor‑sandwich reproduces  
  \(-a\cdot b\) for arbitrary directions.

- **2D detector sweep (this notebook)**  
  Produces the clean experimental‑style correlation curve.

Together, these three pieces form a complete analytic + numerical validation of the STA singlet prediction.
