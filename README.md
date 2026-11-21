# Discord Reviews Data Project: DSA 405 (P4)

## What this project is

This project investigates whether user sentiment in Discord's Apple App Store reviews declines after major software updates, using regional English proficiency as a secondary demographic control. It joins 4,491 Discord iOS reviews across 9 storefronts to the EF English Proficiency Index by country, translates non-English reviews locally on a GPU, and runs text classification and Named Entity Recognition (NER).

Average ratings range from 1.68 stars (Canada) to 4.45 (Germany). Because proficiency-band averages mix countries that differ widely, the analysis compares individual countries and review text rather than broad proficiency bands.

### Key findings

* **UI redesigns drive negative sentiment:** Negative reviews (1-2 stars, $n = 1,780$) focus heavily on post-update interface backlash, led by *update* (28.0% vs. 16.1% in other groups), *new* (28.0% vs. 13.8%), and *ui* (14.5% vs. 1.9%). Positive reviews (4-5 stars, $n = 2,175$) highlight everyday social features like *friend* (28.6%) and *chat* (16.6%).
* **Product UX outweighs regional demographics:** A text-only TF-IDF classifier achieves **81.54%** binary accuracy (0.8877 ROC-AUC) separating negative and positive reviews, while regional English proficiency (`ef_score`) performs near chance at **54.99%** and adds **-0.13%** lift.
* **Neutral reviews reflect bug reports:** Including neutral 3-star reviews ($n = 512$) drops 3-class accuracy to **65.44%** (20.4% neutral recall), largely because neutral ratings come from otherwise positive users reporting technical issues they want fixed (*fix* at 26.0%).

## Where the data came from

| Source | What it is | Access | License / terms |
| --- | --- | --- | --- |
| Apple App Store customer reviews (Discord, App ID 985746746) | 499 most-helpful reviews for each of 9 storefronts (4,491 total) | Public RSS JSON feed, 10 pages per storefront, 1-second pause between requests | Apple Media Services Terms, Section F. `robots.txt` contains `Disallow: /*/rss/*`, which matches this endpoint |
| EF English Proficiency Index (Wikipedia) | Country proficiency scores and bands | Wikipedia page, fetched once and saved | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) |

Download URLs and dates are in [`data/raw/SOURCES.md`](https://www.google.com/search?q=data/raw/SOURCES.md).

The five native-English storefronts (US, UK, Canada, Australia, New Zealand) are not in the EF table. The notebook gives them a placeholder score of `700` and the band `"Native"`. These are not measured scores.

## How to run it

The notebook links directly to the cached raw data files already saved in this repository, so you only need to download the notebook file itself:

1. Download `DSA405_002_FA26_P4_awgross.ipynb` from this repository.
2. Upload the notebook to **Google Colab**.
3. Switch the Colab runtime to **T4 GPU** (**Runtime → Change runtime type → T4 GPU**) to run the local language translation model.
4. Click **Run All** to execute the entire notebook from start to finish.

The notebook pulls the cached files from `data/raw/` in this GitHub repository and saves working copies inside the Colab session without re-querying live endpoints. Defensive unit tests are included to verify error handling and score bounds cleanly during execution.

## Repository structure

```
DSA405_002_FA26_P0_awgross.ipynb   # P0 notebook
DSA405_002_FA26_P2_awgross.ipynb   # P2 notebook: audit, cleaning, provenance
DSA405_002_FA26_P3_awgross.ipynb   # P3 notebook: acquisition, cleaning, join, verification, analysis
DSA405_002_FA26_P4_awgross.ipynb   # P4 notebook: GPU translation, NLP/TF-IDF modeling, NER, final analysis
data/
  raw/
    SOURCES.md                              # download URLs and dates
    discord_reviews_multi_country_raw.json  # Apple feed, all storefronts
    discord_reviews_raw.csv                 # Apple feed, flattened to CSV
    wikipedia_ef_epi_raw.html               # Wikipedia page
    wiki_ef_epi_uncleaned.csv               # EF table as parsed from the page
README.md

```

## Notes

* Each storefront has 499 reviews because the code requests 10 pages. Page 1 includes one app-metadata entry, which is dropped, so `49 + 9 × 50 = 499` reviews per storefront (`4,491` total across 9 storefronts).
* After translating non-English reviews into English, 24 reviews containing only emojis or symbols (leaving zero alphabetic tokens) were filtered out, leaving `4,467` clean reviews for machine learning.
* Because the Apple RSS feed does not pair reviews with exact app release timestamps, post-update sentiment drops are inferred from user vocabulary (*update*, *new ui*, *revert*) rather than a strict before-and-after release timeline.
