# intermolecular-Navier-Stokes-Extension

> Intermolecular activity-based extension of Navier–Stokes equations for hypersonic continuum flow.
> **Pre-publication draft — shared for review only.**

---

## Status

This repository contains a **preliminary research manuscript**.

* Not peer-reviewed
* Not finalized
* Shared only for **technical feedback and scrutiny**

**This work should not be cited or reused.**

---

## Contents

- `intermolecular_ns_extension.pdf` — Full manuscript (pre-publication draft)  
- `ns_model_viz` — Interactive visualization of model behavior
-  `Stress Test Sandbox.zip`-Equation stress test sandbox for reviewers

## Overview

This work introduces a modified Navier–Stokes formulation incorporating **intermolecular pressure contributions** using a thermodynamically consistent framework.

Author Statement

All theoretical development, derivations, and modeling presented in this manuscript are original work by the author. Any computational or writing tools used did not contribute to the scientific reasoning or results.

Update: I have uploaded a script Stress testing the equation against imaginary physics and at universal scale, reviewers may use it to chack validation and stress test the equations but the script must not be replicated or reused for other academic purposes, The sandbox script and values are in the assumption of the current scope of the model, it is not a representative scale.

Key elements:

* Pressure decomposition:
  ( P = P_{NS} + P_{IM} )
* Van der Waals attractive term with Redlich–Kwong temperature scaling
* Fully coupled density and temperature gradient contributions
* No empirical parameters in final formulation (uses published constants)
* A value sandbox to stress test

A new dimensionless parameter is defined:

> **Intermolecular Activity Number** ( I_a )

which characterizes the transition between classical and intermolecularly-influenced flow regimes.

---

## Validation

The formulation is evaluated using:

* Planar Poiseuille flow (velocity profile deviation)
* Intermolecular activity scaling vs temperature and density
* Hypersonic regime mapping (Mach vs ( I_a ))
* Transport and thermodynamic consistency checks

All results show:

* Recovery of classical Navier–Stokes limit
* Physically consistent deviations in intermediate-density regimes

---

## Repository Structure

```
.
├── README.md
├── LICENSE
├── intermolecular_ns_extension.pdf
├── ns_model_viz.html
└── Stress Test Sandbox.zip
```

---

## ⚙️ Model Scope

Valid under:

* Continuum regime (low Knudsen number)
* Intermediate density conditions
* Temperature range ~500–2000 K
* Hypersonic flows (Mach 5–25)

Limitations include:

* No chemical reactions or ionization
* Orientation-averaged intermolecular interactions
* Reduced-order thermodynamic closure

---

## Usage Restrictions

This repository is released under **All Rights Reserved**.

* No reproduction
* No redistribution
* No derivative work
* No formal citation

This is a **review draft only**.

---

## Feedback

Critical review is welcome.

If you find:

* inconsistencies
* broken assumptions
* edge-case failures

→ open an issue or discussion.

---

## Author

Ayush Sreejith
Independent research (pre-university)

---

##  Note

This work builds upon established physical models including:

* Navier–Stokes equations
* van der Waals equation of state
* Redlich–Kwong temperature scaling
* Sutherland transport law

All foundational models remain credited to their original sources.

---

