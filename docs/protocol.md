# ASIF Protocol Specification

## 1. Service Manifest (`asif-manifest.json`)
```json
{
  "asif_version": "1.0",
  "service_name": "Neon Postgres",
  "category": "database/relational",
  "description": "Serverless Postgres with autoscaling.",
  "provider_signature": "sha256:8f4b...",
  "endpoints": {
    "provision": "https://api.neon.tech/asif/v1/provision",
    "documentation_rag": "https://api.neon.tech/asif/v1/context.json"
  },
  "pricing": {
    "model": "freemium",
    "free_tier_limit": "500MB Storage"
  }
}
```

## 2. Provisioning Request (POST `/provision`)
```json
{
  "agent_id": "agent_x892_alpha",
  "timestamp": "2023-10-27T10:00:00Z",
  "intent_context": {
    "project_name": "MyEcommerceApp",
    "environment": "development"
  },
  "requested_tier": "free",
  "encryption_key_public": "-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqh..."
}
```

## 3. Secure Handover (Response)
```json
{
  "status": "success",
  "account_id": "proj_889900",
  "payload_encrypted": "eyJhbGciOiJSU0EtT0E..."
}
```

## 4. Runtime Tool Schema (MCP)
```json
{
  "tool_name": "pusher_send",
  "description": "Sends a push notification to a specific device or topic. Use this when the user mentions alerting or notifying a client.",
  "parameters": {
    "target": { "type": "string", "description": "The device ID or topic name (e.g., 'news-updates')." },
    "message": { "type": "string", "description": "The text content of the notification." },
    "priority": { "enum": ["high", "normal"], "default": "normal" }
  }
}
```
