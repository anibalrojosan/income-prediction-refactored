# Income Prediction: From Monolithic Notebooks to Production-Grade Engineering

[![Python Version](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/)
[![Software Engineering](https://img.shields.io/badge/Engineering-Refactored-green.svg)](#)

This project aims to apply the best practices of software engineering to a data science income prediction project.MW

## 📋 Table of Contents
- [🎯 Project purpose](#project-purpose)
- [🛠️️ The Challenge: From chaos to order](#the-challenge-from-chaos-to-order)
- [🏗️ Modular Architecture](#modular-architecture)
- [📊 Research vs. Production](#research-vs-production-the-value-of-refactoring)
- [📂 Project Structure](#project-structure)
- [⚙️ How to Run](#how-to-run)
- [📓 Notebooks Overview](#notebooks-overview)
- [💎 Software Engineering Best Practices Applied](#software-engineering-best-practices-applied)
- [🚀 Future-Proofing & Tech Stack](#future-proofing--tech-stack)

## Project purpose
**This is not just another income prediction model.** While the core task is classifying income levels using the "Adult" dataset, this project serves as a **technical chronicle of refactoring**. 

It demonstrates the transition from messy, exploratory research to a modular, maintainable, and scalable Python ecosystem.

## The Challenge: From chaos to order

Most Data Science projects start (and unfortunately end) in a single, monolithic Jupyter Notebook. This leads to several "Engineering Debts" that this project specifically addresses:

*   **The "Spaghetti" Logic:** Global variables and tightly coupled code that make testing impossible.
*   **The "Copy-Paste" Trap:** Feature engineering logic duplicated across multiple notebooks, leading to training-serving skew.
*   **Manual Execution:** Heavy reliance on running cells in a specific order without a clear data pipeline.
*   **Lack of Persistence:** Models and artifacts living only in memory rather than being treated as versioned software assets.

**The Goal:** Transform a research-heavy workflow into a system where the exploration code is identical to the production logic by abstracting core functionality into a dedicated `src/` package.

## Modular Architecture

To solve the challenge, the project was re-engineered into a decoupled structure. The notebooks now act as thin "analysis layers" that import heavy-lifting logic from the core library.

![New Architecture](docs/new_arquitecture.png)

## Research vs. Production: The Value of Refactoring

| Feature | Monolithic Notebooks (Research) | Modular Ecosystem (Production) |
| :--- | :--- | :--- |
| **Code Reuse** | Copy-pasting cells between files. | Centralized logic in `src/` imported by any client. |
| **Testing** | Manual visual inspection of cell outputs. | Ready for automated Unit Testing with `pytest`. |
| **Scalability** | Hard to maintain as the project grows. | Decoupled components allow independent scaling. |
| **Reproducibility** | "Run all" and pray for no hidden state. | Managed dependencies and deterministic scripts. |
| **Deployment** | Requires manual cleanup of research code. | `src/` logic is ready to be wrapped in an API/Docker. |

## Project Structure

The repository is organized using a standard data science project structure to ensure modularity and reproducibility.

```text
income-prediction-refactored/
├── data/               # 📊 Dataset storage (raw & processed)
├── models/             # 🧠 Trained model artifacts (joblib)
├── notebooks/          # 📓 EDA and experimentation
├── reports/            # 📈 Generated metrics and figures
├── src/                # 🛠️ Source code (Production Core)
│   ├── data/           # 📥 Data ingestion scripts
│   ├── features/       # 🧪 Feature engineering logic
│   ├── models/         # 🚂 Training and inference logic
│   └── visualization/  # 🖼️ Reusable plotting functions
├── requirements.txt    # 📦 Dependency management
└── README.md           # 📖 Project documentation
```

## How to Run

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/anibalrojosan/income-prediction-refactored
    cd income-prediction-refactored
    ```

2.  **Set up a virtual environment:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Run the notebooks:**
    It is crucial to run the notebooks in order, as they depend on each other.
    
    -   **Start with `0.1-eda-and-data-cleaning.ipynb`**. This notebook must be run first to generate the `adult_cleaned.csv` file in the `data/processed` directory, which is required by all other notebooks.
    -   Afterward, you can run the other notebooks (`1.0`, `2.0`, and `3.0`) in any order to explore the different analyses.

## Notebooks Overview

The analysis is structured as a sequential pipeline. Each notebook represents a critical stage in the machine learning lifecycle, from data sanitization to advanced model interpretability.

### Phase 1: Data Foundation
*   **`0.1-eda-and-data-cleaning.ipynb`**
    *   **Goal:** Establish a robust data baseline through exhaustive exploration and sanitization.
    *   **Technical Discussion (Logic):** Beyond simple cleaning, this stage involves a deep dive into feature distributions and correlations. We handle missing values using context-aware strategies and perform categorical encoding designed to minimize dimensionality explosion. The logic focuses on ensuring that the "garbage in, garbage out" principle is mitigated from the start.
    *   **Output:** 💾 `data/processed/adult_cleaned.csv`

### Phase 2: Modeling & Experimentation
*   **`1.0-baseline-model-comparison.ipynb`**
    *   **Goal:** Define the "minimum viable performance" using standard algorithms.
    *   **Technical Discussion (Logic):** We contrast a regularized linear approach (`ElasticNet`) against a non-linear ensemble (`RandomForest`). The choice of `ElasticNet` over standard `LinearRegression` is intentional: it allows us to evaluate the impact of both L1 and L2 penalties simultaneously, providing a more resilient baseline against potential multi-collinearity in the Adult dataset.
    *   **Output:** 🧠 `models/baseline_model.joblib`

*   **`2.0-boosting-ensemble-analysis.ipynb`**
    *   **Goal:** Maximize predictive power through Gradient Boosting architectures.
    *   **Technical Discussion (Logic):** This is a high-stakes comparison between the industry's "Big Four": `AdaBoost`, `XGBoost`, `LightGBM`, and `CatBoost`. The logic centers on hyperparameter optimization and cross-validation to identify the best trade-off between bias and variance. We specifically monitor `ROC-AUC` to ensure the model maintains high discriminative power across imbalanced income classes.
    *   **Output:** 🏆 `models/best_performing_model.joblib`

### Phase 3: Interpretability & Theory
*   **`3.0-regularized-regression-analysis.ipynb`**
    *   **Goal:** Deconstruct model behavior through the lens of regularization.
    *   **Technical Discussion (Logic):** By treating the classification task as a regression problem for analytical purposes, we visualize how L1 (Lasso) and L2 (Ridge) penalties "squeeze" coefficients. This provides a theoretical validation of feature importance: which variables are truly robust and which are noise. It’s a bridge between "black-box" prediction and transparent engineering.
    *   **Focus:** Theoretical validation and feature selection insights.

## Software Engineering Best Practices Applied

This project implements industry-standard practices to bridge the gap between experimental Data Science and Production Engineering:

*   **Modular "Library-First" Architecture:** Core logic is abstracted into a standalone `src/` package. This ensures that the same code used for training in notebooks is the exact same code used for inference in production, eliminating "training-serving skew".
*   **Separation of Concerns (SoC):** Distinct layers for Data Ingestion, Feature Engineering, and Model Evaluation. This decoupling allows for independent testing and scaling of each component.
*   **Defensive Programming & DRY:** Implementation of reusable functions with clear input/output definitions, reducing code duplication compared to the original monolithic notebooks.
*   **Artifact Versioning:** Models are not just "saved"; they are treated as versioned software assets in the `models/` directory, ready for programmatic loading and deployment.
*   **Environment Determinism:** Use of strict dependency management via `requirements.txt` to ensure 100% reproducibility across different development and execution environments.

## Future-Proofing & Tech Stack

<details>
<summary>🔮 Future Improvements</summary>

To evolve this project into a full-scale MLOps pipeline, the following milestones are planned:

### 🛠️ Quality & Validation
*   **Unit Testing Suite:** Implement `pytest` for the `src/` layer to ensure 100% coverage of critical data transformations.
*   **Data Contract Validation:** Integrate `Pydantic` to enforce strict schemas on input data, preventing silent failures in production.

### 🚀 Automation & DevOps
*   **CI/CD Pipeline:** GitHub Actions to automate linting, testing, and model performance auditing on every push.
*   **Containerization:** Dockerize the training and inference environments to ensure "Write Once, Run Anywhere" portability.

### 📈 Orchestration
*   **Makefile Automation:** Standardize the workflow with a `Makefile` (e.g., `make data`, `make train`, `make test`) to simplify the developer experience and onboarding.
</details>

<details>
<summary>🛠️ Tech Stack</summary>

*   **Data Science & ML Stack:** `Python` , `Pandas` , `Scikit-Learn` , `XGBoost` , `LightGBM` , `CatBoost`, `Joblib`.
*   **Modern Tooling:** `pip` (Manager), `requirements.txt`.
*   **Infrastructure (Planned):** `Docker` , `GitHub Actions`.
</details>


> This project was developed with ❤️ by [Anibal Rojo](https://github.com/anibalrojosan).