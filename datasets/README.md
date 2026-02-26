# Downloaded Datasets

This directory contains datasets for the research project. Data files are NOT committed to git due to size. Follow the download instructions below.

## Dataset 1: GSM8K (Grade School Math 8K)

### Overview
- **Source**: OpenAI / HuggingFace (`openai/gsm8k`)
- **Size**: Train: 7,473 examples, Test: 1,319 examples
- **Format**: HuggingFace Dataset (Arrow format)
- **Task**: Multi-step grade school math word problems
- **Splits**: train (7,473), test (1,319)
- **License**: MIT
- **Original repo**: https://github.com/openai/grade-school-math

### Download Instructions

**Using HuggingFace (recommended):**
```python
from datasets import load_dataset
dataset = load_dataset("openai/gsm8k", "main")
dataset.save_to_disk("datasets/gsm8k")
```

**Loading once downloaded:**
```python
from datasets import load_from_disk
dataset = load_from_disk("datasets/gsm8k")
```

### Data Format
Each example has two fields:
- `question`: The math word problem (string)
- `answer`: Step-by-step solution ending with `#### <final_answer>` (string)

The answer field contains calculator annotations like `<<16-3-4=9>>` within the solution text. The final numerical answer appears after `####`.

### Sample Data
```json
{
  "question": "Janet\u2019s ducks lay 16 eggs per day. She eats three for breakfast every morning and bakes muffins for her friends every day with four. She sells every remaining one at the farmers' market daily for $2 per fresh duck egg. How much in dollars does she make every day at the farmers' market?",
  "answer": "Janet sells 16 - 3 - 4 = <<16-3-4=9>>9 duck eggs a day.\nShe makes 9 * 2 = $<<9*2=18>>18 every day at the farmer's market.\n#### 18"
}
```

### Notes
- Grade school level (ages 6-12) but requires multi-step reasoning
- Average of 2-8 reasoning steps per problem
- Standard benchmark for CoT prompting evaluation
- Used by Wei et al. (2022), Kojima et al. (2022), Wang et al. (2022)

---

## Dataset 2: MATH (Competition Mathematics)

### Overview
- **Source**: EleutherAI/hendrycks_math (HuggingFace mirror of Hendrycks et al.)
- **Size**: Train: 7,500 examples, Test: 5,000 examples
- **Format**: HuggingFace Dataset (Arrow format)
- **Task**: Competition-level mathematics problems
- **Splits**: train (7,500), test (5,000)
- **License**: MIT
- **Original repo**: https://github.com/hendrycks/math

### Download Instructions

**Using HuggingFace (recommended):**
```python
from datasets import load_dataset, concatenate_datasets, DatasetDict

subjects = ['algebra', 'counting_and_probability', 'geometry', 'intermediate_algebra',
            'number_theory', 'prealgebra', 'precalculus']
all_train, all_test = [], []
for subject in subjects:
    ds = load_dataset("EleutherAI/hendrycks_math", subject)
    all_train.append(ds['train'])
    all_test.append(ds['test'])

combined = DatasetDict({
    'train': concatenate_datasets(all_train),
    'test': concatenate_datasets(all_test)
})
combined.save_to_disk("datasets/math")
```

**Loading once downloaded:**
```python
from datasets import load_from_disk
dataset = load_from_disk("datasets/math")
```

### Data Format
Each example has fields:
- `problem`: The math problem statement (string, may contain LaTeX)
- `solution`: Step-by-step solution with LaTeX formatting (string)
- `level`: Difficulty level ("Level 1" through "Level 5")
- `type`: Subject area (e.g., "Algebra", "Geometry", etc.)

### Difficulty Levels
- Level 1: Easiest (basic operations)
- Level 2: Easy
- Level 3: Medium
- Level 4: Hard
- Level 5: Hardest (competition-level)

### Subject Areas
- Algebra (train: 1,744, test: 1,187)
- Counting & Probability (train: 771, test: 474)
- Geometry (train: 870, test: 479)
- Intermediate Algebra (train: 1,295, test: 903)
- Number Theory (train: 869, test: 540)
- Prealgebra (train: 1,205, test: 871)
- Precalculus (train: 746, test: 546)

### Notes
- Significantly harder than GSM8K (competition-level vs grade school)
- Answers often require LaTeX parsing (e.g., `\boxed{42}`)
- 5 difficulty levels enable stratified analysis of CoT effectiveness
- Problems span diverse mathematical domains
- Solutions include step-by-step derivations suitable for CoT analysis
