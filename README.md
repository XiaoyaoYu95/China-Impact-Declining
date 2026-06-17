# China International Citation Ratio

This repository contains a notebook-oriented reproduction package for the paper **The statistical penalty of scientific hypergrowth: Why China's international citation ratio is low and declining**.

## Repository Layout

- `notebooks/0_data_processing.ipynb`: OpenAlex snapshot flattening, citation matrix construction, paper properties, ISSN matching, Web of Science journal filtering, and SJR quartile assignment.
- `notebooks/1_compute_core_data_products.ipynb`: core result tables for international citation ratio `f`, domestic preference `Delta_i`, international preference `Delta_{j,i}`, publication quantities, and reference-list quantities.
- `notebooks/2_neutralization_and_perturbation.ipynb`: citation-preference neutralization plus China/India publication perturbation procedures.
- `notebooks/3_plot_paper_figures.ipynb`: consolidated plotting entry point for manuscript and supplementary figures.
- `code/`: archived copy of the original scripts, unchanged.
- `data/`: expected local inputs and generated pickles. Large data are not included.
- `outputs/results/`: generated tabular intermediate outputs.
- `outputs/figures/`: generated figures.

## Data

Place raw data in these locations before running the notebooks:

- `data/Openalex_2025/snapshot/`: OpenAlex snapshot. OpenAlex documents public snapshot downloads and gives an anonymous AWS CLI sync command for the snapshot. See [OpenAlex data downloads](https://developers.openalex.org/download/overview) and [download instructions](https://developers.openalex.org/download/download-to-machine).
- `data/scimagojr/scimagojr_YYYY.csv`: SCImago Journal Rank yearly CSV files for 1999-2025. See [SJR journal rankings](https://www.scimagojr.com/journalrank.php).
- `data/wos_core_collection/`: Web of Science Master Journal List collection CSVs named exactly as used by the notebook: `Science Citation Index Expanded (SCIE).csv`, `Social Sciences Citation Index (SSCI).csv`, `Arts & Humanities Citation Index (AHCI).csv`, and `Emerging Sources Citation Index (ESCI).csv`. See Clarivate [Collection List Downloads](https://mjl.clarivate.com/collection-list-downloads).

## Running Order

1. Run `notebooks/0_data_processing.ipynb` to create CSV extracts and pickles under `data/Openalex_2025/`.
2. Run `notebooks/1_compute_core_data_products.ipynb` to create core result folders under `outputs/results/`.
3. Run `notebooks/2_neutralization_and_perturbation.ipynb` for neutralization and perturbation results. Expensive bootstrap calls are present but commented by default.
4. Run `notebooks/3_plot_paper_figures.ipynb` after all required result tables exist.

The repository is intended as reproducible code, not as a precomputed data release. The original task explicitly avoids running the full data processing and plotting pipeline during repository assembly.

## System and software requirements

The project was created and executed on the the High Performance Computing Center from Southwest University and New York University Abu Dhabi. The code in this repo can run on any commercial laptop with Python 3 installed.


Python libraries:

- pandas 2.2.2
- numpy 1.26.4
- scipy 1.13.1
- seaborn 0.13.2
- matplotlib 3.9.2

Full OpenAlex-scale runs require substantial RAM and disk space because the workflow builds large sparse citation matrices and all-paper dictionaries.
