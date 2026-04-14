# Code Refactoring Report: Fake News ML Project
So basically I inherited all your logic but:
## 1. Global Architecture & Dependency Management
* **Previous State:** Libraries were loaded via multiple `library()` calls scattered throughout the script, risking missing dependencies and execution failures.
* **Refactored State:** I implemented a new architecture. All dependencies are now loaded globally via a single `pacman::p_load()` call in the setup chunk. This ensures strict computational reproducibility and a clean global environment before any data is processed, and I think the adcom will value a potential PhD student with great meticulousness in organizing workspace.

## 2. Reproducible Pathing
* **Previous State:** Data was imported using a local, absolute path (`/Users/ldhuyjoseph/...`), which breaks the execution pipeline when the code is run on another machine or evaluated by external researchers.
* **Refactored State:** I changed it to relative pathing (`data/fakenewsdata.csv`), allowing the replication package to run across different local computers.

## 3. Dynamic Data Subsetting (Eliminating Magic Numbers)
* **Previous State:** Estimation samples were constructed by dropping hardcoded column indices (e.g., `subset[,c(-2,-3,-4,-5)]`). This approach is brittle and highly prone to silent data leakage if the underlying dataframe structure shifts.
* **Refactored State:** I substituted the part that you described how you construct the subsetting algorithm with a description of a new functional subsetting helper (`prep_data()`). It dynamically constructs the estimation sample by selecting covariates by name and performing localized listwise deletion (`drop_na()`) strictly for the active variables, preventing errors (especially when it comes to a new dataset) and maximizing the retained sample size.

## 4. DRY (Don't Repeat Yourself) Principle via Functional Mapping
* **Previous State:** Model fitting and standard error calculations were copy-pasted repetitively for all five dependent variables, leading to a bloated codebase.
* **Refactored State:** I used `lapply()` to programmatically map model specifications (SLR, MLR, Post-LASSO, DoubleML) across the vector of outcomes. This reduced the script's footprint by over 100 lines (yeah it was so messy), making the methodology easier to audit and scale.

## 5. Centralized Robust Standard Errors
* **Previous State:** `vcovHC` matrix extraction was repeated manually within individual model summaries.
* **Refactored State:** I did abstract the heteroskedasticity-consistent standard error (HC1) calculation into a globally defined helper function (`get_robust_se()`), ensuring mathematical precision and consistency across all OLS estimations (again just helping you to keep the code neat and clean)

## 6. Modernized Visualization Pipeline
* **Previous State:** Relied on redundant `ggplot` blocks and the soft-deprecated `aes_string()` function.
* **Refactored State:** So basically just changed the old function to the new one and if the plots are rendered it will still look the same as the one you rendered. I replaced deprecated syntax with modern tidy evaluation (`.data[[]]`) and wrapped the visualization generation into programmatic loops (`create_bar_plots`), culminating in an automated `ggarrange` grid output.