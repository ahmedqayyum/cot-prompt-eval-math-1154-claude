# Cloned Repositories

## Repository 1: grade-school-math (GSM8K)
- **URL**: https://github.com/openai/grade-school-math
- **Purpose**: Official GSM8K dataset repository from OpenAI
- **Location**: `code/grade-school-math/`
- **Key files**:
  - `grade_school_math/dataset.py` - Dataset loading utilities
  - `grade_school_math/calculator.py` - Calculator annotation handling
  - `dataset/` - Raw dataset files (JSONL format)
- **Notes**: Contains the dataset in JSONL format along with utilities for answer extraction and calculator annotation parsing. The `calculator.py` module handles the `<<expression=result>>` annotations found in solutions.

## Repository 2: math-dataset (MATH)
- **URL**: https://github.com/hendrycks/math
- **Purpose**: Official MATH dataset repository from Hendrycks et al.
- **Location**: `code/math-dataset/`
- **Key files**:
  - `modeling/` - Baseline model code
  - Various data directories by subject
- **Notes**: Contains the MATH dataset with competition-level mathematics problems across 7 subjects and 5 difficulty levels. Each problem includes a complete step-by-step solution.

## Usage for Experiments

The experiment runner can use these repositories to:
1. Load datasets directly from the JSONL/JSON files
2. Use answer extraction utilities (especially for GSM8K's calculator annotations)
3. Reference the solution format for constructing CoT exemplars
4. Access the dataset splits (train/test) for few-shot exemplar selection

For the experiment, the HuggingFace versions in `datasets/` are preferred for easier loading, but these repositories serve as reference implementations and contain additional utilities.
