# Getting started with the ForumScout API

This guide will help you get started, generate your API key, and make your first API request.

## Overview

The ForumScout API lets you search forum posts using the `/api/forum_search` endpoint. Every registered developer gets **50 free requests per month**. If you exceed this quota, a Stripe subscription is automatically created to meter additional usage at **$0.008 per request**.

## Authentication

All API calls require you to include your unique API key in the `X-API-Key` header. You can generate (or regenerate) your API key from the [Developer Dashboard](https://forumscout.app/developers).

## Example Request in Python

Make sure you have the [requests](https://pypi.org/project/requests/) library installed:

```bash
pip install requests
```

Then use the following code snippet to perform your first forum search request:

```python
import requests

# Replace with your actual API key (you can get this from your Developer Dashboard)
api_key = "YOUR_API_KEY_HERE"

# The endpoint URL
url = "https://forumscout.app/api/forum_search"

# Define your query parameters
params = {
    "keyword": "python",  # The search keyword
    "time": "any",        # Time filter (e.g., "any" or a specific value)
    "country": "us",      # Country code (optional)
    "page": 0             # Pagination (default is 0)
}

# Set the headers, including your API key
headers = {
    "X-API-Key": api_key
}

# Make the GET request
response = requests.get(url, headers=headers, params=params)

if response.status_code == 200:
    data = response.json()
    print("Search Results:")
    print(data)
else:
    print("Error:", response.status_code, response.text)
```

To get the next page of results, you can repeat the request and increment the `page` parameter by 1:

```python
params = {
    "keyword": "python",
    "time": "any",
    "country": "us",
    "page": 1             # Incremented by 1 for the next page
}
```

If you get less than 10 results in any request, it means you've hit the last page of results for that query.

## Response Structure
A successful API call will return a JSON object with your search results. For example:

```json
[
  {
    "domain": "www.reddit.com",
    "position": 1,
    "rank": 1,
    "snippet": "I built a platform called Forumscout that tracks Reddit, X, YouTube, LinkedIn, and Instagram. It's free if you get less than 100 mentions ...",
    "source": "Reddit",
    "title": "Best social listening tool out there? : r/digital_marketing - Reddit",
    "url": "https://www.reddit.com/r/digital_marketing/comments/1iof8mz/best_social_listening_tool_out_there/"
  },
  {
    "domain": "www.quora.com",
    "position": 2,
    "rank": 2,
    "snippet": "ForumScout is probably the best forum search engine I've found out there. All the others seem to be broken in some way or have very limited ...",
    "source": "Quora",
    "title": "Is there a reliable search engine that I can use to perform ...",
    "url": "https://www.quora.com/Is-there-a-reliable-search-engine-that-I-can-use-to-perform-searches-on-discussion-boards-forums-message-boards"
  },
  ...
]
```

## Support

For all questions and issues, email me at josh@forumscout.app.
