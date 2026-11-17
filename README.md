# Discord Reviews Data Project: DSA 405 (P3)

## What this project is

This project joins Discord's Apple App Store reviews to the EF English Proficiency Index
by country, then checks the join before analyzing it.

Average ratings range from 1.68 stars (Canada) to 4.45 (Germany). The proficiency-band
averages mix countries that differ widely, so the analysis compares countries instead of
bands.

## Where the data came from

| Source | What it is | Access | License / terms |
|---|---|---|---|
| Apple App Store customer reviews (Discord, App ID 985746746) | 499 most-helpful reviews for each of 9 storefronts | Public RSS JSON feed, 10 pages per storefront, 1-second pause between requests | Apple Media Services Terms, Section F. `robots.txt` contains `Disallow: /*/rss/*`, which matches this endpoint |
| EF English Proficiency Index (Wikipedia) | Country proficiency scores and bands | Wikipedia page, fetched once and saved | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) |

Download URLs and dates are in [`data/raw/SOURCES.md`](data/raw/SOURCES.md).

The five native-English storefronts (US, UK, Canada, Australia, New Zealand) are not in the
EF table. The notebook gives them a placeholder score of 700 and the band "Native." These
are not measured scores.

## How to run it

1. Open `DSA405_002_FA26_P3_awgross.ipynb` in Google Colab.
2. Go to **Runtime → Restart session**.
3. Run each cell one at a time, in order from top to bottom. Do not use **Run all**.

Cells 2b, 2d and 3b are assertion demonstrations. They corrupt a copy of the data on purpose
and raise an `AssertionError` to show that the data checks fail loudly. Those two errors
are expected. After each one, continue with the next cell.

The notebook saves its working copies to `data/cache/` inside the Colab session and never
writes to `data/raw/`. If a cached file already exists, the cell loads it instead of
sending a new request. The notebook does not read from GitHub. The files in this
repository's `data/raw/` folder are copies of one run's output, uploaded by hand and not
edited since.

## Repository structure

```
DSA405_002_FA26_P0_awgross.ipynb   # P0 notebook
DSA405_002_FA26_P2_awgross.ipynb   # P2 notebook: audit, cleaning, provenance
DSA405_002_FA26_P3_awgross.ipynb   # P3 notebook: acquisition, cleaning, join, verification, analysis
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

- Each storefront has 499 reviews because the code requests 10 pages. Page 1 includes one
  app-metadata entry, which is dropped, so 49 + 9 × 50 = 499.
data/
  raw/
    discord_reviews_raw.csv   # original, unmodified scrape
    SOURCES.md                 # where the raw data came from, and when
  cleaned/
    apple_reviews_cleaned.csv  # output of the cleaning notebook
README.md
```
