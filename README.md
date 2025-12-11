# Policy Text Mining for County-Level Water Pollution Governance

## Overview
This project analyzes county-level water pollution governance policies using text mining and simple NLP techniques.  
The goal is to quantify how different types of policy instruments (regulatory, incentive, informational) evolve over time and across counties.

## Data
- Source: County-level policy documents collected from local government websites.
- Format: `.docx` files organized by city and county.
- Scope: [600+ policy documents, 2009–2023]

> Note: Raw policy documents are not included in this repository due to data sharing constraints.  
> Instead, the repo provides scripts and example outputs.

## Main Steps
1. **Document Ingestion**
   - Traverse folder structure: `city / county / .docx`
   - Extract raw text from `.docx`
   - Parse year from filenames

2. **Text Preprocessing**
   - Remove whitespace and non-Chinese characters
   - Chinese segmentation using `jieba`
   - Stopword removal

3. **Text Representation**
   - TF-IDF vectorization (`scikit-learn`)
   - Keyword extraction for each document / period

4. **Policy Instrument Classification**
   - Rule-based classification into:
     - *Regulatory* (e.g. enforcement, standards, penalties)
     - *Incentive* (e.g. subsidies, rewards, funding)
     - *Informational* (e.g. publicity, training, guidance)
   - Assign a dominant instrument type to each document

5. **Analysis & Visualization**
   - Yearly counts of each policy instrument type
   - County-level comparison
   - Export aggregated results as `.csv` for Power BI dashboard



## Notebooks
- `notebooks/01_load_and_clean.ipynb` – Load `.docx` files and clean text  
- `notebooks/02_tokenize_and_tfidf.ipynb` – Tokenization & TF-IDF  
- `notebooks/03_classify_policy_instruments.ipynb` – Rule-based classification  
- `notebooks/04_visualization.ipynb` – Trend plots & export for Power BI  

## Example Outputs
- `results/policy_clean.csv` – Cleaned and tokenized texts
- `results/policy_tfidf.csv` – TF-IDF matrix with metadata
- `results/year_tool_counts.csv` – Year × policy instrument statistics

## How to Run
1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/policy-text-mining-water-governance.git
   cd policy-text-mining-water-governance
