# Greenhouse Jobs Scraper: Python example

**Greenhouse Jobs, Lever, SmartRecruiters Scraper.** Live jobs from a company's Greenhouse, Lever, Ashby or SmartRecruiters board, with salary and Canadian province tags. Price, example input and output, and FAQ: [Greenhouse Jobs Scraper on the Aurelix tools site](https://aurelix-solutions.github.io/tools/greenhouse-jobs-scraper/). Run it on the Apify Store: [apify.com/aurelix/greenhouse-jobs-scraper](https://apify.com/aurelix/greenhouse-jobs-scraper).


**The problem:** You want every open job at a list of companies, read straight from their Greenhouse, Lever, Ashby or SmartRecruiters careers pages, without checking each page by hand.

**The tool:** [Greenhouse Jobs Scraper](https://apify.com/aurelix/greenhouse-jobs-scraper), an Apify Actor by Aurelix. This repository is a small, runnable Python example for it.

**The price:** $1.50 per 1,000 jobs on Apify's free plan and $1.05 on paid plans, plus $0.00005 per run; you pay only for results. Apify's free plan includes $5 of credit a month.

**Try it** (needs an Apify API token from Console > Settings > API & Integrations):

```bash
pip install -r requirements.txt
export APIFY_TOKEN=your_token_here
python main.py
```

[![Greenhouse Jobs Scraper: 75-second demo video](https://api.apify.com/v2/key-value-stores/twkCCtTWzsi8fVbx5/records/greenhouse-jobs-scraper-demo-thumb-v1.png)](https://api.apify.com/v2/key-value-stores/twkCCtTWzsi8fVbx5/records/greenhouse-jobs-scraper-demo-v1.mp4)

**[▶ Watch the 75-second demo](https://api.apify.com/v2/key-value-stores/twkCCtTWzsi8fVbx5/records/greenhouse-jobs-scraper-demo-v1.mp4)**

## What it does

Greenhouse Jobs Scraper collects live job postings directly from employers' own career sites, using the official public job-board APIs of Greenhouse, Lever, Ashby and SmartRecruiters, not a stale database. Give it company boards (greenhouse:geotab, a jobs.ashbyhq.com link, lever:pointclickcare) or a bundled starter list and get one clean schema: title, department, locations, country, Canadian province, remote/hybrid/on-site, salary range when published, posted date and apply link. Turn on new-jobs-only mode for a daily feed of postings you have not seen.

## Why this over alternatives

Compared with the leading alternatives on the Apify Store (full table on the Store page):

- $1.50 per 1,000 jobs: 40% under the leading career-site job feed and 8x cheaper than the leading jobs API ($12).
- Type a company domain and it finds the employer's board, read live at run time, with a new-since-last-run mode. Covers 4 ATS platforms to their 58.

## When to use it

- Job boards and aggregators adding direct-from-employer postings every day with the new-jobs-only mode
- Recruiters watching target companies for new openings
- Canadian job sites using the Canada-only filter and province codes
- HR and market analysts tracking hiring by company, team and salary band

## Input example

This is the `canadian-tech-jobs` input used in `main.py`:

```json
{
  "starterList": "canada",
  "canadaOnly": true
}
```

Every input field is documented on the [Store page](https://apify.com/aurelix/greenhouse-jobs-scraper).

## How to run

1. Get an Apify API token from Apify Console (Settings, API & Integrations).
2. Install and run:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
export APIFY_TOKEN=your_token_here
python main.py
```

The script starts a run of `aurelix/greenhouse-jobs-scraper`, prints a few fields from the first results and writes every result to `results.csv`. Lists and nested objects are stored in the CSV as JSON text. Each run is billed to your Apify account (see Pricing below).

## Sample output

One record as returned by a real run (long text is shortened):

```json
{
  "job_id": "lever:pointclickcare:76cdab93-644a-47d6-a89d-9c4add288692",
  "ats": "lever",
  "company_token": "pointclickcare",
  "company": "PointClickCare",
  "title": "(Canada) Sales Development Representative (6 month contract)",
  "department": "Acute & Payer",
  "team": "Sales",
  "locations": [
    "Remote or Mississauga"
  ],
  "countries": [
    "CA"
  ],
  "provinces": [
    "ON"
  ],
  "is_canada": true,
  "remote": true,
  "workplace_type": "remote",
  "employment_type": "CONTRACT",
  "employment_type_raw": "Contract",
  "salary_min": 29,
  "salary_max": 31,
  "salary_currency": "CAD",
  "salary_interval": "hour",
  "salary_text": "This is contract role paid in an hourly rate, based on a 40 hour work week. The offer is $29 - 31CAD per hour, and is not eligible for benefits or paid time off. You will receive another 4% per hour in lieu of these benefits. Your recruiter can share more information about the terms during the hirin... [11 more characters]",
  "posted_at": "2026-10-13T20:52:35Z",
  "updated_at": "2026-10-13T20:52:35Z",
  "apply_url": "https://jobs.lever.co/pointclickcare/76cdab93-644a-47d6-a89d-9c4add288692/apply",
  "description_text": "The Role: As an entry-level sales position, the Sales Development Representative (SDR) will support a Senior Sales Executive and be responsible for day-to-day interactions with our prospective customers in the health care industry. The SDR, as part of a larger team, plays a major role in the company... [2271 more characters]",
  "description_html": "<div data-qa=\"job-description\">\n<div>The Role: As an entry-level sales position, the Sales Development Representative (SDR) will support a Senior Sales Executive and be responsible for day-to-day interactions with our prospective customers in the health care industry. The SDR, as part of a larger te... [3459 more characters]",
  "source_url": "https://jobs.lever.co/pointclickcare/76cdab93-644a-47d6-a89d-9c4add288692",
  "scraped_at": "2026-11-04T11:17:28Z"
}
```

## Export to CSV

`main.py` writes `results.csv` with the `csv` module. You can also download any run's results directly:

```
https://api.apify.com/v2/datasets/<datasetId>/items?format=csv&clean=true
```

Send your token in an `Authorization: Bearer <token>` header (or `?token=`) if the dataset is not readable without one. Other formats: `format=json`, `format=xlsx`.

## Google Sheets

- Simplest: use Apify's Google Sheets integration on the Actor or a saved task, so each run's results land in a sheet with no token in the sheet itself.
- Quick pull of one run: `=IMPORTDATA("https://api.apify.com/v2/datasets/<datasetId>/items?format=csv&clean=true")`. This only works without a token if your account lets anyone with the dataset ID read it. Do not paste an API token into a sheet formula: anyone who can view or copy the sheet can read it and use your account.

## n8n

- Apify node: choose "Run an Actor", enter `aurelix/greenhouse-jobs-scraper`, paste the input above, then read the run's dataset items.
- HTTP Request node: `POST https://api.apify.com/v2/acts/aurelix~greenhouse-jobs-scraper/run-sync-get-dataset-items` with header `Authorization: Bearer <token>` (stored as an n8n credential) and the input as the JSON body. The response is the list of results. This endpoint waits for the run to finish, so for large runs start the run asynchronously and fetch the dataset when it ends.

## Limits

- You need the company's board token or URL; the bundled starter list covers 49 verified employers (25 Canadian). There is no search across all companies.
- Only Greenhouse, Lever, Ashby and SmartRecruiters boards. Workday, iCIMS, Taleo and custom career sites are not covered.
- Country and province are detected from text when the ATS gives none; unusual location strings can be missed.
- Lever and Ashby do not publish an 'updated' time, so updated_at equals posted_at there. Lever has no company display name; the token is used unless the company is in the starter list.
- SmartRecruiters needs one extra request per job for the description; turn descriptions off for very large boards.
- 'Max jobs per company' is applied before the 'new since last run' filter.

## Pricing

At the time of writing:

Pay per event: you pay only for what the run returns, plus a small start fee. Bronze, Silver, Gold and higher Apify plans pay less per result.

| Event | Free plan | Paid plans (Bronze, Silver, Gold) |
|---|---|---|
| `job-result` | $1.50 per 1,000 jobs | $1.05 per 1,000 jobs |
| `apify-actor-start` | $0.00005 per run | $0.00005 per run |

Example: 1,000 jobs cost $1.50 on the free plan and $1.05 on a paid plan, plus the start fee. Apify's free plan includes $5 of credit a month, enough for about 3,300 jobs.

No charge for boards that return nothing.

Check the [Store page](https://apify.com/aurelix/greenhouse-jobs-scraper) for current prices.

## Links

- Actor: https://apify.com/aurelix/greenhouse-jobs-scraper
- Questions, bugs and feature requests: the Issues tab on the Store page.

## Licence

The example code in this repository is released under the MIT licence (see `LICENSE`). The Actor itself runs on Apify and is billed through your Apify account.
