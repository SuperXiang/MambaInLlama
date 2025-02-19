## Evaluations

To run evaluations of models in the [lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness/tree/big-refactor) library:

1. Clone the `lm-evaluation-harness` repository by running `git clone https://github.com/EleutherAI/lm-evaluation-harness.git`. Use the `big-refactor` branch by running `git checkout big-refactor`.
2. Follow the number of shots specified in `https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard`. For example, for the teacher model HuggingFaceH4/zephyr-7b-beta, their configuration is [here](https://huggingface.co/HuggingFaceH4/zephyr-7b-beta).
3. Run the evaluation with the following command (more documentation is available in the [lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness/tree/big-refactor) repository):

```
python evals/lm_harness_eval.py --model mamba_hybrid --model_args pretrained=[MODEL_PATH] --tasks mmlu --num_fewshot 5 --device cuda --batch_size 16
```

```
python benchmark/llm_eval/lm_harness_eval.py --model mamba_hybrid --model_args pretrained=JunxiongWang/llama3_mamba_0_5_dpo_ep3 --tasks hellaswag,piqa,arc_easy,arc_challenge,winogrande,openbookqa,pubmedqa,race --num_fewshot 0 --device cuda --batch_size 16
```

| Model                     | Training Tokens | WG    | PIQA  | HellaSwag | ARC-Easy  | ARC-Challenge  | MMLU  | OpenBook | TruthFul | PubMed | RACE  | Avg   |
|---------------------------|--------|-------|-------|-----------|--------|--------|-------|----------|----------|--------|-------|-------|
| Mamba-2-Hybrid-4K         | 3.5T   | **71.27** | **79.65** | **77.68**   | **77.23** | 47.70  | 53.60 | 42.80    | 38.72   | 69.80 | **39.71** | 59.82 |
| Our [Mamba-Llama3 (50% att)](https://huggingface.co/JunxiongWang/llama3_mamba_0_5_dpo_ep3) | 20B     | 68.43 | 78.02 | 77.55     | 72.60  | **50.85** | **59.26** | **44.00**  | **45.24**  | **72.80**  | 38.47 | **60.72** |

LM eval benchmark results for Mamba-Llama3 compared with Nvidia Mamba-2-Hybrid-4K.