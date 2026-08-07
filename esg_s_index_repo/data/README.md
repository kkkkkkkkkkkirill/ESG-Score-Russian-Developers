# Data

The original review corpus and intermediate datasets are not distributed in this repository.

The research notebooks reference the following intermediate files produced during the project:

- `avito_reviews_msc_7.csv` — reviews collected from Avito;
- `cian_reviews_optima.csv` — reviews collected from CIAN;
- `cian_zastroischiki_info_all.csv` — developer metadata collected from CIAN;
- `all_reviews_bert.csv` — consolidated review corpus prepared for sentiment modelling;
- `reviews_with_sentiment.csv` — review corpus with sentiment labels / predictions;
- `joined_with_onehot_to_use_final.csv` — final merged analytical dataset used for topic modelling and S-Index experiments.

The full research report in `docs/` describes the collection and preprocessing methodology in detail.

Please note that external website structure may have changed since the research was conducted in 2025, so the scraping notebooks may require selector updates before reproducing the collection step.
