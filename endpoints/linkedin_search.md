# LinkedIn Search API

The LinkedIn Search endpoint allows you to search for posts and content across LinkedIn's platform.

**Endpoint:** `GET /api/linkedin_search`

## Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| keyword | string | Yes | The search term to find in LinkedIn posts |
| page | integer | No | Page number for pagination (default: 1) |
| sort_by | string | No | Sort method for results (default: 'date_posted') |

## Response Format

```json
[
  {
    "title": "string",
    "url": "string",
    "date": "YYYY-MM-DD HH:MM:SS",
    "author": "string",
    "source": "LinkedIn",
    "domain": "linkedin.com",
    "snippet": "string"
  }
]
```

## Example Request

```bash
curl -H "X-API-Key: your_api_key_here" \
  "https://forumscout.app/api/linkedin_search?keyword=startup&sort_by=date_posted&page=1"
```

```python
import requests

headers = {
    'X-API-Key': 'your_api_key_here'
}

params = {
    'keyword': 'startup',
    'sort_by': 'date_posted',
    'page': 1
}

response = requests.get(
    'https://forumscout.app/api/linkedin_search',
    headers=headers,
    params=params
)
```

## Example Response

```json
[
  {
    "title": "@johndoe on LinkedIn",
    "url": "https://linkedin.com/posts/johndoe-123456",
    "date": "2024-03-20 15:30:00",
    "author": "John Doe",
    "source": "LinkedIn",
    "domain": "linkedin.com",
    "snippet": "Excited to announce our startup's latest funding round..."
  }
]
```

## Sort Options

| sort_by | Description |
|---------|-------------|
| date_posted | Sort by post date (newest first) |
| relevance | Sort by relevance to search query |

## Error Responses

| Status Code | Description |
|-------------|-------------|
| 400 | Missing keyword parameter or invalid page/sort parameter |
| 401 | Missing or invalid API key |
| 402 | Usage limit exceeded - Payment required |
| 429 | Too many requests |
| 500 | Server error |

## Usage Notes

1. Results are paginated with posts per page varying based on LinkedIn's API response
2. The free tier allows 50 requests per month
3. Additional requests are charged at $0.006 per request
4. Posts are returned in a standardized format for easy integration
5. Date format follows ISO 8601 standard
6. URLs are direct links to LinkedIn posts
7. The 'title' field combines the author's name with "on LinkedIn" for consistency
8. Response includes both regular posts and articles shared on LinkedIn 
