---
layout: default
---

# Rare Disease Wikipedia Pageviews Analysis

## Project Goal
The goal of this project is to analyze Wikipedia page traffic for a subset of articles related to rare diseases from 2015 to 2024 using data collected from the Wikimedia Analytics Pageviews API. Specifically, this project focuses on measuring the traffic for these articles across desktop and mobile platforms, generating several time series datasets, and performing basic visual analysis of the data. The results will help to understand trends and patterns in public interest regarding rare diseases over time.

## Data Source and License
The data for this project is sourced from the [Wikimedia Analytics Pageviews API](https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/reference/page-views.html). The API provides access to page traffic data, including desktop, mobile web, and mobile app views, starting from July 2015 through the most recent complete month.

The data collected through the Wikimedia API is subject to the [Wikimedia Foundation Terms of Use](https://foundation.wikimedia.org/wiki/Terms_of_Use). Under these terms, you are allowed to reuse, adapt, and share the data, provided that proper attribution is given. In this project, the data retrieved is used for analysis purposes, adhering to the license requirements and the attribution guidelines specified.

## API Documentation
To gather the data, the [Pageviews API](https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/reference/page-views.html) was used. This API allows querying for pageviews on specific articles, split by platform (desktop, mobile web, mobile app). The analysis makes use of these API endpoints to collect and organize traffic data from Wikipedia.

## Project Steps
### 1. Data Collection
The project starts by collecting pageview data for Wikipedia articles related to rare diseases. These articles were identified by matching a database of rare diseases maintained by the National Organization for Rare Diseases (NORD) to corresponding Wikipedia articles. The raw dataset containing the rare disease name, pageid and url can be found and downloaded from the repository in the file rare-disease_cleaned.AUG.2024.csv.

Three datasets are generated from the collected data, each representing monthly activity for different access types. All datasets are saved in JSON format with article titles as keys and corresponding time series data as values:

1. **Monthly Mobile Access** (`rare-disease_monthly_mobile_<startYYYYMM>-<endYYYYMM>.json`):
   - Includes pageview data from mobile web and mobile app combined.
2. **Monthly Desktop Access** (`rare-disease_monthly_desktop_<startYYYYMM>-<endYYYYMM>.json`):
   - Includes pageview data from desktop access.
3. **Monthly Cumulative** (`rare-disease_monthly_cumulative_<startYYYYMM>-<endYYYYMM>.json`):
   - Includes cumulative pageview data from both mobile and desktop platforms using access_type = "all-access".

### 2. Data Analysis
The collected data is analyzed to produce the following visualizations:

1. **Maximum and Minimum Average Pageviews**:
   - A time series plot showing the articles with the highest and lowest average pageviews for both desktop and mobile access types. This graph includes four lines: max desktop, min desktop, max mobile, and min mobile.

2. **Top 10 Peak Pageviews**:
   - A time series plot for the articles with the highest peak pageviews, split by desktop and mobile access types. This plot contains the top 10 articles for desktop and the top 10 articles for mobile access, resulting in 20 lines in total.

3. **Fewest Months of Data**:
   - A time series plot for articles with the fewest available months of data, showing the top 10 articles with the least amount of pageview data for both desktop and mobile platforms.

All plots are saved in the `imgs` directory, and they are clearly labeled with legends, axis titles, and appropriate scaling.

### 3. Requirements
To run the project, the following dependencies are required. These dependencies are listed in the `requirements.txt` file:

- `matplotlib==3.8.3` for plotting the visualizations
- `pandas==1.5.3` for data manipulation
- `Requests==2.32.3` for API calls

To install the dependencies, you can run:
```
pip install -r requirements.txt
```

### 4. Data Files
The project creates output files:

- **Output JSON Files** (stored in `datasets/`):
  1. `rare-disease_monthly_mobile_<startYYYYMM>-<endYYYYMM>.json`
  2. `rare-disease_monthly_desktop_<startYYYYMM>-<endYYYYMM>.json`
  3. `rare-disease_monthly_cumulative_<startYYYYMM>-<endYYYYMM>.json`

  Schema for each output JSON is as follows:

  The schema for the generated datasets is as follows:

```{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Generated schema for Root",
  "type": "object",
  "properties": {
    "Klinefelter syndrome": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "project": {
            "type": "string"
          },
          "article": {
            "type": "string"
          },
          "granularity": {
            "type": "string"
          },
          "timestamp": {
            "type": "string"
          },
          "agent": {
            "type": "string"
          },
          "views": {
            "type": "number"
          }
        },
        "required": [
          "project",
          "article",
          "granularity",
          "timestamp",
          "agent",
          "views"
        ]
      }
    }
  }
}```

- **Image Files** (stored in `imgs/`):
  1. `max_min_avg_pageviews.png`
  2. `top_10_peak_pageviews.png`
  3. `fewest_months_data.png`

  Note that for all visualizations, trend lines related to mobile access are denoted as dashed lines (--), while trend lines for desktop access are solid line (-).


### 5. Known Issues and Considerations
- **API Limitations**: The Wikimedia Pageviews API has rate limits, so care must be taken to avoid exceeding these limits when collecting data.
- **Inflation Adjustment**: The analysis does not adjust for inflation in terms of the changing number of internet users, which might affect the interpretation of trends over the years.
- **Data Completeness**: Pageview data is only available from July 2015 onwards. Some articles may have incomplete data for early periods, resulting in discrepancies in analysis.
- **Data Aggregation**: Mobile pageviews are aggregated from mobile web and mobile app separately, which may lead to differences compared to the direct use of an all-access API call.

## Data Availability
The data used in this project is available through the [Wikimedia Analytics Pageviews API](https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/reference/page-views.html). This API provides public access to pageview statistics across multiple Wikimedia projects, following the terms of use of the Wikimedia Foundation.

## License
This project is based on data licensed under the [Wikimedia Foundation Terms of Use](https://foundation.wikimedia.org/wiki/Terms_of_Use), and code samples are licensed under CC-BY, allowing reuse and adaptation with proper attribution.

## Acknowledgements
This project utilized text and code suggestions generated by ChatGPT, developed by OpenAI. GPT-generated code has been marked within the .ipynb file.

For more information on ChatGPT, visit [OpenAI's website](https://openai.com).

