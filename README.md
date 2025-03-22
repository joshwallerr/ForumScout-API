# ForumScout API Documentation

ForumScout provides a powerful API for searching social media content across multiple platforms. Our API enables developers to search for posts, comments, and content across LinkedIn, Instagram, Reddit, YouTube, and Twitter (X).

## Available Endpoints

- `/api/forum_search` - General forum search
- `/api/linkedin_search` - LinkedIn posts search
- `/api/instagram_search` - Instagram posts search
- `/api/reddit_posts_search` - Reddit posts search
- `/api/reddit_comments_search` - Reddit comments search
- `/api/youtube_search` - YouTube videos search
- `/api/x_search` - Twitter (X) posts search

## Getting Started

1. [Create a ForumScout Developer Account](https://forumscout.app/api-signup)
2. Generate your API key from the developer dashboard
3. Read the [Authentication Guide](authentication.md)
4. Explore individual endpoint documentation in this directory

## Pricing

- **Free Tier**: 50 API calls per month
- **Paid Plans**: Per-request pricing after free tier
  - Forum Search: $0.008/request
  - LinkedIn Search: $0.006/request
  - Instagram Search: $0.006/request
  - Reddit Search: $0.003/request
  - YouTube Search: $0.005/request
  - Twitter (X) Search: $0.006/request

## Response Format

All endpoints return data in a consistent JSON format:

```json
{
  "title": "Post Title or Username",
  "url": "URL to Original Content",
  "date": "YYYY-MM-DD HH:MM:SS",
  "author": "Content Author",
  "source": "Platform Name",
  "domain": "Platform Domain",
  "snippet": "Content Preview"
}
```

## Rate Limiting

- Free tier: 50 requests per month
- Paid tier: No rate limits, pay per request
- All requests require authentication via API key

## Error Handling

All endpoints use standard HTTP status codes:
- 200: Success
- 400: Bad Request
- 401: Unauthorized
- 402: Payment Required
- 429: Too Many Requests
- 500: Server Error

## Support

For API support, contact us at josh@forumscout.app 
