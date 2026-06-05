# indexacao-encoinfo

🇺🇸 English | 🇧🇷 [Português](README.md)

> Semantic web-page search by embeddings: crawl a site, index it in Pinecone, and answer queries by similarity through a Flask interface.

## Overview

A **semantic search** system over web pages. It web-scrapes a site, generates **embeddings** for each page with Sentence Transformers, indexes the vectors in **Pinecone**, and serves a Flask interface that answers queries by vector similarity (instead of keyword search).

## Pipeline

1. **`extracao.py`** — crawler that cleans HTML and produces `pages.csv`.
2. **`db.py`** — loads the CSV, generates embeddings (`all-MiniLM-L6-v2`), and upserts them in batches into Pinecone.
3. **`cli.py`** — Flask app: search queries Pinecone and fetches titles in parallel (30 threads), returning similarity scores.

## Stack

Python · sentence-transformers (all-MiniLM-L6-v2) · Pinecone · Flask · requests · pandas · concurrent.futures.

## Running

```bash
export PINECONE_API_KEY=<your_key>
python extracao.py     # generate pages.csv (crawler)
python db.py           # index into Pinecone
python cli.py          # http://localhost:5000
```

## Project status

Functional prototype — full pipeline (crawl → embeddings → index → search); needs more robust error handling and UI polish.

## License

This project does not yet declare a license. Until one is added, all rights are reserved by the author.
