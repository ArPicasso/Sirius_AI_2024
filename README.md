# **Sirius AI** Spring 2024

<p float="left">
  <img src="https://github.com/z1nex-1/Sirius_AI/blob/main/img/logo1.png" width="300" />
  <img src="https://github.com/z1nex-1/Sirius_AI/blob/main/img/logo2.png" width="150" />
</p>

## A Tool for Analyzing Customer Reviews

### Project Team:

- Konchakov Pavel (Me)
- Grigoryev Ilya
- Aksenov Vladimir
- Dyrkov Dmitry

________

# Phase 1

For the first stage, we chose to use the **zephyr beta 7B Q4_K_S** model.

We launch it in **LM Studio**, and then connect to it from our Python program via the local server.

## Demo

<p float="left">
  <img src="https://github.com/z1nex-1/Sirius_AI/blob/main/img/im4.png" width="500" />
  <img src="https://github.com/z1nex-1/Sirius_AI/blob/main/img/img5.png" width="500" />
</p>

## Result

<p float="left">
  <img src="https://github.com/z1nex-1/Sirius_AI/blob/main/img/img6.png" width="500" />
  <img src="https://github.com/z1nex-1/Sirius_AI/blob/main/img/img7.png" width="500" />
</p>

## Video Demo for Phase 1

<p float="left">
  <img src="https://github.com/z1nex-1/Sirius_AI/blob/main/img/qr.png" width="300" />
</p>

________________________________

# Phase 2

### Below is a detailed description of Phase 2

## Implementation Plan:
1. Data collection
2. Cleaning and structuring the data for analysis
3. Feature extraction

## Data Collection

### We used two types of parsers from two sources:

| Website         | banki.ru             | sravni.ru                             |
|----------------|:--------------------:|:-------------------------------------:|
| Tools Used     | **bs4** and **urllib** | **selenium** and **webdriver_manager** |
| How It Works   | Simple **GET** requests | Automated browsing with **ChromeDriver** |

<p float="left">
  <img src="https://github.com/z1nex-1/Sirius_AI/blob/main/img/img8.png" width="450" />
  <img src="https://github.com/z1nex-1/Sirius_AI/blob/main/img/img9.png" width="550" />
</p>

## Data Processing

+ The banki.ru parser required additional HTML character cleanup.
+ The sravni.ru parser outputs clean data, so no post-processing was needed.

<p float="left">
  <img src="https://github.com/z1nex-1/Sirius_AI/blob/main/img/img10.png" width="500" />
  <img src="https://github.com/z1nex-1/Sirius_AI/blob/main/img/img11.png" width="500" />
</p>

## Feature Extraction

+ We performed text preprocessing: stopword removal, lemmatization/stemming, punctuation removal.

<p float="left">
  <img src="https://github.com/z1nex-1/Sirius_AI/blob/main/img/img12.png" width="1000" />
</p>

+ Converted review texts into vector representations using NLP techniques such as TF-IDF.

<p float="left">
  <img src="https://github.com/z1nex-1/Sirius_AI/blob/main/img/img13.png" width="1000" />
</p>

## Review Analysis & Interpretation

+ Using the extracted features, we identified topics and trends in the reviews. We performed clustering into 10 clusters.
+ Sentiment analysis was **not** performed — it requires more advanced models like BERT, and handling Russian language adds complexity.

This analysis is exported as an HTML file by our program (clustering by 10 topics instead of 4).

### For more details, see the **presentationforsirius.pdf** file

______

# Conclusion

### See you on April 1st at 13:00!

_____
# Repository Contents

+ `fo_sir_tink` — all files for Phase 1, including:
  + `req.txt` — requirements
  + `localSemantic.py` — semantic analysis and sentiment separation
  + `table_excel_load.py` — exporting reviews to Excel
  + `wordcloud_base.py` — word cloud generation

+ `second_stage` — all files for Phase 2:
  + `level2/` — parser for **sravni.ru** and test Python scripts
  + `theme5.ipynb` — Jupyter notebook with **banki.ru** parser and text processing
  + `LICENSE.chromedriver` — license for ChromeDriver used in sravni.ru parsing

+ `img/` — images used in README
+ `presentationforsirius.pdf` — project presentation
