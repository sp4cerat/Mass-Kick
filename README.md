# Conformal Mass-Kick Sector in CLASS_EDE

**First implementation and exploratory constraints from Planck, BAO, and SH0ES**

Sven Forstmann (Independent Research, Konstanz, Germany)  
📧 info@svenforstmann.com

> **Paper:** [arXiv:XXXX.XXXXX](https://arxiv.org/abs/XXXX.XXXXX)

---

## What This Repository Contains

This repository provides the complete code to reproduce the results in the paper *"A Conformal Mass-Kick Sector in CLASS_EDE: First Implementation and Exploratory Constraints from Planck, BAO, and SH0ES"*.

The conformal Mass-Kick mechanism generates a time-dependent dark matter mass via a conformal coupling to a pNGB vacuum field, suppressing late-time clustering (σ₈) while preserving the EDE resolution of H₀.

### Key Result

```
Γ = 0.062 ± 0.043    P(Γ > 0.01) = 90%    R-1 < 0.10
```

---

## Repository Structure

```
mass-kick-class-ede/
│
├── README.md
├── LICENSE                          # MIT or similar
│
├── paper/
│   ├── v8_eft_paper.tex             # LaTeX source
│   ├── fig1_corner.png              # Posterior corner plot
│   ├── fig2_chains.png              # Chain convergence diagnostic
│   └── fig3_gamma_posterior.png      # Γ posterior distribution
│
├── patch/
│   ├── v8_mass_kick_v2.patch        # Unified diff against CLASS_EDE
│   ├── deploy_v2.sh                 # Automated deployment script
│   └── PATCH_README.md              # How to apply the patch
│
├── class_ede_modified/              # Full modified source files
│   ├── background.c                 # Modified background evolution
│   ├── perturbations.c              # Modified perturbation equations
│   └── background.h                 # Header (if modified)
│
├── mcmc/
│   ├── v8_mcmc_final.yaml           # 6-chain production config
│   ├── v8_mcmc_diag.yaml            # 2-chain diagnostic config
│   └── covmat/                      # Learned covariance matrix
│       └── v8_proposal.covmat
│
├── analysis/
│   ├── make_paper_figures.py        # Generate all 3 paper figures
│   ├── analyze_chains.py            # Chain diagnostics & convergence
│   └── requirements.txt             # Python dependencies
│
├── alpha_eff/
│   ├── alpha_eff_v4.py              # Adiabatic renormalization derivation
│   └── fig_adiabaticity.png         # Adiabaticity parameter plot
│
└── build/
    ├── fix_classy_v5.sh             # Fix CLASS_EDE Cython build (Python 3.12)
    └── BUILD_INSTRUCTIONS.md        # Step-by-step build guide
```

---

## Quick Start

### 1. Apply the Mass-Kick patch to CLASS_EDE

```bash
# Clone CLASS_EDE
git clone https://github.com/mwt5345/class_ede.git
cd class_ede

# Apply the Mass-Kick patch
git apply ../patch/v8_mass_kick_v2.patch

# Build (Python 3.12 requires the Cython fix)
bash ../build/fix_classy_v5.sh
```

### 2. Run a test spectrum

```bash
cd ..
cobaya-run mcmc/v8_mcmc_diag.yaml --test
```

### 3. Reproduce the MCMC fit

```bash
# 6-chain production run (requires ~6 CPU cores, ~8 GB RAM, ~1 week)
mpirun -n 6 cobaya-run mcmc/v8_mcmc_final.yaml
```

### 4. Generate paper figures

```bash
python3 analysis/make_paper_figures.py
```

---

## The Mass-Kick Mechanism

The conformal coupling modifies the CDM energy density:

```
A²(χ) = 1 + (Γ/2) cos(χ/f_χ)
```

This enters CLASS_EDE through:
- **background.c**: Modified CDM background evolution with conformal factor
- **perturbations.c**: Modified CDM perturbation equations (density + velocity + fifth force)

### Parameters

| Parameter | Description | Prior |
|-----------|-------------|-------|
| `Gamma_mk` | Mass-Kick coupling strength | [0, 0.50] |
| `f_phi_mk` | Coupled DM fraction | Fixed at 0.20 |

### Null Test

Setting `Gamma_mk = 0` reproduces standard EDE spectra to < 0.01% in C_ℓ.

---

## Build Notes (Python 3.12 + Cython 3.x)

CLASS_EDE was designed for Python 3.8-3.10. On Python 3.12, the Cython build fails. The fix script `fix_classy_v5.sh` handles:

1. Downgrade Cython to < 3.0
2. Fix `np.int_t` → `np.int64_t`
3. Add `# cython: language_level=3`
4. Fix Python 2 dict methods (`.iteritems()` etc.)
5. Insert `#undef I` between NumPy and CLASS headers
6. Direct gcc compilation of the `.pyx` → `.c` → `.so`

---

## Citation

```bibtex
@article{Forstmann2026,
  author  = {Forstmann, Sven},
  title   = {A Conformal Mass-Kick Sector in {CLASS\_EDE}: 
             First Implementation and Exploratory Constraints 
             from {Planck}, {BAO}, and {SH0ES}},
  year    = {2026},
  eprint  = {XXXX.XXXXX},
  archivePrefix = {arXiv},
  primaryClass  = {astro-ph.CO}
}
```

---

## License

MIT License. The modified CLASS_EDE files inherit the CLASS license (GPL v3).
