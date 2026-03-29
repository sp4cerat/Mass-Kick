# A Conformal Mass-Kick Sector in CLASS_EDE

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Status: First Implementation](https://img.shields.io/badge/Status-First_Implementation-blue.svg)]()

[span_0](start_span)This repository contains the source code, MCMC configurations, and the accompanying preprint for the paper **"A Conformal Mass-Kick Sector in CLASS_EDE: First Implementation and Exploratory Constraints from Planck, BAO, and SH0ES"**[span_0](end_span).

## Overview

[span_1](start_span)Early Dark Energy (EDE) can ease the Hubble tension but typically leaves the $S_8$ tension unaddressed[span_1](end_span). [span_2](start_span)This repository provides a modified version of the Boltzmann code [`CLASS_EDE`](https://github.com/mwt5345/class_ede)[span_2](end_span) [span_3](start_span)that implements a conformal **Mass-Kick coupling**[span_3](end_span). 

[span_4](start_span)By generating a time-dependent dark matter mass $m^2(\chi) \propto A^2(\chi)$ coupled to a pNGB vacuum field $\chi$, the mechanism suppresses late-time clustering while preserving the EDE resolution of $H_0$[span_4](end_span).

### Key Features of this Mod
[span_5](start_span)[span_6](start_span)We provide three successive implementations of the coupled quintessence formalism in `perturbations.c`[span_5](end_span)[span_6](end_span):
1. **[span_7](start_span)v1 (Friction-only):** Suppresses CDM clustering during the mass-kick transition[span_7](end_span).
2. **[span_8](start_span)v2 (Quasi-static screening):** Includes fifth-force approximations[span_8](end_span).
3. **[span_9](start_span)[span_10](start_span)v3 (Full Jordan-frame):** The complete coupled system including CDM backreaction and a scale-dependent fifth force[span_9](end_span)[span_10](end_span).

*[span_11](start_span)Null-Test:* Setting $\Gamma = 0$ in this modified code perfectly reproduces the standard EDE background and perturbation spectra to numerical precision ($<0.01\%$ deviation in $C_\ell$)[span_11](end_span).

## Exploratory MCMC Results

[span_12](start_span)[span_13](start_span)[span_14](start_span)We performed a 10-parameter MCMC fit (6 $\Lambda$CDM + 3 EDE + $\Gamma$) against Planck 2018 TT+TE+EE+lensing, BAO, and SH0ES using `Cobaya`[span_12](end_span)[span_13](end_span)[span_14](end_span). 

* **[span_15](start_span)[span_16](start_span)Constraint on $\Gamma$:** $\Gamma = 0.062 \pm 0.043$ (95% upper limit $\Gamma < 0.14$)[span_15](end_span)[span_16](end_span).
* **[span_17](start_span)[span_18](start_span)Preference:** The data show a mild preference for $\Gamma > 0$ ($P(\Gamma > 0.01) = 90\%$), but do not strictly require it[span_17](end_span)[span_18](end_span).
* **[span_19](start_span)Clustering Suppression:** The mechanism yields a clean linear scaling of $\Delta\sigma_8/\sigma_8 \approx -40\% \times \Gamma \times f_\varphi$[span_19](end_span).

*Note: The coupled DM fraction $f_\varphi$ is fixed at 0.20 in this exploratory run. [span_20](start_span)[span_21](start_span)Freeing $f_\varphi$ and adding weak-lensing data (DES Y3 / KiDS-1000) are the designated next steps[span_20](end_span)[span_21](end_span).*

## Repository Structure

* [span_22](start_span)[span_23](start_span)`/class_ede_mod/`: Contains the modified `background.c` and `perturbations.c` files[span_22](end_span)[span_23](end_span). 
* [span_24](start_span)`/cobaya_mcmc/`: YAML configuration files and analysis scripts used for the MCMC runs[span_24](end_span).
* [span_25](start_span)`/paper/`: The PDF preprint of the paper detailing the theoretical EFT framework, the implementation, and the falsification matrix[span_25](end_span).

## Installation

1. Clone the original `CLASS_EDE` repository.
2. Replace `source/background.c` and `source/perturbations.c` with the modified files provided in this repository.
3. Compile standardly via `make clean` and `make`.

## Broader EFT Context

[span_26](start_span)The Mass-Kick sector is mathematically designed to be embeddable into a broader two-field Effective Field Theory (EFT)[span_26](end_span). [span_27](start_span)This framework motivates connections to gauge-friction inflation, $\mathrm{U}(1)_{B-L}$ Chern-Simons baryogenesis, and a running vacuum coefficient $\alpha_{\rm eff} \sim 10^{-3}$[span_27](end_span). 

[span_28](start_span)[span_29](start_span)Please note that these early-universe connections are *programmatic*; only the late-time Mass-Kick is quantitatively tested against data in this repository[span_28](end_span)[span_29](end_span).

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

