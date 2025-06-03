# 🧩 Latent-Variable Model for Generating High-Fidelity Synthetic CPRD Data  
*Supplementary code & evaluation workflow*

This folder accompanies the study **“Generating High-Fidelity Synthetic Patient Data for Assessing Machine Learning Healthcare Software”** (*npj Digital Medicine* 13, 2020).  

The scripts recreate the end-to-end pipeline:

1. **🎯 Learn a Bayesian network with latent variables** from UK primary-care records  
2. **👥 Sample synthetic patients** whose statistics and downstream ML behaviour match the ground truth  
3. **📏 Quantify fidelity and privacy** through a battery of statistical tests  

Read the open-access article for full methodological detail:  
<https://www.nature.com/articles/s41746-020-00353-9>

---

## 🏃‍♀️ Quick-start

```bash
# R ≥ 4.1 — install dependencies
install.packages(c(
  "bnlearn","pcalg","missForest","Rgraphviz","gRain",
  "LaplacesDemon","cluster","arules","ggplot2","gridExtra",
  "RevoScaleR","summarytools","kernlab","dplyr",
  "SuperLearner","precrec","lmtest"
))

# Generate 10 batches of synthetic data (≈ 100 k patients each)
Rscript latentModel.R

# Reproduce all figures & tables from the paper
Rscript tables_figures.R
````

---

## 📦 Prerequisite R packages

**Minimum R version:** 4.1

### Core packages

| Package         | Purpose                                        |
| --------------- | ---------------------------------------------- |
| `bnlearn`       | Bayesian-network learning & sampling           |
| `pcalg`         | RFCI causal-discovery algorithm                |
| `missForest`    | Random-forest imputation of missing data       |
| `Rgraphviz`     | Graph visualisation                            |
| `gRain`         | Probabilistic inference in graphical models    |
| `LaplacesDemon` | Kullback–Leibler divergence utilities          |
| `cluster`       | *k*-means clustering for latent initialisation |
| `arules`        | Equal-interval discretisation helper           |
| `ggplot2`       | Plotting                                       |
| `gridExtra`     | Plot arrangement                               |

### Evaluation-only packages

| Package        | Purpose                               |
| -------------- | ------------------------------------- |
| `RevoScaleR`\* | Efficient handling of large TXT files |
| `summarytools` | Compact descriptive-statistics tables |
| `kernlab`      | Kernel MMD calculation                |
| `dplyr`        | Tidy data manipulation                |
| `SuperLearner` | Ensemble classifier framework         |
| `precrec`      | ROC & PR-curve metrics                |
| `lmtest`       | Granger causality tests               |

\*If `RevoScaleR` (part of Microsoft R) is unavailable, replace its I/O calls with `readr::read_delim()` or `data.table::fread()`.

---

## 🔄 Pipeline in a nutshell

1. **Data preparation** – discretise continuous attributes, impute missing values with random-forest (`missForest`) and convert factors to integer levels
2. **Structure discovery** – learn Partial Ancestral Graphs on 10 bootstrap samples via RFCI (α = 0.9), inject six latent variables where edges suggest unobserved common causes, then refine with Structural EM (hill-climbing, 5 iterations)
3. **Synthetic generation** – sample the fitted conditional Gaussian BN to create patient-like records, then coerce values to clinically plausible ranges
4. **Validation** – `tables_figures.R` verifies that synthetic distributions, multi-way interactions and ML performance remain indistinguishable from the real data while maintaining low re-identification risk

---

## 📄 Files

| File                   | Role                                               | Key steps                                                                                                                                                                 |
| ---------------------- | -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`latentModel.R`**    | Learn the causal graph and generate synthetic data | • RFCI bootstrap to flag hidden confounders<br>• Structural EM with six hand-seeded latent nodes<br>• `bnlearn::rbn` sampling and biological-sanity filters               |
| **`tables_figures.R`** | Replicate the paper’s evaluation suite             | • Marginal & joint distribution tests (χ², KS, KLD, MMD)<br>• Ten-fold KL-divergence benchmark<br>• Stroke-risk classifier transfer (ROC / PR curves, AUC, Granger tests) |

### 🗄️ Data paths

| Variable                  | Purpose                                    | Example                |
| ------------------------- | ------------------------------------------ | ---------------------- |
| `G:/cvdgt.txt`            | CPRD “ground-truth” cohort (de-identified) | `/data/cprd/cvdgt.txt` |
| `A:/Wangz/R Scripts/Ntr/` | Output directory for synthetic batches     | `latent_model/output/` |

---

## 📚 Citation

> Tucker A, Wang Z, Rotalinti Y, Myles P. **Generating High-Fidelity Synthetic Patient Data for Assessing Machine Learning Healthcare Software.** *npj Digital Medicine* 13 (2020). [https://doi.org/10.1038/s41746-020-00353-9](https://doi.org/10.1038/s41746-020-00353-9)

Please cite the paper when using this code or synthetic data in academic or commercial work.

---

## 📝 Licence & ethics

The scripts are released under the **MIT Licence**.
Synthetic datasets produced by the pipeline **do not contain real patient records**; nevertheless, evaluate privacy risk before public release and comply with local governance frameworks.

---

## 🤝 Support

Raise issues or pull requests in the main repository. Contributions that improve portability, speed or documentation are welcome.
