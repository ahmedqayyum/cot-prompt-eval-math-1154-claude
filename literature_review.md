# Literature Review: Chain-of-Thought Prompting for Mathematical Reasoning

## Research Area Overview

Chain-of-thought (CoT) prompting has emerged as one of the most impactful techniques for improving large language model (LLM) performance on complex reasoning tasks, particularly mathematical reasoning. First introduced by Wei et al. (2022), CoT prompting involves providing intermediate reasoning steps as part of few-shot exemplars, enabling models to decompose multi-step problems into sequential sub-steps. This technique has spawned a rich research area exploring variations (zero-shot CoT, self-consistency, tree-of-thought), applications across mathematical domains of varying difficulty, and mechanistic understanding of why step-by-step reasoning improves performance.

## Key Papers

### Paper 1: Chain-of-Thought Prompting Elicits Reasoning in Large Language Models
- **Authors**: Jason Wei, Xuezhi Wang, Dale Schuurmans, Maarten Bosma, et al.
- **Year**: 2022 (NeurIPS 2022)
- **Source**: arXiv:2201.11903
- **Citations**: ~15,700
- **Key Contribution**: Introduced chain-of-thought prompting — augmenting few-shot exemplars with intermediate reasoning steps to improve LLM reasoning.
- **Methodology**: Few-shot prompting where each exemplar includes a step-by-step reasoning chain (8 manually written exemplars). Evaluated with greedy decoding across GPT-3, LaMDA, PaLM, UL2, and Codex.
- **Datasets Used**: GSM8K, SVAMP, ASDiv, AQuA, MAWPS (arithmetic); CSQA, StrategyQA, Date Understanding, Sports Understanding, SayCan (commonsense); Last Letter Concatenation, Coin Flip (symbolic).
- **Key Results**:
  - PaLM 540B + CoT: 57% on GSM8K (vs 18% standard prompting, vs 55% finetuned GPT-3+verifier)
  - CoT is an **emergent ability** requiring ~100B+ parameters; hurts performance on small models (<10B)
  - **Larger gains on harder problems**: GSM8K performance more than doubled; minimal gains on single-step problems (SingleOp)
  - Robust across different annotators, exemplar orders, numbers of exemplars, and model families
- **Ablation findings**: Equation-only prompting, variable compute (dots), and chain-of-thought-after-answer all fail to match CoT, demonstrating that sequential natural language reasoning is the key factor.
- **Limitations**: No guarantee of correct reasoning paths; only works at large scale; doesn't answer whether models truly "reason."
- **Code Available**: No official repository.
- **Relevance to Our Research**: This is the foundational paper for our hypothesis. Directly demonstrates that CoT improves math reasoning by 15-200%+ depending on task difficulty, strongly supporting the hypothesis that gains vary by problem complexity.

### Paper 2: Large Language Models are Zero-Shot Reasoners
- **Authors**: Takeshi Kojima, Shixiang Shane Gu, Machel Reid, Yutaka Matsuo, Yusuke Iwasawa
- **Year**: 2022 (NeurIPS 2022)
- **Source**: arXiv:2205.11916
- **Citations**: ~6,400
- **Key Contribution**: Showed that simply adding "Let's think step by step" enables zero-shot chain-of-thought reasoning without any few-shot exemplars.
- **Methodology**: Two-stage prompting: (1) reasoning extraction with "Let's think step by step", (2) answer extraction. Evaluated on 12 datasets with 17 models (InstructGPT-3, GPT-3, PaLM 8B/62B/540B, GPT-2, GPT-Neo, GPT-J, T0, OPT).
- **Key Results**:
  - text-davinci-002: MultiArith 17.7% → 78.7%, GSM8K 10.4% → 40.7%
  - PaLM 540B: GSM8K 12.5% → 43.0% (zero-shot-CoT), → 70.1% (+ self-consistency)
  - Zero-shot-CoT underperforms few-shot-CoT but substantially beats standard few-shot prompting
  - No improvement on simple tasks (SingleEq, AddSub) or commonsense reasoning
  - "Let's think step by step" best among 16 tested templates (78.7% vs next best 77.3%)
- **Model scale finding**: Same emergent pattern as Wei et al. — flat curve without CoT, steep improvement with CoT as scale increases.
- **Relevance**: Establishes zero-shot-CoT as an important baseline. Shows that even without hand-crafted exemplars, the reasoning capability exists — the prompt just needs to trigger it. Critical for our experimental design: we should compare direct, zero-shot-CoT, and few-shot-CoT.

### Paper 3: Self-Consistency Improves Chain of Thought Reasoning in Language Models
- **Authors**: Xuezhi Wang, Jason Wei, Dale Schuurmans, Quoc Le, Ed Chi
- **Year**: 2022
- **Source**: arXiv:2203.11171
- **Citations**: ~6,000
- **Key Contribution**: Proposed self-consistency decoding — sampling multiple reasoning paths and selecting the most frequent answer via majority vote, replacing greedy decoding.
- **Key Results**: PaLM 540B + few-shot-CoT + self-consistency → 74.4% on GSM8K (vs 56.9% greedy CoT). Works with zero-shot-CoT too (PaLM 540B: 43.0% → 70.1% on GSM8K).
- **Relevance**: Self-consistency is a key enhancement to CoT that we could incorporate as an experimental condition. Demonstrates that the quality of reasoning paths varies and aggregation helps.

### Paper 4: Training Verifiers to Solve Math Word Problems (GSM8K)
- **Authors**: Karl Cobbe, Vineet Kosaraju, Mohammad Bavarian, Mark Chen, et al.
- **Year**: 2021
- **Source**: arXiv:2110.14168
- **Citations**: ~7,500
- **Key Contribution**: Introduced GSM8K dataset (8.5K grade school math word problems) and showed that training verifiers to rank candidate solutions improves performance.
- **Key Results**: Finetuned GPT-3 175B: 33% → 55% with verifier on GSM8K.
- **Relevance**: GSM8K is our primary dataset. The paper established the benchmark and demonstrated that multi-step reasoning is challenging even for large models, providing the motivation for CoT prompting research.

### Paper 5: Measuring Mathematical Problem Solving With the MATH Dataset
- **Authors**: Dan Hendrycks, Collin Burns, Saurav Kadavath, Akul Arora, Steven Basart
- **Year**: 2021
- **Source**: arXiv:2103.03874
- **Key Contribution**: Introduced MATH dataset (12,500 competition math problems) with 5 difficulty levels and 7 subject areas, each with step-by-step solutions.
- **Datasets**: 7 subjects (algebra, counting/probability, geometry, intermediate algebra, number theory, prealgebra, precalculus), 5 difficulty levels.
- **Relevance**: MATH is our secondary dataset, representing harder problems than GSM8K. Its difficulty levels allow direct testing of the hypothesis that CoT gains increase with problem complexity.

### Paper 6: Tree of Thoughts: Deliberate Problem Solving with Large Language Models
- **Authors**: Shunyu Yao, Dian Yu, Jeffrey Zhao, Izhak Shafran, Thomas L. Griffiths
- **Year**: 2023
- **Source**: arXiv:2305.10601
- **Key Contribution**: Generalized CoT from a single linear chain to a tree structure, allowing exploration, backtracking, and strategic lookahead during reasoning.
- **Relevance**: Represents the next evolution beyond CoT — if linear CoT helps, exploring multiple reasoning branches helps more. Could be a comparison point for our experiments.

### Paper 7: ART: Automatic multi-step reasoning and tool-use for large language models
- **Authors**: Bhargavi Paranjape, Scott Lundberg, Sameer Singh, et al.
- **Year**: 2023
- **Source**: arXiv:2303.09014
- **Key Contribution**: Automates CoT prompting by selecting demonstrations from a task library and interleaving reasoning with tool use (e.g., running code for calculations).
- **Relevance**: Shows that CoT can be automated and combined with tool use, suggesting experimental conditions beyond pure natural language reasoning.

### Paper 8: Measuring Faithfulness in Chain-of-Thought Reasoning
- **Authors**: Tamera Lanham, Anna Chen, Ansh Radhakrishnan, et al.
- **Year**: 2023
- **Source**: arXiv:2307.13702
- **Key Contribution**: Investigates whether stated CoT reasoning actually reflects the model's internal reasoning process. Finds that models show large variability in faithfulness.
- **Relevance**: Important for interpreting our results — CoT performance gains may not mean the model is truly "reasoning" step-by-step internally.

### Paper 9: Large Language Models as Optimizers (OPRO)
- **Authors**: Chengrun Yang, Xuezhi Wang, Yifeng Lu, et al.
- **Year**: 2023
- **Source**: arXiv:2309.03409
- **Key Contribution**: Uses LLMs to optimize prompts, discovering that optimized prompts can substantially outperform hand-crafted ones including "Let's think step by step."
- **Relevance**: Suggests that the specific wording of CoT prompts matters and can be optimized, which is relevant to experimental design.

### Paper 10: Large Language Models Cannot Self-Correct Reasoning Yet
- **Authors**: Jie Huang, Xinyun Chen, Swaroop Mishra, et al.
- **Year**: 2023
- **Source**: arXiv:2310.01798
- **Key Contribution**: Shows that LLMs cannot reliably self-correct reasoning without external feedback, challenging the assumption that iterative refinement helps.
- **Relevance**: Important negative result — suggests that single-pass CoT may be more reliable than multi-round self-correction approaches for our experiments.

## Common Methodologies

- **Few-shot CoT (Wei et al., 2022)**: 8 manually written exemplars with reasoning chains; used in [Papers 1, 2, 3]
- **Zero-shot CoT (Kojima et al., 2022)**: "Let's think step by step" trigger; used in [Papers 2, 3]
- **Self-consistency (Wang et al., 2022)**: Sample multiple paths, majority vote; used in [Papers 2, 3]
- **Greedy decoding**: Default in most CoT papers; temperature=0
- **Two-stage evaluation**: Generate reasoning, then extract answer (especially for zero-shot)

## Standard Baselines

- **Standard prompting (direct answer)**: No reasoning steps, just Q→A
- **Zero-shot prompting**: Task instruction only, no examples
- **Few-shot prompting (without CoT)**: Examples with Q→A only, no intermediate steps
- **Finetuned models**: GPT-3 finetuned on GSM8K training data (33% accuracy)
- **Finetuned + verifier**: GPT-3 + trained verifier (55% on GSM8K)

## Evaluation Metrics

- **Solve rate / Accuracy**: Exact match of final numerical answer (primary metric across all papers)
- **Answer extraction**: Parse final answer after "The answer is" or specific format triggers
- **Error analysis categories**: Semantic understanding errors, one-step missing, calculator errors, hallucinations

## Datasets in the Literature

| Dataset | Type | Size (test) | Difficulty | Used in |
|---------|------|-------------|------------|---------|
| GSM8K | Grade school math | 1,319 | Medium (multi-step) | Papers 1,2,3,4 |
| MATH | Competition math | 5,000 | Hard (5 levels) | Paper 5 |
| MultiArith | Arithmetic | 600 | Easy-Medium | Papers 1,2 |
| SVAMP | Math word problems | 1,000 | Medium | Papers 1,2 |
| AQuA-RAT | Algebraic (MC) | 254 | Medium | Papers 1,2 |
| MAWPS | Math word problems | varies | Easy | Paper 1 |
| ASDiv | Diverse math | 2,096 | Medium | Paper 1 |

## Gaps and Opportunities

1. **Cross-model comparison with modern models**: The original CoT papers tested on GPT-3, LaMDA, and PaLM. No systematic comparison across GPT-4, Claude, and Gemini with the same methodology exists.
2. **Quantifying complexity-dependent gains**: While Wei et al. note "larger gains on harder problems," no systematic analysis correlates number of reasoning steps or difficulty level with CoT improvement magnitude.
3. **Budget-conscious evaluation**: Most papers use very large models (540B PaLM). Our $50 budget constrains us to API-based evaluation, which is practical and realistic.
4. **Standardized prompts across models**: Papers often use model-specific prompts. A controlled comparison using identical prompts across model families would be valuable.

## Recommendations for Our Experiment

Based on the literature review:

### Recommended Datasets
1. **GSM8K** (primary): Well-established benchmark, moderate difficulty, used across all key papers. 1,319 test problems provide statistical significance.
2. **MATH** (secondary): Higher difficulty with 5 levels, enabling direct measurement of complexity-dependent CoT gains. 5,000 test problems across 7 subjects.

### Recommended Baselines
1. **Direct prompting** (no CoT): Standard few-shot or zero-shot without reasoning steps
2. **Zero-shot-CoT**: "Let's think step by step" — minimal effort, strong baseline
3. **Few-shot-CoT**: 8 exemplars with reasoning chains (following Wei et al.)
4. **(Optional) Self-consistency**: If budget allows, sample multiple paths and majority vote

### Recommended Metrics
- **Primary**: Solve rate (exact match accuracy)
- **Secondary**: Accuracy by difficulty level (MATH) or number of reasoning steps (GSM8K)
- **Analysis**: Error categorization on a sample of failures

### Methodological Considerations
- Use **greedy decoding** (temperature=0) for reproducibility, consistent with prior work
- Use **identical prompts** across model families for fair comparison
- Evaluate a **subset** (e.g., 200-500 problems) per condition to stay within budget
- Compare at least 2-3 model families (GPT-4, Claude, Gemini) as specified in the hypothesis
- Stratify analysis by problem difficulty to test the "larger gains on harder problems" hypothesis
- Consider using the answer extraction format from Kojima et al. for consistency
