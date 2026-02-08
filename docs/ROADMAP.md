# Technical Roadmap: Income Prediction Refactoring

## Tech Stack

| Category | Tool | Purpose | Phase |
| --- | --- | --- | --- |
| **Environment** | `uv` | High-performance package & project management | Phase 1 |
| **Quality** | `Ruff` | Ultra-fast Linting and Formating | Phase 1 |
| **Quality** | `MyPy` | Static Type Checking | Phase 1 |
| **Data Analysis** | `Pandas`, `NumPy` | Data manipulation and numerical computing | Core |
| **Machine Learning** | `Scikit-Learn` | Core ML algorithms and pipelines | Core |
| **Boosting Models** | `XGBoost`, `LightGBM`, `CatBoost` | High-performance gradient boosting | Core |
| **Visualization** | `Matplotlib`, `Seaborn` | Data visualization and EDA | Core |
| **Validation** | `Pydantic` | Data Contract Validation | Phase 2 |
| **ML Lifecycle** | `MLflow` | Experiment Tracking & Model Registry | Phase 3 |
| **Data Versioning** | `DVC` | Data & Artifact Versioning | Phase 3 |
| **Testing** | `Pytest` | Unit and Integration Testing | Phase 2 |
| **CI/CD** | `GitHub Actions` | Automated Quality Gates | Phase 4 |

## Phase 1: Foundation & Modern Tooling
**Goal:** Establish a professional development environment and clean up the codebase.
### Requirements
* Migrate from `requirements.txt` to `uv` and `pyproject.toml`.
* Configure `Ruff` and `MyPy` for strict code quality.
* Initial refactor of `src/` to include type hints.

## Phase 2: Industrialized Pipeline (OOP)
**Goal:** Transform scripts into a robust, object-oriented ML pipeline.
### Requirements
* Implement `DataIngestor` with Pydantic schemas.
* Implement `FeaturePipeline` using Scikit-Learn `Pipeline` and `ColumnTransformer`.
* Create unit tests for data transformations.

## Phase 3: MLOps & Observability
**Goal:** Implement experiment tracking and data versioning.
### Requirements
* Integrate `MLflow` for tracking hyperparameters and metrics.
* Setup `DVC` for managing data artifacts.
* Implement a `ModelTrainer` class that logs to MLflow.

## Phase 4: Deployment & Automation
**Goal:** Prepare the system for production-ready delivery.
### Requirements
* Dockerize the training and inference environment.
* Setup GitHub Actions for automated testing and linting.
* Final documentation and "Recruiter-Ready" README update.
