# Raw data sources

All files in this folder come from one run of the P3 notebook and were uploaded by hand. They are not edited after upload.

## discord_reviews_multi_country_raw.json and discord_reviews_raw.csv

- **Source:** Apple iTunes RSS "Customer Reviews" feed for the Discord app (App Store ID: 985746746)
- **URL pattern:** `https://itunes.apple.com/{country_code}/rss/customerreviews/page={page}/id=985746746/sortby=mostHelpful/json`
- **Country codes used:** us, br, ru, in, gb, de, ca, au, nz
- **Pages per country:** 1 through 10 (the code requests 10 pages per storefront)
- **Contents:** 4,491 reviews, 499 per storefront. The JSON and the CSV hold the same records.
- **Example single request:** `https://itunes.apple.com/us/rss/customerreviews/page=1/id=985746746/sortby=mostHelpful/json`
- **Date downloaded:** [REPLACE WITH THE DATE YOU RAN THE NOTEBOOK]

## wikipedia_ef_epi_raw.html and wiki_ef_epi_uncleaned.csv

- **Source:** English Wikipedia, "EF English Proficiency Index" (data from EF Education First)
- **URL:** `https://en.wikipedia.org/wiki/EF_English_Proficiency_Index`
- **Contents:** The HTML file is the page as downloaded. The CSV is the country ranking table (123 rows) parsed from that page.
- **License:** CC BY-SA 4.0
- **Date downloaded:** [REPLACE WITH THE DATE YOU RAN THE NOTEBOOK]
