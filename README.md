# multi-source-research

Search 13 academic and technical sources in one command.

No API keys needed for most sources. Results ranked by relevance, deduplicated, returned as structured JSON or markdown.

> 🇮🇹 [Versione italiana disponibile in fondo](#versione-italiana)

---

## Sources

| Source | Type | Access |
|--------|------|--------|
| arXiv | Preprints (CS, Physics, Math, AI) | Free |
| Semantic Scholar | Academic graph, 200M+ papers | Free |
| OpenAlex | Open academic metadata | Free |
| BASE | Bielefeld Academic Search Engine | Free |
| GitHub | Code repositories | Free (rate-limited) |
| Unpaywall | Open-access versions of paywalled papers | Free |
| POLITesi | Politecnico di Milano theses | Free |
| CrossRef | DOI metadata, citations | Free |
| CORE | Open research papers | Free |
| PubMed | Biomedical literature | Free |
| Internet Archive | Historical and digitized texts | Free |
| CNKI (partial) | Chinese academic literature | Free preview |
| Baidu Scholar (partial) | Chinese research | Free preview |

---

## Quick start

```bash
pip install requests beautifulsoup4 aiohttp
```

```bash
# Search across all sources
python research_agent.py "transformer attention mechanism efficiency"

# Limit sources
python research_agent.py "query" --sources arxiv semantic_scholar github

# Save results
python research_agent.py "query" --output results.json

# Top N results per source
python research_agent.py "query" --top 5
```

---

## Output

```json
{
  "query": "transformer attention efficiency",
  "results": [
    {
      "source": "arxiv",
      "title": "FlashAttention: Fast Memory-Efficient Exact Attention...",
      "authors": ["Dao", "Fu", "Ermon", "Rudra", "Re"],
      "year": 2022,
      "url": "https://arxiv.org/abs/2205.14135",
      "abstract": "...",
      "relevance_score": 0.94
    }
  ],
  "total": 47,
  "sources_queried": 13,
  "elapsed_sec": 4.2
}
```

---

## Architecture

Queries run in parallel (`asyncio` + `aiohttp`). Each source has an independent adapter. Results are deduplicated by title similarity before ranking.

---

## Changelog

| Version | Date | Status |
|---------|------|--------|
| **v1.1** | 2026-05-28 | **ACTIVE** — 13 sources, async parallel, dedup |
| v1.0 | 2026-04 | REPLACED by v1.1 — 8 sources, sequential |
| v0.1 | 2026-03 | REPLACED by v1.0 — arXiv + Semantic Scholar only |

---

## Part of

[TITANIUM_OS](https://github.com/Microindustry/TITANIUM_OS) — personal cognitive OS.
Full source: `NODES/RESEARCH_AGENT/research_agent.py`

---

## Versione italiana

Cerca su 13 fonti accademiche e tecniche con un solo comando.

Nessuna API key necessaria per la maggior parte delle fonti. Risultati ordinati per rilevanza, deduplicati, restituiti come JSON o markdown.

**Fonti principali:** arXiv, Semantic Scholar, OpenAlex, BASE, GitHub, Unpaywall, CrossRef, CORE, PubMed, Internet Archive, POLITesi, CNKI (parziale), Baidu Scholar (parziale).

**Architettura:** le query girano in parallelo (`asyncio` + `aiohttp`). Ogni fonte ha un adattatore indipendente. I risultati vengono deduplicati per similarità del titolo prima del ranking.

Codice sorgente: [TITANIUM_OS](https://github.com/Microindustry/TITANIUM_OS) → `NODES/RESEARCH_AGENT/research_agent.py`
