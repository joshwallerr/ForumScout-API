# Authentication Guide

ForumScout API uses API key authentication for all requests. This guide explains how to obtain and use your API key.

## Obtaining an API Key

1. Sign up for a ForumScout developer account at [forumscout.app/api-signup](https://forumscout.app/api-signup)
2. Log in to your developer dashboard
3. Click "Generate API Key"
4. Store your API key securely - it cannot be retrieved once generated

## Using Your API Key

Include your API key in the request headers:

```http
X-API-Key: your_api_key_here
```

Example using cURL:
```bash
curl -H "X-API-Key: your_api_key_here" https://forumscout.app/api/forum_search?keyword=example
```

Example using Python requests:
```python
import requests

headers = {
    'X-API-Key': 'your_api_key_here'
}

response = requests.get(
    'https://forumscout.app/api/forum_search',
    headers=headers,
    params={'keyword': 'example'}
)
```

## Security Best Practices

1. Never share your API key or commit it to version control
2. Use environment variables to store your API key
3. Regenerate your API key if it's ever exposed
4. One API key per application/project

## API Key Management

- To regenerate your key: Use the "Regenerate Key" button in the developer dashboard
- To revoke your key: Use the "Destroy Key" button in the developer dashboard
- Lost keys cannot be recovered - you'll need to generate a new one

## Rate Limiting

Your API key is used to track your usage:
- Free tier: 50 requests per month
- Paid tier: Unlimited requests (pay per use)
- Usage resets on the 1st of each month 
