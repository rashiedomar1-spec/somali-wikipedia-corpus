# Somali Wikipedia Corpus

This repository contains a cleaned and merged text corpus of **Somali Wikipedia**, suitable for use in natural language processing (NLP), large language model (LLM) training, and linguistic research.

---

## 📅 Dataset Coverage

- **Base snapshot:** [Somali Wikipedia](https://so.wikipedia.org/) official Wikimedia dump dated **2025-09-01**  
  (`sowiki-20250901-pages-articles-multistream.xml.bz2`)

- **Live updates:** A subset of pages (≈10–15% of the corpus) was re-fetched directly from the live site on **2025-09-09** to preserve structured information (e.g. tables, infoboxes, lists).  

Thus, most content reflects the official dump from September 1, 2025, with some updated content as of September 9, 2025.

---

## 📂 Corpus Contents

- **One `.txt` file per article**  
  - Includes `title`, `url`, and `text` fields.  
  - Text may contain paragraphs, lists, Markdown tables, infobox entries, captions, categories, and coordinates.  

- **`somali_wikipedia_corpus.jsonl`**  
  - JSON Lines version of the corpus, one record per article.  
  - Fields: `title`, `url`, `text`.

- **`manifest.csv`**  
  - Metadata for every file:  
    - `file`: filename  
    - `title`: article title  
    - `url`: original page link  
    - `word_count`: word count of final text  
    - `has_tables`: whether Markdown tables were included  
    - `has_infobox`: whether infobox entries were preserved  
    - `chosen_from`: which source (dump, upgraded scrape, etc.) provided the final version  

- **`README.txt`**  
  - Local documentation with summary statistics and merge rules.

---

## 🛠️ Extraction & Cleaning Process

1. **Dump extraction**  
   - Used WikiExtractor on the 2025-09-01 Somali Wikipedia XML dump.  
   - Removed markup, templates, and metadata.  

2. **Live scraping (targeted)**  
   - Identified articles with potential tables, infoboxes, or list-heavy structures.  
   - Scraped live HTML using BeautifulSoup to recover structured content.  
   - Preserved:
     - Tables → converted to Markdown format
     - Infoboxes → key–value pairs
     - Lists → bulleted text
     - Captions, categories, and coordinates  

3. **Merging strategy**  
   - For each article (matched by URL/title):
     1. Prefer version with tables.  
     2. Else prefer version with infobox.  
     3. Else prefer longer version (higher word count).  
     4. Else fallback to dump text.  

---

## 📊 Corpus Statistics

- **Articles:** ~9,500 unique pages  
- **Average length:** ~250–300 words (many stubs, some long pages up to 10k+ words)  
- **Tables preserved:** Several hundred pages contain Markdown tables  
- **Infoboxes preserved:** Most biographical and geographic entries include infobox metadata  
- **Duplicates:** Deduplicated at the page level; one version per URL  

*(Exact counts available in `manifest.csv`)*

---

## 🔍 Intended Use

This corpus is intended for:
- Training and fine-tuning Somali language models (LLMs)  
- Developing Somali NLP tools (tokenizers, classifiers, embeddings)  
- Research on low-resource languages and morphological analysis  
- Applications in Somali-centric AI systems (e.g. chatbots, translation, summarization)

---

## ⚠️ Caveats

- Somali Wikipedia is relatively small; many articles are **short stubs** (1–5 sentences).  
- Some structured content (complex tables with rowspan/colspan) may be simplified in Markdown form.  
- Categories, captions, and coordinates are included where available, but may not be exhaustive.  
- This dataset is **not balanced** across topics; heavy on geography, history, and religion.

---

## 📜 License

Somali Wikipedia text is licensed under the [Creative Commons Attribution-ShareAlike License (CC BY-SA 3.0)](https://creativecommons.org/licenses/by-sa/3.0/).  
Please attribute **Wikimedia Foundation contributors** when reusing the dataset.

---

## 🙌 Acknowledgments

- **Wikimedia Foundation** for hosting and maintaining Wikipedia.  
- **Somali Wikipedia contributors** for creating and curating the content.  
- This dataset was prepared by merging the 2025-09-01 official dump with targeted live scraping as of 2025-09-09.

---

## 📬 Contact

If you use this dataset in research or projects, please cite or mention:  
*Somali Wikipedia Corpus (2025), merged dump + live scrape, created by Abdirashid Omar.*

