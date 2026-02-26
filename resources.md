# Resources Catalog

## Summary
This document catalogs all resources gathered for the research project: "Evaluating Chain-of-Thought Prompting Effectiveness Across Mathematical Reasoning Tasks."

Resources include 12 downloaded papers, 2 datasets, and 2 code repositories, sufficient to conduct experiments testing whether CoT prompting improves LLM performance on multi-step mathematical reasoning by 15-30% with larger gains on harder problems.

## Papers
Total papers downloaded: 12

| # | Title | Authors | Year | File | Key Info |
|---|-------|---------|------|------|----------|
| 1 | Chain-of-Thought Prompting Elicits Reasoning in LLMs | Wei et al. | 2022 | `papers/2201.11903_chain_of_thought_prompting.pdf` | Foundational CoT paper; NeurIPS 2022; ~15.7K citations |
| 2 | Large Language Models are Zero-Shot Reasoners | Kojima et al. | 2022 | `papers/2205.11916_zero_shot_cot.pdf` | Zero-shot CoT; NeurIPS 2022; ~6.4K citations |
| 3 | Self-Consistency Improves CoT Reasoning | Wang et al. | 2022 | `papers/2203.11171_self_consistency_cot.pdf` | Majority vote decoding; ~6K citations |
| 4 | Training Verifiers to Solve Math Word Problems | Cobbe et al. | 2021 | `papers/2110.14168_training_verifiers_gsm8k.pdf` | GSM8K dataset paper; ~7.5K citations |
| 5 | Measuring Math Problem Solving With MATH Dataset | Hendrycks et al. | 2021 | `papers/2103.03874_measuring_math_dataset.pdf` | MATH dataset paper |
| 6 | Tree of Thoughts | Yao et al. | 2023 | `papers/2305.10601_tree_of_thoughts.pdf` | Tree-structured reasoning |
| 7 | Large Language Models as Optimizers (OPRO) | Yang et al. | 2023 | `papers/2309.03409_cumulative_reasoning.pdf` | Prompt optimization |
| 8 | LLMs Cannot Self-Correct Reasoning Yet | Huang et al. | 2023 | `papers/2310.01798_llemma_math_llm.pdf` | Self-correction limits |
| 9 | LLMs Are Human-Level Prompt Engineers (APE) | Zhou et al. | 2022 | `papers/2211.01910_pal_program_aided.pdf` | Auto prompt engineering |
| 10 | ART: Automatic Reasoning and Tool-use | Paranjape et al. | 2023 | `papers/2303.09014_complexity_based_prompting.pdf` | Automated CoT + tools |
| 11 | Measuring Faithfulness in CoT Reasoning | Lanham et al. | 2023 | `papers/2307.13702_skills_in_context.pdf` | CoT faithfulness analysis |
| 12 | MATH-Shepherd Verifier | Wang et al. | 2023 | `papers/2312.08935_math_shepherd_verifier.pdf` | Process reward models |

See `papers/README.md` for detailed descriptions.

## Datasets
Total datasets downloaded: 2

| Name | Source | Size | Task | Location | Notes |
|------|--------|------|------|----------|-------|
| GSM8K | openai/gsm8k (HuggingFace) | Train: 7,473 / Test: 1,319 | Grade school math word problems | `datasets/gsm8k/` | Primary benchmark; multi-step reasoning |
| MATH | EleutherAI/hendrycks_math (HuggingFace) | Train: 7,500 / Test: 5,000 | Competition mathematics | `datasets/math/` | 5 difficulty levels, 7 subjects |

See `datasets/README.md` for detailed descriptions and download instructions.

## Code Repositories
Total repositories cloned: 2

| Name | URL | Purpose | Location | Notes |
|------|-----|---------|----------|-------|
| grade-school-math | github.com/openai/grade-school-math | GSM8K dataset + utilities | `code/grade-school-math/` | Answer extraction, calculator annotations |
| math-dataset | github.com/hendrycks/math | MATH dataset + baselines | `code/math-dataset/` | Competition math problems |

See `code/README.md` for detailed descriptions.

## Resource Gathering Notes

### Search Strategy
1. Started with the two user-specified papers (arXiv:2201.11903 and arXiv:2205.11916)
2. Used Semantic Scholar API to retrieve reference networks from both papers
3. Identified highly cited related papers from reference lists
4. Fetched abstracts via arXiv API for all additional papers
5. Deep-read both user-specified papers using PDF chunker (all pages)
6. Skimmed additional papers via API abstracts

### Selection Criteria
- Papers directly relevant to CoT prompting and mathematical reasoning
- Dataset papers for the two benchmarks specified in the research topic
- Papers introducing key methodological variants (zero-shot CoT, self-consistency, tree-of-thought)
- Papers with critical analysis of CoT (faithfulness, self-correction limitations)
- High citation count (>1000) as indicator of impact

### Challenges Encountered
- Semantic Scholar keyword search was rate-limited (HTTP 429), requiring reliance on reference network traversal
- Paper-finder service was not available, requiring manual search
- HuggingFace dataset name for MATH required searching multiple mirrors (resolved via `EleutherAI/hendrycks_math`)
- Some arXiv IDs returned different papers than expected file names (documented in papers/README.md)

### Gaps and Workarounds
- Could not search for very recent (2024-2025) papers systematically due to API rate limits. The literature review focuses on 2021-2023 foundational work which is sufficient for experimental design.
- No official CoT prompting reference implementation exists. Prompts must be constructed from examples in the papers (available in appendices of Wei et al. and Kojima et al.).

## Recommendations for Experiment Design

Based on gathered resources, recommend:

### 1. Primary Dataset: GSM8K
- Well-established benchmark used across all key CoT papers
- 1,319 test problems sufficient for statistical significance
- Multi-step reasoning with clear answer extraction (`#### <answer>`)
- Directly comparable to results in Wei et al. (2022) and Kojima et al. (2022)

### 2. Secondary Dataset: MATH
- 5 difficulty levels enable testing hypothesis that CoT gains increase with problem complexity
- 7 subject areas allow cross-domain analysis
- More challenging than GSM8K, providing ceiling room for measuring improvement
- LaTeX-formatted answers require careful parsing (`\boxed{answer}`)

### 3. Prompting Conditions to Compare
1. **Direct prompting** (zero-shot): "Q: [problem] A: The answer is"
2. **Zero-shot-CoT**: "Q: [problem] A: Let's think step by step."
3. **Few-shot standard**: 8 exemplars with Q→A only
4. **Few-shot-CoT**: 8 exemplars with step-by-step reasoning chains

### 4. Models to Evaluate
Per the hypothesis, evaluate across model families:
- GPT-4 (OpenAI) — via API
- Claude (Anthropic) — via API
- Gemini (Google) — via API

### 5. Evaluation Metrics
- **Primary**: Solve rate / accuracy (exact match of final answer)
- **Stratified**: Accuracy broken down by difficulty level (MATH) and number of solution steps (GSM8K)
- **Delta**: Improvement from direct prompting to CoT (absolute and relative)

### 6. Budget Considerations ($50)
- Use subsets if needed: 200-500 problems per condition
- Prioritize test set evaluation (not training)
- GSM8K (1,319 problems) is manageable; MATH (5,000) may need sampling
- Estimate ~$0.01-0.05 per API call depending on model and token count
- With 4 conditions x 3 models x ~500 problems = ~6,000 API calls
- At ~$0.02/call average ≈ $120, so subsampling to ~200 problems per condition may be necessary (~$48)
