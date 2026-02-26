# Downloaded Papers

## Core Papers (User-Specified)

1. **Chain-of-Thought Prompting Elicits Reasoning in Large Language Models**
   - File: `2201.11903_chain_of_thought_prompting.pdf`
   - Authors: Jason Wei, Xuezhi Wang, Dale Schuurmans, et al. (Google Research)
   - Year: 2022 (NeurIPS)
   - arXiv: 2201.11903
   - Citations: ~15,700
   - Why relevant: Foundational paper introducing CoT prompting; directly tests the hypothesis

2. **Large Language Models are Zero-Shot Reasoners**
   - File: `2205.11916_zero_shot_cot.pdf`
   - Authors: Takeshi Kojima, Shixiang Shane Gu, Machel Reid, et al.
   - Year: 2022 (NeurIPS)
   - arXiv: 2205.11916
   - Citations: ~6,400
   - Why relevant: Introduces zero-shot CoT ("Let's think step by step"); key baseline method

## Additional Papers

3. **Self-Consistency Improves Chain of Thought Reasoning in Language Models**
   - File: `2203.11171_self_consistency_cot.pdf`
   - Authors: Xuezhi Wang, Jason Wei, Dale Schuurmans, Quoc Le, Ed Chi
   - Year: 2022
   - arXiv: 2203.11171
   - Why relevant: Self-consistency decoding is a major enhancement to CoT

4. **Training Verifiers to Solve Math Word Problems (GSM8K paper)**
   - File: `2110.14168_training_verifiers_gsm8k.pdf`
   - Authors: Karl Cobbe, Vineet Kosaraju, Mohammad Bavarian, et al. (OpenAI)
   - Year: 2021
   - arXiv: 2110.14168
   - Why relevant: Introduces GSM8K dataset; establishes baselines for math reasoning

5. **Measuring Mathematical Problem Solving With the MATH Dataset**
   - File: `2103.03874_measuring_math_dataset.pdf`
   - Authors: Dan Hendrycks, Collin Burns, Saurav Kadavath, et al.
   - Year: 2021
   - arXiv: 2103.03874
   - Why relevant: Introduces MATH dataset with difficulty levels; key evaluation benchmark

6. **Tree of Thoughts: Deliberate Problem Solving with Large Language Models**
   - File: `2305.10601_tree_of_thoughts.pdf`
   - Authors: Shunyu Yao, Dian Yu, Jeffrey Zhao, et al.
   - Year: 2023
   - arXiv: 2305.10601
   - Why relevant: Extends CoT to tree-structured reasoning; comparison method

7. **Large Language Models as Optimizers (OPRO)**
   - File: `2309.03409_cumulative_reasoning.pdf`
   - Authors: Chengrun Yang, Xuezhi Wang, Yifeng Lu, et al.
   - Year: 2023
   - arXiv: 2309.03409
   - Why relevant: Optimizes prompts using LLMs; found improved CoT triggers

8. **Large Language Models Cannot Self-Correct Reasoning Yet**
   - File: `2310.01798_llemma_math_llm.pdf`
   - Authors: Jie Huang, Xinyun Chen, Swaroop Mishra, et al.
   - Year: 2023
   - arXiv: 2310.01798
   - Why relevant: Negative result on self-correction; informs experimental design

9. **Large Language Models Are Human-Level Prompt Engineers (APE)**
   - File: `2211.01910_pal_program_aided.pdf`
   - Authors: Yongchao Zhou, Andrei Ioan Muresanu, Ziwen Han, et al.
   - Year: 2022
   - arXiv: 2211.01910
   - Why relevant: Automatic prompt engineering; alternative to manual CoT prompts

10. **ART: Automatic multi-step reasoning and tool-use for large language models**
    - File: `2303.09014_complexity_based_prompting.pdf`
    - Authors: Bhargavi Paranjape, Scott Lundberg, Sameer Singh, et al.
    - Year: 2023
    - arXiv: 2303.09014
    - Why relevant: Automated CoT with tool use; integration of reasoning and computation

11. **Measuring Faithfulness in Chain-of-Thought Reasoning**
    - File: `2307.13702_skills_in_context.pdf`
    - Authors: Tamera Lanham, Anna Chen, Ansh Radhakrishnan, et al.
    - Year: 2023
    - arXiv: 2307.13702
    - Why relevant: Studies whether CoT reasoning is faithful to model's internal process

12. **MATH-Shepherd: Verify and Reinforce LLMs Step-by-step**
    - File: `2312.08935_math_shepherd_verifier.pdf`
    - Authors: Peiyi Wang, Lei Li, Zhihong Shao, et al.
    - Year: 2023
    - arXiv: 2312.08935
    - Why relevant: Process reward models for verifying step-by-step reasoning

## Supporting Files

- `search_results.json` - Search results from Semantic Scholar API
- `paper_abstracts.json` - Abstracts fetched from arXiv API
- `pages/` - Chunked PDF files for detailed reading
