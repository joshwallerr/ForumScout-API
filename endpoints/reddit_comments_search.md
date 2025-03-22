# Reddit Comments Search API

The Reddit Comments Search endpoint allows you to search for comments across all of Reddit.

**Endpoint:** `GET /api/reddit_comments_search`

## Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| keyword | string | Yes | The search term to find in Reddit comments |
| page | integer | No | Page number for pagination (default: 1, must be > 0) |
| sort_by | string | No | Sort method for results (default: 'created_utc') |

## Response Format

```json
[
  {
    "title": "string",
    "url": "string",
    "date": "YYYY-MM-DD HH:MM:SS",
    "author": "string",
    "source": "Reddit (Comment)",
    "domain": "reddit.com",
    "snippet": "string",
    "type": "comment",
    "subreddit": "string",
    "score": integer
  }
]
```

## Example Request

```bash
curl -H "X-API-Key: your_api_key_here" \
  "https://forumscout.app/api/reddit_comments_search?keyword=machine+learning&sort_by=created_utc&page=1"
```

```python
import requests

headers = {
    'X-API-Key': 'your_api_key_here'
}

params = {
    'keyword': 'machine learning',
    'sort_by': 'created_utc',
    'page': 1
}

response = requests.get(
    'https://forumscout.app/api/reddit_comments_search',
    headers=headers,
    params=params
)
```

## Example Response

```json
[
  {
    "title": "user123 on r/MachineLearning",
    "url": "https://www.reddit.com/comments/abc123/comment/xyz789",
    "date": "2024-03-20 15:30:00",
    "author": "user123",
    "source": "Reddit (Comment)",
    "domain": "reddit.com",
    "snippet": "The latest developments in transformer architecture have revolutionized...",
    "type": "comment",
    "subreddit": "MachineLearning",
    "score": 42
  }
]
```

## Sort Options

| sort_by | Description |
|---------|-------------|
| created_utc | Sort by creation date (newest first, default) |
| score | Sort by comment score (highest first) |

## Error Responses

| Status Code | Description |
|-------------|-------------|
| 400 | Missing keyword parameter or invalid page/sort parameter |
| 401 | Missing or invalid API key |
| 402 | Usage limit exceeded - Payment required |
| 429 | Too many requests |
| 500 | Server error |

## Usage Notes

1. Results are paginated with 10 comments per page
2. The free tier allows 50 requests per month
3. Additional requests are charged at $0.003 per request
4. Date format follows ISO 8601 standard
5. URLs are direct links to the specific comment
6. The title field combines the username and subreddit for context
7. The snippet field contains the comment body
8. Comment score indicates community rating (upvotes minus downvotes)
9. Search includes comments from all subreddits
10. Deleted comments are marked with '[deleted]' as the author
11. Comments are retrieved in batches of 100 internally for efficient pagination
12. The source field is specifically marked as "Reddit (Comment)" to distinguish from posts 
