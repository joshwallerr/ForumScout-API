# X (Twitter) Search API

The X Search endpoint allows you to search for posts (tweets) across Twitter's platform.

**Endpoint:** `GET /api/x_search`

## Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| keyword | string | Yes | The search term to find in tweets |
| page | integer | No | Page number for pagination (default: 1) |
| sort_by | string | No | Sort method for results (default: 'Latest') |

## Response Format

```json
[
  {
    "title": "string",
    "url": "string",
    "date": "YYYY-MM-DD HH:MM:SS",
    "author": "string",
    "source": "Twitter (𝕏)",
    "domain": "x.com",
    "snippet": "string"
  }
]
```

## Example Request

```bash
curl -H "X-API-Key: your_api_key_here" \
  "https://forumscout.app/api/x_search?keyword=artificial+intelligence&sort_by=Latest&page=1"
```

```python
import requests

headers = {
    'X-API-Key': 'your_api_key_here'
}

params = {
    'keyword': 'artificial intelligence',
    'sort_by': 'Latest',
    'page': 1
}

response = requests.get(
    'https://forumscout.app/api/x_search',
    headers=headers,
    params=params
)
```

## Example Response

```json
[
  {
    "title": "@techexpert on 𝕏",
    "url": "https://twitter.com/techexpert/status/123456789",
    "date": "2024-03-20 15:30:00",
    "author": "techexpert",
    "source": "Twitter (𝕏)",
    "domain": "x.com",
    "snippet": "The latest breakthroughs in artificial intelligence are transforming..."
  }
]
```

## Sort Options

| sort_by | Description |
|---------|-------------|
| Latest | Sort by most recent posts (default) |
| Top | Sort by engagement and popularity |

## Error Responses

| Status Code | Description |
|-------------|-------------|
| 400 | Missing keyword parameter or invalid page/sort parameter |
| 401 | Missing or invalid API key |
| 402 | Usage limit exceeded - Payment required |
| 429 | Too many requests |
| 500 | Server error |

## Usage Notes

1. Results are paginated with 20 tweets per page
2. The free tier allows 50 requests per month
3. Additional requests are charged at $0.006 per request
4. Date format follows ISO 8601 standard
5. URLs are direct links to individual tweets
6. The source field is marked as "Twitter (𝕏)" to reflect platform branding
7. The title field combines the username with "on 𝕏" for consistency
8. Results include original tweets, retweets, and quote tweets
9. The snippet field contains the full tweet text
10. Pagination uses cursor-based navigation internally
11. URLs use twitter.com domain but domain field reflects x.com
12. Results are returned in chronological order when using 'Latest' sort 
