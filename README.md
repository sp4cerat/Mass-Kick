# A Conformal Mass-Kick Sector in CLASS_EDE

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Status: First Implementation](https://img.shields.io/badge/Status-First_Implementation-blue.svg)]()

This repository contains the source code, MCMC configurations, and the accompanying preprint for the paper **"A Conformal Mass-Kick Sector in CLASS_EDE: First Implementation and Exploratory Constraints from Planck, BAO, and SH0ES"**.

## Overview

Early Dark Energy (EDE) can ease the Hubble tension but typically leaves the $S_8$ tension unaddressed. This repository provides a modified version of the Boltzmann code [`CLASS_EDE`](https://github.com/mwt5345/class_ede) that implements a conformal **Mass-Kick coupling**. 

By generating a time-dependent dark matter mass $m^2(\chi) \propto A^2(\chi)$ coupled to a pNGB vacuum field $\chi$, the mechanism suppresses late-time clustering while preserving the EDE resolution of $H_0$.

### Key Features of this Mod
We provide three successive implementations of the coupled quintessence formalism in `perturbations.c`:
1. **v1 (Friction-only):** Suppresses CDM clustering during the mass-kick transition.
2. **v2 (Quasi-static screening):** Includes fifth-force approximations.
3. **v3 (Full Jordan-frame):** The complete coupled system including CDM backreaction and a scale-dependent fifth force.

*Null-Test:* Setting $\Gamma = 0$ in this modified code perfectly reproduces the standard EDE background and perturbation spectra to numerical precision ($\lt 0.01\%$ deviation in $C_\ell$).

## Exploratory MCMC Results

We performed a 10-parameter MCMC fit (6 $\Lambda$CDM + 3 EDE + $\Gamma$) against Planck 2018 TT+TE+EE+lensing, BAO, and SH0ES using `Cobaya`. 

* **Constraint on $\Gamma$:** $\Gamma = 0.062 \pm 0.043$ (95% upper limit $\Gamma \lt 0.14$).
* **Preference:** The data show a mild preference for $\Gamma \gt 0$ ($P(\Gamma \gt 0.01) = 90\%$), but do not strictly require it.
* **Clustering Suppression:** The mechanism yields a clean linear scaling of $\Delta\sigma_8/\sigma_8 \approx -40\% \times \Gamma \times f_\varphi$.

*Note: The coupled DM fraction $f_\varphi$ is fixed at 0.20 in this exploratory run. Freeing $f_\varphi$ and adding weak-lensing data (DES Y3 / KiDS-1000) are the designated next steps.*

## Repository Structure

* `/class_ede_mod/`: Contains the modified `background.c` and `perturbations.c` files. 
* `/cobaya_mcmc/`: YAML configuration files and analysis scripts used for the MCMC runs.
* `/paper/`: The PDF preprint of the paper detailing the theoretical EFT framework, the implementation, and the falsification matrix.

## Installation

1. Clone the original `CLASS_EDE` repository.
2. Replace `source/background.c` and `source/perturbations.c` with the modified files provided in this repository.
3. Compile standardly via `make clean` and `make`.

## Broader EFT Context

The Mass-Kick sector is mathematically designed to be embeddable into a broader two-field Effective Field Theory (EFT). This framework motivates connections to gauge-friction inflation, $\mathrm{U}(1)_{B-L}$ Chern-Simons baryogenesis, and a running vacuum coefficient $\alpha_{\mathrm{eff}} \sim 10^{-3}$. 

Please note that these early-universe connections are *programmatic*; only the late-time Mass-Kick is quantitatively tested against data in this repository.

## Citation

If you use this code or build upon the Mass-Kick implementation, please cite this repository and the included preprint:

```bibtex
@misc{forstmann2026masskick,
  author = {Forstmann, Sven},
  title = {A Conformal Mass-Kick Sector in CLASS_EDE: First Implementation and Exploratory Constraints},
  year = {2026},
  publisher = {GitHub},
  howpublished = {\url{[https://github.com/YOUR_USERNAME/YOUR_REPO_NAME](https://github.com/YOUR_USERNAME/YOUR_REPO_NAME)}}
}
