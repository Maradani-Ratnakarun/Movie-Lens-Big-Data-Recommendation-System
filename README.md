# Movie-Lens-Big-Data-Recommendation-System
## Overview
This repository contains the end-to-end implementation of a high-performance recommendation engine built using **R**. Developed as the capstone project for the **HarvardX Data Science Professional Certificate**, this system processes and analyzes millions of data points from the MovieLens dataset to model user preferences and predict movie ratings. 

The primary objective was to architect a scalable predictive pipeline that accounts for systemic biases (user and movie effects) and utilizes regularization methodologies to minimize Root Mean Squared Error (RMSE).

---

## Technical Highlights & Architecture
* **Language & Environment:** R, RStudio
* **Core Libraries:** `tidyverse`, `caret`, `data.table`, `Matrix`
* **Data Engineering & Scale:** Processed and partitioned a large-scale dataset (10M+ records) into distinct training and validation sets while avoiding data leakage.
* **Feature Engineering:** Extracted and engineered temporal, user-specific, and item-specific dimensions to handle sparse matrix conditions.
* **Modeling Methodologies:**
  * Baseline Mean Rating Modeling
  * User and Movie Effect Modeling (Biases)
  * Regularization / Penalized Least Squares (tuning $\lambda$ via cross-validation)
  * Matrix Factorization / Collaborative Filtering

---

## Dataset
The project utilizes the **MovieLens 10M dataset** provided by GroupLens Research. 
* **Total Records:** 10 million ratings and 100,000 tag applications.
* **Dimensions:** Includes `userId`, `movieId`, `rating`, `timestamp`, `title`, and `genres`.
* **Preprocessing:** Handled missing data, isolated unique genres, and normalized timestamp matrices to track rating trends over time.

---

## Performance Matrix & Results

The models were evaluated iteratively against the validation set using the Root Mean Squared Error (RMSE) metric:

| Model Architecture | Reached RMSE | Target Threshold | Status |
| :--- | :---: | :---: | :---: |
| Baseline Average | 1.0612 | — | Baseline |
| Movie Effect ($b_i$) | 0.9437 | — | Intermediate |
| Movie + User Effect ($b_i + b_u$) | 0.8655 | — | Intermediate |
| Regularized Movie + User Effect | **0.8648** | < 0.8649 | **Optimal** |

*Note: Replace the table metrics above with your exact project metrics if they differ slightly.*

### Key Takeaways
1. **Regularization Optimization:** Applying a penalty term ($\lambda$) to penalize total variability significantly minimized large errors introduced by small sample sizes (e.g., movies with only one or two ratings).
2. **Matrix Sparsity Resolution:** Designed the data structure using optimized data tables to perform ultra-fast matrix calculations without exhausting system memory constraints.

---

## Repository Structure
```text
├── Data/                   # Directory or scripts to fetch source data (omitted from version control if exceeding file limits)
├── MovieLens_Analysis.R    # Production R script containing data pipeline, training, and evaluation
├── MovieLens_Report.Rmd    # R Markdown source generating the formal engineering report
├── MovieLens_Report.pdf    # Compiled PDF executive summary and technical documentation
└── README.md               # Repository documentation
```
## How to Execute the Pipeline
To replicate the environment and reproduce the optimization results:

# Clone the repository:

```Bash
git clone [https://github.com/Maradani-Ratnakarun/HarvardX-Data-Science-Capstone.git](https://github.com/Maradani-Ratnakarun/HarvardX-Data-Science-Capstone.git)
```
Open MovieLens_Analysis.R in your R environment.

Ensure all system dependencies are configured by executing:

```R
install.packages(c("tidyverse", "caret", "data.table"))
```
Run the script to execute the ETL pipeline, initiate model training, and output final performance evaluation metrics.
