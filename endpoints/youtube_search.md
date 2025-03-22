# YouTube Search API

The YouTube Search endpoint allows you to search for videos and shorts across YouTube's platform.

**Endpoint:** `GET /api/youtube_search`

## Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| keyword | string | Yes | The search term to find in YouTube videos |
| page | integer | No | Page number for pagination (default: 1) |
| upload_date | string | No | Filter results by upload date (default: None) |

## Response Format

```json
[
  {
    "title": "string",
    "url": "string",
    "date": "YYYY-MM-DD HH:MM:SS",
    "author": "string",
    "source": "YouTube" | "YouTube Shorts",
    "domain": "youtube.com",
    "snippet": "string"
  }
]
```

## Example Request

```bash
curl -H "X-API-Key: your_api_key_here" \
  "https://forumscout.app/api/youtube_search?keyword=react+tutorial&upload_date=this_week&page=1"
```

```python
import requests

headers = {
    'X-API-Key': 'your_api_key_here'
}

params = {
    'keyword': 'react tutorial',
    'upload_date': 'this_week',
    'page': 1
}

response = requests.get(
    'https://forumscout.app/api/youtube_search',
    headers=headers,
    params=params
)
```

## Example Response

```json
[
  {
    "title": "Complete React Tutorial 2024",
    "url": "https://youtube.com/watch?v=abc123xyz",
    "date": "2024-03-20 15:30:00",
    "author": "CodeTeacher",
    "source": "YouTube",
    "domain": "youtube.com",
    "snippet": "Learn React from scratch with this comprehensive guide..."
  }
]
```

## Upload Date Options

| upload_date | Description |
|-------------|-------------|
| last_hour | Videos uploaded in the last hour |
| today | Videos uploaded today |
| this_week | Videos uploaded this week |
| this_month | Videos uploaded this month |
| this_year | Videos uploaded this year |

## Error Responses

| Status Code | Description |
|-------------|-------------|
| 400 | Missing keyword parameter or invalid page/upload_date parameter |
| 401 | Missing or invalid API key |
| 402 | Usage limit exceeded - Payment required |
| 429 | Too many requests |
| 500 | Server error |

## Usage Notes

1. Results include both regular YouTube videos and Shorts
2. The free tier allows 50 requests per month
3. Additional requests are charged at $0.005 per request
4. Date format follows ISO 8601 standard
5. URLs are direct links to YouTube videos
6. The source field distinguishes between regular videos ("YouTube") and shorts ("YouTube Shorts")
7. The snippet field contains the video description (if available)
8. Results are returned in English language by default
9. Videos are region-agnostic but prioritize English content
10. Pagination uses continuation tokens internally for accurate results
11. If no description is available, snippet will show "This video has no description"
12. Results include both public and unlisted videos (if directly accessible) 
