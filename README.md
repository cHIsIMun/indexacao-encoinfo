# indexacao-encoinfo

🇧🇷 Português | 🇺🇸 [English](README.en.md)

> Busca semântica de páginas web por embeddings: faz crawl de um site, indexa no Pinecone e responde por similaridade via interface Flask.

## Visão geral

Sistema de **busca semântica** sobre páginas web. Faz *web scraping* de um site, gera **embeddings** de cada página com Sentence Transformers, indexa os vetores no **Pinecone**, e oferece uma interface Flask que responde consultas por similaridade vetorial (em vez de busca por palavra-chave).

## Pipeline

1. **`extracao.py`** — *crawler* que limpa o HTML e gera `pages.csv`.
2. **`db.py`** — carrega o CSV, gera embeddings (`all-MiniLM-L6-v2`) e faz *upsert* em lotes no Pinecone.
3. **`cli.py`** — app Flask: a busca consulta o Pinecone e faz *fetch* paralelo dos títulos (30 threads), retornando scores de similaridade.

## Stack

Python · sentence-transformers (all-MiniLM-L6-v2) · Pinecone · Flask · requests · pandas · concurrent.futures.

## Como executar

```bash
export PINECONE_API_KEY=<sua_chave>
python extracao.py     # gera pages.csv (crawler)
python db.py           # indexa no Pinecone
python cli.py          # http://localhost:5000
```

## Estado do projeto

Protótipo funcional — pipeline completo (crawl → embeddings → índice → busca); faltam tratamento de erros mais robusto e refino da interface.

## Licença

Este projeto ainda não declara uma licença; até que uma seja adicionada, todos os direitos são reservados ao autor.
