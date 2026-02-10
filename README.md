# MIPLIB-NL

This repository contains a dataset of large-scale optimization problems derived and reverse-engineered from the **MIPLIB 2017** collection. The dataset is designed to support research in operations research and machine learning for optimization, featuring a unique **Problem-Data Separation** format.

Each problem instance is presented with a natural language description, a structured mathematical model, and raw data files, separating the problem logic from the specific instance data.

*Note: This dataset is currently a preview version, so only the `instance.json` file is displayed in the repository.*

## Repository Structure

The core content is located in the `dataset/` directory. Each subdirectory within `dataset/` represents a distinct optimization problem and contains the following files:

```text
dataset/
├── <problem_name>/          # E.g., air03, 30n20b8
│   ├── data/                # Directory containing data files (CSVs)
│   ├── instance.json        # Metadata, problem description, and file schemas
│   ├── model.md             # Mathematical formulation (LaTeX/Markdown)
│   └── solve.py             # Reference Python script to solve the instance (e.g., using Gurobi)
```

### File Descriptions

*   **`data/`**: detailed data files required to instantiate the problem. These are typically CSV files referenced by `instance.json`.
*   **`instance.json`**: The central metadata file for the problem. It contains the natural language description, parameters, and specifications for input data files.
*   **`model.md`**: A formal mathematical description of the problem, including sets, parameters, decision variables, constraints, and the objective function.
*   **`solve.py`**: An executable Python script that demonstrates how to read the `instance.json`, load the data from `data/`, and solve the optimization model using a solver (typically Gurobi).

## `instance.json` Structure

The `instance.json` file serves as the standard definition for each problem. Its fields are defined as follows:

*   **`abstract_problem`**: A comprehensive natural language string describing the background, logic, constraints, and objective of the optimization problem.
*   **`parameters`**: A dictionary of key numerical values defining the scale of the problem (e.g., `{ "n": 100, "m": 50 }`).
*   **`files`**: A dictionary where each key represents a specific data component (e.g., cost inputs, constraint matrices). Each entry contains:
    *   `path`: The relative path to the corresponding file in the `data/` directory.
    *   `description`: A textual description of the file's purpose, including the expected columns and data format.
*   **`optimal_value`**: The objective value of the known best solution for this specific instance.
