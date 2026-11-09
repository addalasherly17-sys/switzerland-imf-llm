# switzerland-imf-llm

A Google Colab notebook that reads one IMF staff report with Gemini models and checks the results against the report.

**Source:** IMF Country Report No. 25/263, *Switzerland: 2025 Article IV Consultation* (September 2025, 76 pages). The PDF is in `data/`.

## Layout

| Path | Contents |
|---|---|
| `Switzerland_IMF_Pipeline.ipynb` | the notebook, saved with the outputs of its Colab run |
| `data/` | the IMF report |
| `cache/replies.zip` | every model reply of the recorded run, so a rerun needs no key |
| `cache/vectors_*.npy` | the chunk embeddings |
| `results/` | JSON outputs and the two 300 dpi figures |
| `requirements.txt` | package versions of the Colab runtime |

## How to run

1. Open the notebook in Colab with `data/` and `cache/` in `/content` (clone this repository there, or upload the two folders).
2. Choose *Runtime > Run all*.

All 160 model calls are answered from `cache/replies.zip`, so no API key is needed. To make fresh calls, add a Gemini key as a Colab secret named `GEMINI_FREE_KEY` and delete `cache/replies.zip`.

The models are `gemini-3.6-flash` (writer) and `gemini-3.5-flash` (judge). Embeddings come from `thenlper/gte-small` and are searched with a FAISS `IndexFlatL2`.

## How the code is organised

Each result is a function marked `@asset`. Its parameter names are the results it needs, and `make()` builds them in dependency order with `graphlib`.

## Licence

MIT, see `LICENSE`. The IMF report remains the property of the International Monetary Fund and is included only so the notebook can run.
