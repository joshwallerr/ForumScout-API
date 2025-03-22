# Forum Search API

The Forum Search endpoint allows you to search for content across various forums and discussion platforms.

**Endpoint:** `GET /api/forum_search`

## Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| keyword | string | Yes | The search term to find in forum content |
| time | string | No | Time filter for results (default: '') |
| country | string | No | Country code to filter results (default: '') |
| page | integer | No | Page number for pagination (default: 0) |

## Response Format

```json
[
  {
    "position": "integer",
    "rank": "string",
    "title": "string",
    "snippet": "string",
    "url": "string",
    "source": "string",
    "domain": "string"
  }
]
```

## Example Request

```bash
curl -H "X-API-Key: your_api_key_here" \
  "https://forumscout.app/api/forum_search?keyword=bitcoin&time=week&country=us&page=0"
```

```python
import requests

headers = {
    'X-API-Key': 'your_api_key_here'
}

params = {
    'keyword': 'bitcoin',
    'time': 'week',
    'country': 'us',
    'page': 0
}

response = requests.get(
    'https://forumscout.app/api/forum_search',
    headers=headers,
    params=params
)
```

## Example Response

```json
[
  {
    "position": 1,
    "rank": "1",
    "title": "Bitcoin Price Discussion",
    "snippet": "Latest analysis of Bitcoin's market performance...",
    "url": "https://example-forum.com/thread/123",
    "source": "Example Forum",
    "domain": "example-forum.com"
  }
]
```

## Time Parameter Options

- `hour` - Last hour
- `day` - Last 24 hours
- `week` - Last 7 days
- `month` - Last 30 days
- `year` - Last year
- Empty string for all time

## Country Parameter

Use ISO 3166-1 alpha-2 country codes (e.g., 'us', 'gb', 'de'). Leave empty for worldwide results.

## Error Responses

| Status Code | Description |
|-------------|-------------|
| 400 | Missing keyword parameter |
| 401 | Missing or invalid API key |
| 402 | Usage limit exceeded - Payment required |
| 429 | Too many requests |
| 500 | Server error |

## Usage Notes

1. Results are paginated with 10 results per page
2. The free tier allows 50 requests per month
3. Additional requests are charged at $0.008 per request
4. Response time may vary based on the scope of the search 
