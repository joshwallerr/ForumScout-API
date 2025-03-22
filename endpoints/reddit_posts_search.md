# Reddit Posts Search API

The Reddit Posts Search endpoint allows you to search for posts (submissions) across all of Reddit.

**Endpoint:** `GET /api/reddit_posts_search`

## Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| keyword | string | Yes | The search term to find in Reddit posts |
| page | integer | No | Page number for pagination (default: 1, must be > 0) |
| sort_by | string | No | Sort method for results (default: 'new') |

## Response Format

```json
[
  {
    "title": "string",
    "url": "string",
    "date": "YYYY-MM-DD HH:MM:SS",
    "author": "string",
    "source": "Reddit",
    "domain": "reddit.com",
    "snippet": "string",
    "nsfw": boolean,
    "type": "post",
    "subreddit": "string"
  }
]
```

## Example Request

```bash
curl -H "X-API-Key: your_api_key_here" \
  "https://forumscout.app/api/reddit_posts_search?keyword=python+tutorial&sort_by=new&page=1"
```

```python
import requests

headers = {
    'X-API-Key': 'your_api_key_here'
}

params = {
    'keyword': 'python tutorial',
    'sort_by': 'new',
    'page': 1
}

response = requests.get(
    'https://forumscout.app/api/reddit_posts_search',
    headers=headers,
    params=params
)
```

## Example Response

```json
[
  {
    "title": "Complete Python Tutorial for Beginners",
    "url": "https://www.reddit.com/r/learnpython/comments/abc123",
    "date": "2024-03-20 15:30:00",
    "author": "pythonteacher",
    "source": "Reddit",
    "domain": "reddit.com",
    "snippet": "I've created a comprehensive Python tutorial covering basics to advanced topics...",
    "nsfw": false,
    "type": "post",
    "subreddit": "learnpython"
  }
]
```

## Sort Options

| sort_by | Description |
|---------|-------------|
| hot | Sort by current popularity and time |
| new | Sort by newest first (default) |
| relevance | Sort by relevance to search query |
| top | Sort by all-time popularity |

## Error Responses

| Status Code | Description |
|-------------|-------------|
| 400 | Missing keyword parameter or invalid page/sort parameter |
| 401 | Missing or invalid API key |
| 402 | Usage limit exceeded - Payment required |
| 429 | Too many requests |
| 500 | Server error |

## Usage Notes

1. Results are paginated with 25 posts per page
2. The free tier allows 50 requests per month
3. Additional requests are charged at $0.003 per request
4. Date format follows ISO 8601 standard
5. URLs are direct links to Reddit posts
6. The snippet field contains either the post's selftext or title if no selftext exists
7. NSFW (Not Safe For Work) content is marked with the nsfw flag
8. Deleted posts are marked with '[deleted]' as the author
9. Search includes posts from all subreddits
10. Response includes additional Reddit-specific fields like subreddit name
11. When sorting by 'new', results are additionally sorted by date in descending order 
