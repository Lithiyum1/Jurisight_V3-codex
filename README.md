# Jurisight V3

Jurisight is an end-to-end legal AI workflow for ECHR article-violation prediction using multi-label transformer models (BERT, RoBERTa, Legal-BERT), fairness diagnostics, explainability, and a Flask web UI generated from the notebook.

## What's improved

This version adds improvements across four areas:

1. **Security hardening**
   - Removed hardcoded ngrok token usage from launch flow.
   - Uses `NGROK_AUTH_TOKEN` environment variable instead.
   - Added safer CORS configuration source via env (`CORS_ORIGINS`).

2. **Code structure**
   - Centralized threshold defaults/grid in `Config`.
   - Added explicit threshold-optimization helper.
   - Saved reusable threshold artifacts (`model_thresholds.json`).

3. **Model quality**
   - Added per-label threshold tuning on validation split.
   - Uses tuned thresholds for test predictions (instead of fixed 0.5).

4. **Deployment polish**
   - Flask now exposes `/api/health`.
   - Prediction endpoint returns per-label threshold metadata.
   - Model API includes threshold info.
   - Frontend can use `window.API_BASE` and displays threshold per result row.

## Run notes

Open and run `Jurisight_V3.ipynb` top-to-bottom in Colab/Jupyter.

For public tunnel launch (optional):

```python
import os
os.environ["NGROK_AUTH_TOKEN"] = "<your-token>"
```

Optional frontend API base override:

```html
<script>
  window.API_BASE = "https://your-api.example.com";
</script>
```

## Artifacts

Expected outputs in `/content/jurisight_outputs` include:
- `model_comparison.csv`
- `fairness_results.json`
- `model_thresholds.json`
- XAI outputs under `/content/jurisight_outputs/xai`
