<img src="img/banner.png" width="100%" alt="Sirius.AI Spring 2024: Review Analysis Tool">

# Review Analysis Tool

A student team project from the **Sirius.AI programme, Spring 2024**. The task: give a bank a way to read thousands of customer reviews without reading them one by one. The tool collects reviews from public review sites, scores how positive each one is, and groups them into topics so recurring complaints become visible.

<p>
  <img src="img/logo1.png" height="56" alt="Sirius.AI logo">
  &nbsp;&nbsp;
  <img src="img/logo2.png" height="56" alt="Logo of the partner bank">
</p>

## What it does

| Stage | What happens | Where |
|:--|:--|:--|
| **Collect** | Reviews are scraped from banki.ru (plain GET requests, BeautifulSoup) and sravni.ru (Selenium with ChromeDriver, because the page loads reviews on scroll). | `second_stage/theme5.ipynb`, `second_stage/level2/sravnyParser.py` |
| **Clean** | HTML control characters are stripped, text is lower-cased, punctuation and Russian stop words removed, words stemmed. | `second_stage/theme5.ipynb`, `second_stage/level2/Main.py` |
| **Score sentiment** | Each review is sent to a locally hosted LLM, which answers with a score from 1 to 100. Reviews at 80 and above count as positive. | `fo_sir_tink/localSemantic.py` |
| **Find topics** | Reviews are vectorised with TF-IDF and clustered into 10 groups with KMeans. For each cluster the tool picks the most central review, the five closest ones and a word cloud. | `second_stage/level2/Main.py` |
| **Report** | Results are written to an HTML report, an Excel sheet and word-cloud images. | `second_stage/level2/cluster_analysis.html`, `fo_sir_tink/weutput.xlsx` |

The first stage used the **Zephyr 7B beta (Q4_K_S)** model, served locally by LM Studio and called from Python through its OpenAI-compatible endpoint. No review text leaves the machine.

## Result

The repository contains the finished output of a run on 100 reviews from sravni.ru:

- `second_stage/level2/cluster_analysis.html`: the topic report, one section per cluster
- `second_stage/level2/cluster_*_wordcloud.png`: a word cloud for each of the 10 clusters
- `presentationforsirius.pdf`: the 22-slide project presentation (in Russian)

Sentiment was only scored in the first stage. For the clustering stage we decided against it: doing it well for Russian text needs a BERT-class model, which was out of scope.

<p>
  <img src="img/im4.png" width="49%" alt="LM Studio serving the model on a local port">
  <img src="img/img7.png" width="49%" alt="Table with the problem the model extracted from each review">
</p>
<p>
  <img src="img/img11.png" width="49%" alt="Merged table of reviews from both sources">
  <img src="second_stage/level2/cluster_0_wordcloud.png" width="49%" alt="Word cloud of one topic cluster">
</p>

## Team

A team of four:

- Pavel Konchakov (me)
- Ilya Grigoryev
- Vladimir Aksenov
- Dmitry Dyrkov

## Stack

Python · pandas · scikit-learn (TF-IDF, KMeans) · NLTK · wordcloud · matplotlib · Selenium · BeautifulSoup · FastAPI · LM Studio with Zephyr 7B

## How to run

**Topic clustering (works offline, data included)**

```bash
cd second_stage/level2
pip install pandas numpy scikit-learn nltk wordcloud matplotlib
python Main.py          # reads sravni.json, writes cluster_analysis.html and the word clouds
```

**Sentiment scoring (needs a local model)**

1. Install [LM Studio](https://lmstudio.ai), download `zephyr-7b-beta` (Q4_K_S) and start the local server on port 1234.
2. Run the script:

```bash
cd fo_sir_tink
pip install pandas numpy matplotlib seaborn wordcloud fastapi openpyxl "openai<1"
python localSemantic.py   # reads samples.csv, writes positive_reviews.txt and negative_reviews.txt
```

`table_excel_load.py` exports the reviews with the detected problems to Excel, `wordcloud_base.py` builds the word clouds only.

**Scraping fresh reviews**

```bash
cd second_stage/level2
pip install selenium webdriver-manager
python sravnyParser.py    # opens Chrome and collects 100 reviews into sravni.json
```

The scrapers depend on the markup of the review sites as it was in March 2024 and may need new selectors today.

## Repository layout

```
fo_sir_tink/            Stage 1: sentiment scoring with a local LLM, Excel export, word clouds
second_stage/
  theme5.ipynb          Stage 2 notebook: banki.ru scraper, merging and cleaning
  level2/               Stage 2 scripts: sravni.ru scraper, clustering, generated report
img/                    Screenshots used in this README
presentationforsirius.pdf
```
