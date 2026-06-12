# API Reference

**Endpoint** = a web address (URL) where the agent's services can be accessed.

## Endpoints

> Replace placeholders with the actual values from your "View Code" panel in the playground.

| Endpoint | Method | Purpose |
|---|---|---|
| `/threads` | POST | Create a new conversation thread |
| `/threads/{thread_id}/messages` | POST | Add a user message to a thread |
| `/threads/{thread_id}/runs` | POST | Process the thread with the agent (reasoning step) |
| `/threads/{thread_id}/messages` | GET | Retrieve messages, including the agent's response |

Base URL: `https://YOUR-PROJECT.services.ai.azure.com/api/projects/YOUR-PROJECT-NAME`

## Sample Request (JSON)

Adding a user message to a thread:

```json
{
  "role": "user",
  "content": "Is the hotel pet-friendly, and what are the restaurant hours?"
}
```

## Sample Response (JSON)

```json
{
  "id": "msg_abc123",
  "role": "assistant",
  "content": [
    {
      "type": "text",
      "text": {
        "value": "Yes! We welcome pets up to 50 lbs with a $75 cleaning fee. Our restaurant, The Grove, serves breakfast 7–10 AM, lunch 11:30 AM–2 PM, and dinner 5–10 PM daily."
      }
    }
  ],
  "created_at": 1718203200
}
```

## Authentication

All requests are authenticated via `DefaultAzureCredential`. No API keys are passed in request headers manually; tokens are acquired automatically from the Azure identity environment. Sensitive values are stored in **Azure Key Vault**, never in source code.
