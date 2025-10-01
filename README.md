# 📚 Somali Wikipedia Corpus  

![Dataset](https://img.shields.io/badge/type-dataset-blue)  
![License: CC BY-SA 3.0](https://img.shields.io/badge/license-CC--BY--SA%203.0-green)

This repository contains a **cleaned and merged dataset** of Somali Wikipedia articles,  
suitable for **NLP, LLM training, and linguistic research**.

---

## 📅 Dataset Coverage

- **Base snapshot:** [Somali Wikipedia](https://so.wikipedia.org/) official Wikimedia dump dated **2025-09-01**  
  (`sowiki-20250901-pages-articles-multistream.xml.bz2`)
- **Live updates:** A subset of pages (≈10–15% of the corpus) was re-fetched directly from the live site on **2025-09-09** to preserve structured information (tables, infoboxes, lists).  

👉 Most content reflects the official dump (Sept 1, 2025), with selected updated content as of Sept 9, 2025.

---

## 📂 Corpus Contents

- **One `.txt` file per article**  
  Each file includes: `title`, `url`, and `text`.

- **`somali_wikipedia_corpus.jsonl`**  
  JSON Lines version (one record per article).  
  Fields: `title`, `url`, `text`.

- **`manifest.csv`**  
  Metadata for each file:  
  - `file` → filename  
  - `title` → article title  
  - `url` → original page link  
  - `word_count` → length of cleaned text  
  - `has_tables` → Markdown tables included  
  - `has_infobox` → infobox preserved  
  - `chosen_from` → source of final version (dump vs scrape)

- **`README.txt`**  
  Local documentation with stats & merge rules.

---

## 🛠️ Extraction & Cleaning Process

1. **Dump extraction**  
   - Used WikiExtractor on 2025-09-01 XML dump.  
   - Removed markup, templates, metadata.  

2. **Targeted live scraping**  
   - Fetched articles with potential tables/infoboxes.  
   - Parsed HTML (BeautifulSoup).  
   - Preserved:  
     - Tables → Markdown  
     - Infoboxes → key–value pairs  
     - Lists → bullets  
     - Captions, categories, coordinates  

3. **Merging strategy**  
   - For each article:  
     1. Prefer version with tables  
     2. Else prefer version with infobox  
     3. Else longer version (higher word count)  
     4. Else fallback to dump text  

---

## 📊 Corpus Statistics

- **Articles:** ~9,500 unique pages  
- **Avg length:** 250–300 words (range: short stubs → 10k+ words)  
- **Tables preserved:** Several hundred pages  
- **Infoboxes preserved:** Most geography & biography pages  
- **Duplicates:** Deduplicated per URL  

📌 Exact stats available in `manifest.csv`.

---

## 🔍 Intended Use

- Training & fine-tuning **Somali LLMs**  
- Developing **NLP tools** (tokenizers, embeddings, classifiers)  
- Research on **low-resource languages**  
- Somali-centric AI applications (translation, chatbots, summarization)

---

## ⚠️ Caveats

- Somali Wikipedia is relatively small; many **short stubs** (1–5 sentences).  
- Complex tables (rowspan/colspan) simplified into Markdown.  
- Some metadata (categories/captions) not exhaustive.  
- **Topic imbalance**: heavy in history, geography, religion.

---

## 📜 License

Somali Wikipedia text is licensed under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/).  
Please attribute **Wikimedia Foundation contributors** when reusing.

---

## 🙌 Acknowledgments

- **Wikimedia Foundation** for hosting & maintaining Wikipedia  
- **Somali Wikipedia contributors** for content creation  
- Dataset prepared by merging the 2025-09-01 official dump with live scraping (Sept 9, 2025)

---

## 📬 Citation

If you use this dataset in research/projects, please cite:

**Somali Wikipedia Corpus (2025)** – merged dump + live scrape.  
Created by *Abdirashid Omar*.


