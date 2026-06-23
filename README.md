[Google Maps Reviews Scraper](https://apify.com/memo23/google-maps-reviews-scraper?fpr=data)

## Overview

Extract all reviews of Google Maps places using place URLs. Get review text, published date, response from owner, review URL, and reviewer's details. Download scraped data, run the scraper via API, schedule and monitor runs or integrate with other tools.

This **Google Maps Reviews Scraper** is a specialized tool designed to extract comprehensive reviews from [Google Maps](https://www.google.com/maps), the world's leading navigation and business listing platform. This scraper delivers rich, structured data encompassing every critical aspect of user reviews to support sentiment analysis, market research, and reputation management.

With this scraper, users gain access to **detailed review information** including ratings, text content, author details, and published dates. The tool captures **comprehensive metadata** with full details about the reviewer and the review context.

**Review specifications** are thoroughly extracted, including review text, star ratings, language detection, and attached images. Author information provides additional context about the reviewer's credibility.

The scraper excels at capturing **review details**, including review IDs, publication times, edit history, and visual content for comprehensive analysis.

Additional **metadata and classification** includes geolocation of images and author profile links for deep-dive investigations.

Whether you're a business owner monitoring reputation, a marketer analyzing customer feedback, or a data scientist performing sentiment analysis, this scraper provides the complete, structured dataset needed for professional-grade insights.

---

## Features

- **Smart Review Extraction**:

- Automatically handles infinite scrolling and pagination
- Extracts both text and rating-only reviews
- **Comprehensive Review Data**:

- Extracts review text, star ratings, and publication dates
- Captures author names, profile IDs, and profile URLs
- Includes review images with high-resolution URLs and captions
- **Efficient Data Extraction**:

- Optimized for speed and reliability using lightweight requests
- Automatically retries failed requests for seamless scraping
- Handles Google's dynamic loading mechanisms
- **Rich Metadata**:

- Extracts language information for each review
- Provides precise timestamps for publication and last edits
- Captures geolocation data from review images where available
- **Dual Data Sources**:

- Primary: Live review data from current place listings
- Fallback: Historical data accessible through deep scrolling

---

## How to Use

1. **Set Up**: Ensure you have an Apify account and access to the Apify platform.
2. **Provide Input Data**: Input specific scraping parameters, such as the Google Maps Place URL.
3. **Adjust Scraper Settings**: Configure settings like `maxItems`, `maxConcurrency`, and `proxy` to optimize performance.
4. **Run the Scraper**: Execute the scraper on the Apify platform.
5. **Download Results**: Export the scraped review data in your preferred format (JSON, CSV, Excel).

### Usage Limitations

**Free Users**: Non-paying users are limited to scraping **10 reviews** per run and can only use **1 start URL**. To access unlimited scraping and all features, please upgrade to a paid Apify account.

**Paid Users**: Enjoy unlimited review scraping, multiple start URLs, and full access to all scraper features.

---

## Input Configuration

To use the scraper, configure the input parameters as follows:

```
{
    "startUrls": [
        {
            "url": "https://www.google.com/maps/place/Eiffel+Tower/@48.8583701,2.2944813,17z/data=!3m1!4b1!4m6!3m5!1s0x47e66e2964e34e2d:0x8ddca9ee380ef7e0!8m2!3d48.8583701!4d2.2944813!16zL20vMDJqODE?entry=ttu"
        }
    ],
    "maxItems": 100,
    "maxConcurrency": 10,
    "minConcurrency": 1,
    "maxRequestRetries": 3,
    "sort": "newest",
    "proxy": {
        "useApifyProxy": true
    }
}
```

### Input Fields Explanation

- **Start URLs** (`startUrls`): The URLs from which the scraper will begin extracting data. The scraper accepts:

- **Place URLs**: Direct links to specific Google Maps places (e.g., `https://www.google.com/maps/place/...`)
- **Review Detail URLs**: Direct links to specific reviews (e.g., `https://www.google.com/maps/reviews/...`)
- **Shortened URLs**: Google Maps mobile short links (e.g., `https://maps.app.goo.gl/...`)
- **Max Items** (`maxItems`): Maximum number of reviews to scrape per run. Default is `100`.
- **Max Concurrency** (`maxConcurrency`): Maximum number of pages processed simultaneously. Default is `10`.
- **Min Concurrency** (`minConcurrency`): Minimum number of pages processed simultaneously. Default is `1`.
- **Max Request Retries** (`maxRequestRetries`): Number of retries for failed requests. Default is `3`.
- **Sort Reviews** (`sort`): Sort order for the reviews. Options: `mostRelevant`, `newest`, `highestRating`, `lowestRating`. Default is `newest`.
- **Language** (`language`): Language code for the reviews (e.g., 'en', 'de', 'es', 'fr'). Default is `en`.
- **Proxy Configuration** (`proxy`): Settings for reliable and anonymous scraping. Default uses Apify's Proxy.

---

## Output Structure

The scraper produces a structured JSON output containing detailed information for each review.

```
{
  "review_id": "ChdDSUhN...",
  "review_url": "https://www.google.com/maps/reviews/data=!4m6!14m5!1m4!2m3!1sChdDSUhN...!2m1!1s0x...",
  "time_published": "2 months ago",
  "time_last_edited": null,
  "author_name": "John Doe",
  "author_profile_url": "https://www.google.com/maps/contrib/...",
  "author_url": "https://www.google.com/maps/contrib/...",
  "author_id": "101012477810529771534",
  "rating": 5,
  "review_text": "Amazing experience! The view was breathtaking.",
  "review_language": "en",
  "images": [
    {
      "id": "...",
      "url": "https://lh3.googleusercontent.com/...",
      "size": {
        "width": 1920,
        "height": 1080
      },
      "location": {
        "friendly": "Paris, France",
        "lat": 48.8584,
        "long": 2.2945
      },
      "caption": "View from the top"
    }
  ],
  "source": "Google",
  "scrapedAt": "2025-01-01T12:00:00.000Z",
  "originalSearchUrl": "https://www.google.com/maps/place/..."
}
```

### Field Descriptions

#### General Information

- **review_id**: Unique identifier for the review.
- **scrapedAt**: Timestamp when the data was extracted.
- **originalSearchUrl**: The URL of the place being scraped.
- **source**: The source of the review (e.g., "Google").

#### Time Information

- **time_published**: Relative time string indicating when the review was posted (e.g., "2 months ago").
- **time_last_edited**: Relative time string indicating when the review was last edited (null if never edited).

#### Author Information

- **author_name**: The name of the reviewer.
- **author_id**: Unique numeric identifier for the reviewer.
- **author_profile_url**: Direct link to the reviewer's Google Maps profile.
- **author_url**: Alternative link to the reviewer's profile.

#### Review Content

- **rating**: Numeric rating given by the reviewer (1-5 stars).
- **review_text**: The actual text content of the review (can be null for rating-only reviews).
- **review_language**: Detected language code of the review text (e.g., "en").

#### Visual Content

- **images**: Array of images attached to the review.

- **id**: Unique identifier for the image.
- **url**: Direct link to the full-resolution image.
- **size**: Object containing `width` and `height` of the image.
- **location**: Object containing `lat`, `long`, and `friendly` name of the image location.
- **caption**: Caption provided for the image (if any).

---

## Benefits of the Google Maps Reviews Scraper

- **Automated Data Collection**: Saves hours of manual copy-pasting and screenshots.
- **High-Quality Data**: Delivers structured, machine-readable JSON for immediate analysis.
- **Scalable Solution**: Capable of scraping thousands of reviews from multiple locations.
- **Sentiment Analysis Ready**: Provides clean text and rating data suitable for NLP models.
- **Reliable Performance**: Built-in retry mechanisms and proxy support ensure consistent results.

---

## Why Choose the Google Maps Reviews Scraper?

The Google Maps Reviews Scraper is an indispensable tool for market researchers, business analysts, and reputation managers. It streamlines the process of gathering customer feedback from one of the world's most trusted sources, enabling you to make data-driven decisions to improve your products and services.

---

## Explore More Scrapers

If you found the Google Maps Reviews Scraper useful, check out other powerful scrapers and actors at [memo23's Apify profile](https://apify.com/memo23). We offer a wide range of tools to enhance your web scraping and automation needs.

---

## Support

- For issues or feature requests, please use the [Issues](https://console.apify.com/actors/ftbw0YFo17iTQ2qjv/issues) section of this actor.
- For further assistance, contact the author:

- Author's website: [https://muhamed-didovic.github.io/](https://muhamed-didovic.github.io/)
- Email: [muhamed.didovic@gmail.com](mailto:muhamed.didovic@gmail.com)

---

## Additional Services

- Request customization or a full dataset: [muhamed.didovic@gmail.com](mailto:muhamed.didovic@gmail.com)
- Need other platforms scraped? Contact [muhamed.didovic@gmail.com](mailto:muhamed.didovic@gmail.com)
- For API services of this scraper, reach out to [muhamed.didovic@gmail.com](mailto:muhamed.didovic@gmail.com)