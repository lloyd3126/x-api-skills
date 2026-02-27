---
name: x-api-dev
description: Use this skill when building applications with the X API (formerly Twitter API). Covers posts, users, spaces, direct messages, lists, trends, media, webhooks, authentication, rate limits, and SDKs for Python and TypeScript.
---

# X API Development Skill

## Overview

The X API provides access to X's real-time global data. Key capabilities include:
- **Posts** - Create, read, search, and manage posts (tweets)
- **Users** - User profiles, followers, following, blocking, muting
- **Spaces** - Live audio spaces
- **Direct Messages** - Send and receive DMs
- **Lists** - Curation and management of lists
- **Trends** - Trending topics and hashtags
- **Media** - Upload images, videos, and GIFs
- **Webhooks** - Real-time event notifications
- **Search** - Search posts, users, and more
- **Streaming** - Real-time stream of posts

## Pricing

The X API uses **pay-per-usage** pricing. No monthly subscriptions — pay only for what you use.

- **Pay-per-usage** - Flexible, credit-based pricing. Scale up or down based on your needs with no commitments or minimum spend.
- **Enterprise** - Dedicated support, complete streams, and custom integrations for high-volume needs.

> [!IMPORTANT]
> Earn free xAI API credits when you purchase X API credits — up to 20% back based on your spend.

## Authentication

### Bearer Token (App-only)
```bash
# Set Authorization header
Authorization: Bearer YOUR_BEARER_TOKEN
```

### OAuth 2.0 (User-context)
```bash
# For user actions, use OAuth 2.0 with appropriate scopes
Authorization: Bearer YOUR_ACCESS_TOKEN
```

### Required Scopes
- `tweet.read` - Read tweets
- `tweet.write` - Create tweets
- `tweet.moderate.write` - Moderate tweets
- `users.read` - Read user profiles
- `follows.read` - Read follows
- `follows.write` - Follow/unfollow
- `offline.access` - Refresh access tokens
- `space.read` - Read Spaces
- `space.write` - Create Spaces
- `dm.read` - Read DMs
- `dm.write` - Send DMs

## SDKs

### Python
Install with `pip install x-python` (official SDK coming soon, use requests for now)

```python
import requests

def get_user_tweets(username, bearer_token):
    url = f"https://api.x.com/2/tweets/by/username/{username}"
    headers = {"Authorization": f"Bearer {bearer_token}"}
    response = requests.get(url, headers=headers)
    return response.json()
```

### JavaScript/TypeScript
Install with `npm install x-sdk` (official SDK coming soon, use fetch for now)

```typescript
async function getUserTweets(username: string, bearerToken: string) {
  const response = await fetch(
    `https://api.x.com/2/tweets/by/username/${username}`,
    {
      headers: { Authorization: `Bearer ${bearerToken}` }
    }
  );
  return response.json();
}
```

## Quick Start

### Get Your API Keys

1. Go to [Developer Console](https://console.x.com)
2. Create a project and app
3. Generate API keys and access tokens
4. Purchase credits (pay-per-usage)

### Make Your First Request

```bash
# Get your own user info
curl "https://api.x.com/2/users/me" \
  -H "Authorization: Bearer YOUR_BEARER_TOKEN"
```

```python
import requests

# Post a tweet
def post_tweet(text, bearer_token):
    url = "https://api.x.com/2/tweets"
    headers = {
        "Authorization": f"Bearer {bearer_token}",
        "Content-Type": "application/json"
    }
    data = {"text": text}
    response = requests.post(url, headers=headers, json=data)
    return response.json()

# Usage
result = post_tweet("Hello from X API!", "YOUR_BEARER_TOKEN")
print(result)
```

## API Base URLs

- **Production**: `https://api.x.com`
- **API Version**: Use `/2/` prefix for most endpoints

## Common Endpoints

### Posts
- `POST /2/tweets` - Create a post
- `GET /2/tweets/:id` - Get a post by ID
- `DELETE /2/tweets/:id` - Delete a post
- `GET /2/tweets/search/recent` - Search recent posts
- `GET /2/tweets/search/all` - Search all posts (premium)

### Users
- `GET /2/users/:id` - Get user by ID
- `GET /2/users/by/username/:username` - Get user by username
- `GET /2/users/:id/tweets` - Get user's tweets
- `GET /2/users/:id/followers` - Get followers
- `GET /2/users/:id/following` - Get following
- `POST /2/users/:id/following` - Follow a user
- `DELETE /2/users/:id/following/:target_user_id` - Unfollow

### Spaces
- `GET /2/spaces/:id` - Get Space by ID
- `GET /2/spaces/search` - Search Spaces
- `GET /2/spaces/:id/tweets` - Get Space tweets

### Lists
- `GET /2/lists/:id` - Get list by ID
- `GET /2/users/:id/lists` - Get user's lists
- `POST /2/lists` - Create a list
- `POST /2/lists/:id/members` - Add member to list

### Direct Messages
- `GET /2/dm_conversations` - Get DM conversations
- `POST /2/dm_conversations` - Create DM conversation
- `GET /2/dm_conversations/:id/messages` - Get messages

### Trends
- `GET /2/trends/by/woeid/:woeid` - Get trends by WOEID

### Media
- `POST /2/media/upload` - Upload media
- `GET /2/media/:id` - Get media info

## Rate Limits

Rate limits vary by endpoint and your plan. Check the [API Reference](https://docs.x.com/x-api/introduction) for specific limits.

General guidelines:
- Free tier: Limited requests
- Basic tier: Higher limits
- Pro/Enterprise: Highest limits

## Documentation

**Documentation Index**: `https://docs.x.com/llms.txt`

Fetch this index to discover all available documentation pages.

### Key Documentation Pages
- [Quickstart](https://docs.x.com/x-api/getting-started/make-your-first-request)
- [API Reference](https://docs.x.com/x-api/introduction)
- [Pricing](https://docs.x.com/x-api/getting-started/pricing)
- [Authentication](https://docs.x.com/x-api/authentication)
- [Rate Limits](https://docs.x.com/x-api/rate-limits)
- [SDKs](https://docs.x.com/xdks/overview)

## Webhooks

Set up webhooks to receive real-time events:

1. Create a webhook via API
2. Register callback URL
3. Subscribe to events (tweets, follows, DMs, etc.)

Events available:
- `tweet_create`
- `tweet_delete`
- `follow`
- `unfollow`
- `favorite`
- `dm_received`
- And more...

## Streaming API

Connect to real-time streams:

- **Filtered Stream** - Stream matching specific rules
- **Sample Stream** - Random sample of all tweets
- **Decahose** - 10% sample (Enterprise)

```python
import sseclient
import requests

def stream_tweets(bearer_token):
    url = "https://api.x.com/2/tweets/search/stream"
    headers = {"Authorization": f"Bearer {bearer_token}"}
    response = requests.get(url, headers=headers, stream=True)
    
    client = sseclient.SSEClient(response)
    for event in client.events():
        print(event.data)
```
