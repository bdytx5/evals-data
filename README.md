# Evaluation Results Data

This repository hosts JSON evaluation results for the OpenEvals leaderboard.

Results are automatically deployed to GitHub Pages when pushed to the main branch.

## Structure

```
results/
├── models.json                          # Index of all models
├── openai_gpt-5_20251106_000343/
│   └── final_results.json
├── openai_gpt-4.1_20251103_015714/
│   └── final_results.json
└── ...
```

## Accessing Results

Results are available at: `https://YOUR_USERNAME.github.io/evals-data/`

Example:
- Models index: `https://YOUR_USERNAME.github.io/evals-data/models.json`
- Specific model: `https://YOUR_USERNAME.github.io/evals-data/openai_gpt-5_20251106_000343/final_results.json`
