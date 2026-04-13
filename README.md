# Policy Instrument Classification: LLM Zero-Shot Evaluation & Prompt Sensitivity Analysis

## 📝 Overview
This project systematically evaluates **Google Gemini's zero-shot capability** for classifying policy instruments in Chinese county-level water pollution governance policies. We compare rule-based classification with LLM results, analyze prompt sensitivity, identify disagreement patterns, and validate findings with human annotation.

**Core Research Questions:**
1. How sensitive is LLM classification to different prompt designs?
2. What is the inter-rater agreement between rule-based and LLM methods?
3. Which method better aligns with human judgment on contentious cases?

## 📊 Dataset
- **Source**: 578 county-level water pollution control policies from Zhejiang Province, China
- **Format**: Structured text with document metadata (city, county, year, clean text)
- **Base Data**: `output/classify/policy_with_labels.csv` (rule-based labels + TF-IDF features)
- **Labels**: 3 policy instrument types
  - *Regulatory* (强制性/约束): enforcement, standards, penalties
  - *Incentive* (激励性): subsidies, rewards, grants
  - *Informational* (信息性): publicity, guidance, training

## 📚 Notebooks

### 1. `policy nlp.ipynb` – Baseline NLP Pipeline
Complete workflow for building the foundation dataset:
- Load and preprocess .docx documents
- Chinese text cleaning and tokenization (jieba)
- TF-IDF feature extraction
- Rule-based policy instrument classification
- Export clean dataset with labels

**Output**: `output/classify/policy_with_labels.csv`

### 2. `policy_llm_evaluation.ipynb` – LLM Evaluation Study
Main research notebook conducting multi-phase annotation agreement study:
- **Phase 1**: Design 8 orthogonal prompt variants (language, detail level, label order, role, format)
- **Phase 2**: Batch classify with Gemini-2.5-Flash via Google GenAI API
- **Phase 3**: Prompt sensitivity analysis (flip rates, consistency scores, unstable document detection)
- **Phase 4**: Compute inter-rater agreement (Cohen's Kappa, confusion matrices, disagreement patterns)
- **Phase 5**: Export disputed samples for human annotation & validation
- **Phase 6**: Three-way evaluation (Rule vs LLM vs Human ground truth)

## 📁 Output Structure

### Evaluation Results
- `policy_full_results.csv` – Complete results with rule, LLM, and human labels
- `multi_prompt_results.csv` – Classification results from all 8 prompt variants
- `disagreements_for_annotation.csv` – Disputed cases for human review
- `human_annotated.csv` – Ground truth labels from manual annotation
- `agreement_control_samples.csv` – Control samples for consistency checking

### Visualizations
- `confusion_matrix_rule_vs_llm.png` – Rule-based vs Gemini classification confusion matrix
- `prompt_agreement_comparison.png` – Inter-prompt agreement heatmap
- `prompt_recall_heatmap.png` – Per-label recall across all prompt variants
- `three_way_confusion.png` – Ternary confusion matrix (Rule vs LLM vs Human)
- `label_distribution_summary.png` – Label distribution comparison
- `error_attribution.png` – Error type breakdown
- `disagreement_patterns.png` – Pattern analysis of rule-LLM disagreements
- `psi_distribution.png` & `psi_vs_textlen.png` – Population Stability Index analysis

### Analysis Exports
- `visual/county_tool_counts.csv` – Policy instrument distribution by county
- `visual/year_tool_counts.csv` – Temporal trends of policy instruments

## 🔧 Setup & Usage

### Requirements
```bash
pip install google-genai pandas scikit-learn matplotlib seaborn numpy tqdm python-docx
```

### Configuration
1. Set Gemini API key in notebook:
   ```python
   GEMINI_API_KEY = "your-api-key-here"
   ```
2. Adjust model name if needed (default: `gemini-2.5-flash`)

### Running the Pipeline
```bash
# 1. Run baseline NLP pipeline first
jupyter notebook policy_nlp.ipynb

# 2. Run LLM evaluation study
jupyter notebook policy_llm_evaluation.ipynb
```

## 📈 Key Findings
- Compare prompt sensitivity across 8 variants
- Quantify rule-LLM inter-rater agreement (Kappa score)
- Identify document types most prone to classification disagreement
- Validate findings against human annotation baseline

## 📖 Technical Notes
- All prompts implemented with Gemini-2.5-Flash API
- Prompt variants designed to test 5 orthogonal dimensions (language, details, order, role, format)
- Ground truth established through manual annotation of disagreement cases
- Metrics: Cohen's Kappa, accuracy, F1-score, confusion matrices
