# Repository Guidelines

## Project Structure & Module Organization

This repository is a Jupyter notebook project. `my-uts.ipynb` contains the analysis, visualizations, preprocessing experiments, and model comparisons for airline passenger satisfaction. The `dataset/` directory contains the CSV input and archive; it is ignored by Git, so obtain the expected data locally before running the notebook. `environment-full.yml` and `conda-lock.yml` describe the Conda environment. There is no separate source or test directory.

## Build, Test, and Development Commands

Create and activate the project environment with Conda:

```bash
conda env create -f environment-full.yml
conda activate jlab
jupyter lab
```

Open `my-uts.ipynb` from the repository root and run cells in order. The notebook reads `dataset/airline_passenger_satisfaction.csv` using a relative path. No build or automated test command is configured.

## Coding Style & Naming Conventions

Keep notebook sections organized with Markdown headings and short, focused code cells. Use Python conventions: four-space indentation, `snake_case` for variables and functions, and descriptive names. Preserve the notebook's existing Indonesian prose unless a change requires consistency across a section. Prefer reproducible operations and explicit random seeds in data splits and models. Avoid committing machine-specific paths or environment secrets.

## Testing Guidelines

There is no standalone test suite or coverage requirement. For analysis changes, restart the kernel and run all cells from top to bottom; confirm expected plots, tables, and model metrics are produced. Check that data paths resolve from the repository root and that preprocessing does not leak test data into training.

## Commit & Pull Request Guidelines

The existing Git history uses short, informal messages (for example, `soal 5` and `initial commit`); no stricter convention is established. Use a concise imperative commit subject that describes the change. Pull requests should summarize the analysis or notebook changes, mention relevant dataset or environment assumptions, and include screenshots when plot or output changes are central to review. Clear stale cell outputs when they are unrelated or excessively large.

## Data and Generated Files

`dataset/` is intentionally excluded by `.gitignore`; do not force-add private or bulky source data. Keep environment files intentional and reproducible, and avoid adding generated checkpoints or temporary exports unless the change requires them.
