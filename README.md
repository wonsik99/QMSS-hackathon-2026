# QMSS Hackathon 2026 — Water quality rhetoric on Reddit

Team project: collect Reddit posts about **water** under two contrasting search framings, run **VADER** sentiment analysis, compare groups statistically, and visualize results.

## What’s in this repo

| Item | Description |
|------|-------------|
| `hackathon_health_sentiment.ipynb` | Main pipeline: PRAW → preprocess → VADER → plots → tests → CSV export |
| `hackathon_water_slides.html` | Short Reveal.js slide deck (open in a browser; same folder as the PNGs) |
| `output1_wordcloud.png` … `output4_sentiment_trend.png` | Figures saved by the notebook |
| `health_reddit_raw.csv` | Scraped posts (metadata + title/body) |
| `health_reddit_sentiment.csv` | Same rows + sentiment columns |
| `Scrapping_Reddit_2.ipynb` | Earlier Reddit/PRAW exploration (Student Loans, etc.) |

## Requirements

- Python 3.10+ (3.12 works)
- Reddit API app: [reddit.com/prefs/apps](https://www.reddit.com/prefs/apps) — type **script**

Install dependencies (from the notebook, or):

```bash
pip install praw vaderSentiment wordcloud matplotlib seaborn pandas scipy
```

## Credentials (do not commit secrets)

1. Copy `.env.example` to `.env` and fill in `REDDIT_CLIENT_ID` and `REDDIT_CLIENT_SECRET`.
2. Load env vars before Jupyter, for example:

```bash
export REDDIT_CLIENT_ID="your_id"
export REDDIT_CLIENT_SECRET="your_secret"
export REDDIT_USER_AGENT="hackathon-water-sentiment/1.0 by /u/your_username"
jupyter notebook hackathon_health_sentiment.ipynb
```

Or use a tool like `direnv` / IDE env loading so the kernel sees the variables.

**Optional:** `pip install python-dotenv`, then add at the top of the credentials cell (or the imports cell):

```python
from dotenv import load_dotenv
load_dotenv()  # loads .env from the working directory
```

**If these keys were ever committed in plain text, rotate them in Reddit app settings.**

## How to run

1. Set environment variables as above.
2. Open `hackathon_health_sentiment.ipynb` and run all cells from the top.
3. Re-scraping overwrites the CSVs and PNGs in this folder.

Slides: from the repo root, open `hackathon_water_slides.html` in a browser (images load via relative paths).

## Methods (short)

- **Source:** `r/all` search, up to 100 posts per query, title + selftext (no comments).
- **Topics:** `water_pollution` (contamination / health-risk queries) vs `water_access` (access / charity / filter-style queries).
- **Sentiment:** VADER `compound` (−1 to +1); labels at ±0.05.
- **Stats:** Welch’s *t*-test, Mann–Whitney U, Cohen’s *d*.

## Limitations

- Results depend heavily on **which search strings** you use (selection bias).
- VADER is weak on irony and long technical context.
- Respect [Reddit API terms](https://www.reddit.com/wiki/api) and do not redistribute data in ways that violate them.

## License

Add a license if your course or team requires one (e.g. MIT).
