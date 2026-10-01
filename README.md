# dsa405-project
DSA 405 class semester project for data wrangeling and web scraping. 
# Discord Reviews Data Project — DSA 405

## What this project is

This repository contains the DSA 405 course project, which examines the top,
most-helpful user reviews of the Discord app on the Apple App Store, drawn from
nine different country storefronts. The goal is to analyze this review data's
ratings, review text, timestamps, and app versions to understand patterns in
user feedback across markets.

The project is built in stages: auditing and cleaning the raw data, documenting
its provenance and structure, and then using the cleaned data to answer the
project's analytical questions.

## Where the data came from

The review data was collected from Apple's public iTunes RSS "Customer Reviews" feed
for the Discord app (App Store ID: 985746746), pulled across nine country storefronts
(US, Brazil, Russia, India, UK, Germany, Canada, Australia, New Zealand), sorted by
"most helpful." Full source URLs and the collection date are recorded in
[`data/raw/SOURCES.md`](data/raw/SOURCES.md).

The raw file, `discord_reviews_raw.csv`, is stored unmodified in `data/raw/` and is
never edited or overwritten by any code in this repository — all cleaning happens on
a working copy inside the notebook, with the result saved separately to
`data/cleaned/`.

## How to run it

1. Open the notebook in Google Colab (use the "Open in Colab" button at the top of
   this file, if viewing on GitHub).
2. Run all cells from top to bottom. The notebook reads the raw data directly from
   this repository's GitHub raw URL, so no manual download is required:
```python
   DATA = "https://raw.githubusercontent.com/austinwgross/dsa405/main/data/raw/"
   df_raw = pd.read_csv(DATA + "discord_reviews_raw.csv")
```
3. The notebook will produce the audit output, data dictionary, cleaning log, row/column
   accounting, and provenance brief in sequence, and will save the cleaned dataset to
   `data/cleaned/apple_reviews_cleaned.csv`.

## Repository structure

```
data/
  raw/
    discord_reviews_raw.csv   # original, unmodified scrape
    SOURCES.md                 # where the raw data came from, and when
  cleaned/
    apple_reviews_cleaned.csv  # output of the cleaning notebook
README.md
```
