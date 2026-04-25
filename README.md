# Intermolecular Activity-Based Extension of Navier–Stokes for Hypersonic Continuum Flow

**Ayush Sreejith** — Independent Researcher, Palakkad, Kerala, India  
*Pre-publication draft — shared for technical review only*

---

## Status

This repository contains a preliminary research manuscript submitted to the **AIAA Journal**.

- Not yet peer-reviewed
- Shared for technical scrutiny and feedback
- Should not be cited, reproduced, or redistributed without author permission

---

## Contents

| File | Description |
|---|---|
| `intermolecular_ns_extension.pdf` | Full manuscript (pre-publication draft) |
| `ns_extended.html` | Interactive browser-based analysis tool |
| `Aero_Tools.zip` | Python CLI tool, physics library, planet selector |
| `Stress_Test_Sandbox.zip` | Mathematical robustness stress tests |
| `LICENSE` | All rights reserved |

---

## Overview

This work proposes a thermodynamically consistent extension to the classical Navier–Stokes equations by incorporating intermolecular pressure contributions through a van der Waals attractive term with Redlich–Kwong temperature scaling.

**Governing equation:**

$$\rho \frac{D\mathbf{u}}{Dt} = -\nabla P_{NS} - \nabla P_{IM} + \mu(T)\nabla^2\mathbf{u} + \mathbf{F}$$

where the intermolecular pressure term is:

$$P_{IM} = -\sum_i \sum_j \frac{a_{ij}(T)\, n_i n_j}{N_A^2}$$

**Key properties:**
- No empirical parameters — all constants from NIST thermochemical tables
- Fully coupled density and temperature gradient contributions retained
- Recovers classical Navier–Stokes exactly in the limit $I_a \to 0$

**A new dimensionless parameter is defined:**

$$I_a = \frac{|P_{IM}|}{(f(T)/2)\, n\, k_B\, T}$$

The **Intermolecular Activity Number** $I_a$ (informally, the *Boredom Constant*) characterises the transition from classical to intermolecularly-influenced continuum flow. It complements the Knudsen number by quantifying energetic significance of molecular interactions rather than collision frequency.

---

## Validation

The formulation is validated against **ten NASA atmospheric entry missions** spanning the solar system:

| Mission | Body | $V_\infty$ [km/s] | $\varepsilon$ [%] |
|---|---|---|---|
| Space Shuttle (STS) | Earth LEO | 7.8 | 0.022 |
| Apollo CM | Earth lunar | 11.0 | 0.152 |
| Stardust SRC | Earth sample | 12.5 | 0.008 |
| MSL / MEDLI | Mars | 5.9 | 0.074 |
| Pioneer Venus | Venus | 11.5 | 0.092 |
| Galileo Probe | Jupiter | 47.4 | **0.467** |
| Cassini (model) | Saturn | 33.0 | 0.120 |
| Huygens Probe | Titan | 6.1 | 0.078 |
| Ice Giants (model) | Uranus | 23.0 | 0.002 |
| Ice Giants (model) | Neptune | 24.0 | 0.010 |

**Mean relative error: 0.102% — Maximum: 0.467% (Galileo Probe, Mach 50)**

All ten cases fall within the excellent band ($\varepsilon < 10\%$) standard in hypersonic aerothermodynamics validation. The Galileo case represents the highest-enthalpy atmospheric entry on record ($V_\infty = 47.4$ km/s, $T_\mathrm{stag} \approx 5 \times 10^4$ K, H₂/He shock layer).

---

## Interactive Tool

`ns_extended.html` runs entirely in the browser — no installation required.

**Open the file in any modern browser.**

Features:
- 10 planetary templates (Earth × 3, Mars, Venus, Jupiter, Saturn, Titan, Uranus, Neptune)
- Live equation routing based on $T_\mathrm{shock}$ (classical NS → Extension → Extension + Dissociation → Extension + Dissociation + Radiation)
- Real-time $I_a$, $f_\mathrm{mix}(T)$, $P_\mathrm{IM}(r,T)$, dissociation $\alpha(T)$, and re-entry trajectory graphs
- Interactive console (⚡ CONSOLE button) with live computation output
- Validation report panel against NASA reference data at every query point
- Dark / light theme toggle

---

## Python Tools (`Aero_Tools.zip`)

Requires Python 3.8+, numpy, matplotlib, scipy.

```bash
pip install numpy matplotlib scipy
```

```bash
# Interactive planet selector:
python ns_extended_main.py

# All planets:
python ns_extended_main.py --all

# Validation suite (reproduces Table 2 of manuscript):
python ns_extended_main.py --validate
```

Generates 10 individual 600 DPI plots per planet saved to `ns_plots_{planet}/`.

---

## Stress Test Sandbox (`Eq_Stress_Test`)

Two scripts testing numerical robustness of $I_a$ under pathological inputs:

**`nuclear_test.py`** — Pathological integral inputs:
- Ramanujan summation $1+2+3+\ldots = -1/12$ as number density
- Riemann zeta at $s=1$ (diverges to infinity)
- $\int_0^\infty e^{x^x}\,dx$ (super-exponential growth)
- Nested factorials, Gamma function explosions, double factorial in cosine
- **Final boss:** all of the above multiplied together

**`chaos_test.py`** — Anti-physical conditions:
- Negative density (anti-universe)
- Imaginary number density (complex plane)
- Supernova conditions ($T \sim 10^{10}$ K, $n \sim 10^{35}$ m⁻³)
- Absolute zero and infinite temperature limits
- Negative temperature (population inversion regime)

**Result:** All inputs survived. The final boss produced $\ln(I_a) \approx 548$, corresponding to $I_a \approx 10^{238}$ — mathematically finite and real. The ratio structure of $I_a$ provides natural regularisation independent of input magnitude.

> These scripts are provided for reviewer scrutiny only. Values are computed within the stated scope of the model and are not representative of physical conditions. Scripts must not be reproduced or repurposed.

---

## Model Scope

| Parameter | Validated range |
|---|---|
| Knudsen number | $\mathrm{Kn} < 10^{-2}$ (continuum) |
| Mach number | $5 \leq M \leq 50$ |
| Freestream temperature | $70$–$300$ K |
| Stagnation temperature | $\leq 5 \times 10^4$ K |
| Composition | N₂/O₂/CO₂/H₂/He/CH₄ |
| Geometry | Blunt-body stagnation point |

**Not modelled:** two-temperature non-equilibrium, ionization, optically-thick radiation, surface catalysis/ablation, three-dimensional effects.

---

## Author Statement

All theoretical development, derivations, and physical reasoning presented in this manuscript are original work by the author. Computational and writing tools were used for implementation and formatting only and did not contribute to the scientific content or results.

---

## License

© Ayush Sreejith. All rights reserved.  
No reproduction, redistribution, derivative work, or formal citation without explicit written permission from the author.

---

## Feedback

Critical technical review is welcome.  
If you find inconsistencies, broken assumptions, or edge-case failures — open an issue or discussion.
