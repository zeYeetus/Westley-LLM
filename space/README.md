# Westley — inference backend

A FastAPI service that serves an instruction-finetuned GPT-2 small (124M),
built from scratch following Sebastian Raschka's *Build a Large Language
Model (From Scratch)*.

## Files
- `model.py` — the GPT-2 architecture and generation helpers (pure PyTorch).
- `app.py` — loads the finetuned weights and exposes `POST /generate`.
- `requirements.txt` — Python dependencies.
- `instruction_finetuned_gpt2.pth` — the finetuned weights (tracked with Git LFS).

## Run it locally
From this `space/` folder:
```bash
pip install -r requirements.txt
uvicorn app:app --host 0.0.0.0 --port 8000
```
The first launch downloads the GPT-2 tokenizer vocabulary, then loads the model.
Once it prints `Application startup complete`, the API is live at
http://localhost:8000. Open the front end (`../frontend/index.html`) in a browser
and the Generate button will call this backend.

## Endpoint
`POST /generate` with JSON:
```json
{ "instruction": "...", "input": "", "max_new_tokens": 256, "temperature": 0.0, "top_k": 1 }
```
returns `{ "response": "..." }`. `GET /` is a health check.
