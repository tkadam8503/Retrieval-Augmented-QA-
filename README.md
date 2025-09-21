# 🗂️ Retrieval-Augmented QA (RAG) — Minimal, Offline-Friendly

This repo contains a single-file Jupyter notebook that implements a compact RAG pipeline:

- **Indexing:** corpus → chunks → embeddings → FAISS (SBERT)  
- **Fallback:** if models can’t download, switches to **TF-IDF**  
- **Answering:** deterministic **extractive** answers with citations (default), or tiny greedy LLM if enabled  
- **Modes:** `BUILD_INDEX`, `ASK_ONCE`, `CHAT_CLI`

## Quickstart

```bash
# (optional) create env
conda create -n rag python=3.10 -y
conda activate rag

# install deps
pip install -r requirements.txt
```

Open the notebook and run cells top→bottom.

### Modes
- **BUILD_INDEX** – builds and saves an index to `./rag_index`
- **ASK_ONCE** – answers a single question and prints sources
- **CHAT_CLI** – simple console chat (type `exit` to quit)

> Default setting uses **extractive** answers for stability.  
> To try generation, set `ANSWER_BACKEND = "llm"` (falls back to extractive if output looks like gibberish).

## Project Structure

```
.
├─ notebooks/Project2_RAG.ipynb        # your notebook
├─ rag_index/                           # saved index (created at runtime)
├─ README.md
├─ requirements.txt
├─ LICENSE
└─ .gitignore
```

## Customize

- Replace the `DOCS` list in the notebook with your own corpus (strings).
- Adjust `chunk_size` and `overlap` in the chunker for longer docs.
- Increase `TOP_K` for more passages; the answer includes bracketed citations `[0]`, `[1]`.

## Troubleshooting

- **No internet / model errors:** The pipeline automatically uses TF-IDF and extractive answers.
- **Weird answers from tiny LLM:** Keep `ANSWER_BACKEND = "extractive"` for demos, or leave `llm` on with the gibberish detector enabled.
- **Windows temp path issues:** The runner executes in a temp directory; if you hit path errors, run from a shallow folder.

## License

MIT © You (see `LICENSE`).
