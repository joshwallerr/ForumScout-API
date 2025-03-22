# Instagram Search API

The Instagram Search endpoint allows you to search for posts and content across Instagram's platform.

**Endpoint:** `GET /api/instagram_search`

## Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| keyword | string | Yes | The search term to find in Instagram posts (hashtags will be cleaned of spaces/quotes) |
| page | integer | No | Page number for pagination (default: 1) |
| sort_by | string | No | Sort method for results (default: 'recent') |

## Response Format

```json
[
  {
    "title": "string",
    "url": "string",
    "date": "YYYY-MM-DD HH:MM:SS",
    "author": "string",
    "source": "Instagram",
    "domain": "instagram.com",
    "snippet": "string"
  }
]
```

## Example Request

```bash
curl -H "X-API-Key: your_api_key_here" \
  "https://forumscout.app/api/instagram_search?keyword=techstartup&sort_by=recent&page=1"
```

```python
import requests

headers = {
    'X-API-Key': 'your_api_key_here'
}

params = {
    'keyword': 'techstartup',
    'sort_by': 'recent',
    'page': 1
}

response = requests.get(
    'https://forumscout.app/api/instagram_search',
    headers=headers,
    params=params
)
```

## Example Response

```json
[
  {
    "title": "@techfounder on Instagram",
    "url": "https://instagram.com/p/abc123xyz",
    "date": "2024-03-20 15:30:00",
    "author": "techfounder",
    "source": "Instagram",
    "domain": "instagram.com",
    "snippet": "Just launched our new tech platform! #techstartup #innovation"
  }
]
```

## Sort Options

| sort_by | Description |
|---------|-------------|
| recent | Sort by post date (newest first) |
| top | Sort by engagement/popularity |

## Error Responses

| Status Code | Description |
|-------------|-------------|
| 400 | Missing keyword parameter or invalid page/sort parameter |
| 401 | Missing or invalid API key |
| 402 | Usage limit exceeded - Payment required |
| 429 | Too many requests |
| 500 | Server error |

## Usage Notes

1. Results are paginated with posts per page varying based on Instagram's API response
2. The free tier allows 50 requests per month
3. Additional requests are charged at $0.006 per request
4. Keywords are automatically converted to hashtag format (spaces and quotes removed)
5. Date format follows ISO 8601 standard
6. URLs are direct links to Instagram posts
7. The 'title' field combines the username with "on Instagram" for consistency
8. Response includes both posts and reels
9. Captions are truncated if they exceed the snippet length limit
10. Private account posts are not included in search results 
