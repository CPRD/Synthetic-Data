
# 🧬 Synthetic Data – Open Repository  
Unlocking secure, shareable 💾 health-care datasets for research 🚀 and innovation
-------------------------------------------------------------------------------

This repository contains **reproducible pipelines** that convert sensitive
clinical records into *statistically faithful yet privacy-preserving* synthetic
data. All code is released under the MIT licence so that hospitals, researchers
and companies can audit, adapt 🔧 and extend each component.

---

## ❓ Why synthetic data?

* **⚡ Accelerate research** – remove lengthy approval queues for real-world
  electronic health records.  
* **🛡️ Protect patients** – minimise re-identification risk while retaining the
  signals clinicians and data-scientists need.  
* **📊 Benchmark fairly** – test machine-learning models on *public* replicas of
  private datasets, enabling open comparison and peer review.

---

## 📂 Current structure

| Folder | Brief description | Key outputs |
|--------|-------------------|-------------|
| **`latent_model/`** | Bayesian-network generator with latent-variable discovery (see accompanying [README](latent_model/README.md)). Implements the method from *npj Digital Medicine* 2020 and provides statistical validation scripts. | • Synthetic CPRD-style patient cohorts<br>• Figures & tables reproducing the paper |

> *✨ More components will land here during the grant period (e.g. time-series
> models 🕒, attack-surface evaluators 🔍, differential-privacy wrappers 🔒).  
> Feel free to watch the repo or raise feature requests.*

---

## 🏃‍♂️ Quick start

```bash
git clone https://github.com/<ORG>/Synthetic-Data.git
cd Synthetic-Data

# Each sub-module documents its own dependencies and usage:
cd latent_model
Rscript latentModel.R        # build synthetic patients
Rscript tables_figures.R     # reproduce paper results
````

---

## 🤝 Contributing

1. Fork the repository and create a feature branch 🌱.
2. Follow the code-style and linting guidelines in each folder 📝.
3. Open a pull request – include tests or example notebooks where possible ✅.

All discussions take place in the *Issues* 💬 tab; please search for existing
tickets before opening a new one.

---

## 📚 Citation

If you use any part of this repository, cite the relevant study:

> Tucker A, Wang Z, Rotalinti Y, Myles P.
> **Generating High-Fidelity Synthetic Patient Data for Assessing Machine
> Learning Healthcare Software.** *npj Digital Medicine* 13 (2020).
> [https://doi.org/10.1038/s41746-020-00353-9](https://doi.org/10.1038/s41746-020-00353-9)

---

## 📝 Licence

This project is licensed under the **MIT Licence**.
Synthetic datasets generated with these tools do **not** contain real patient
records, but please review local governance requirements before public release.


