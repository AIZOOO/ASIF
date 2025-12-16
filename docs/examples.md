# ASIF Example Code

## 1. LLM Agent: Provisioning a Service (Python)
```python
import requests
import json
from cryptography.hazmat.primitives import serialization
from cryptography.hazmat.primitives.asymmetric import rsa

# Generate ephemeral key pair
private_key = rsa.generate_private_key(public_exponent=65537, key_size=2048)
public_key = private_key.public_key().public_bytes(
    encoding=serialization.Encoding.PEM,
    format=serialization.PublicFormat.SubjectPublicKeyInfo
).decode()

# Prepare provisioning request
provision_payload = {
    "agent_id": "agent_x892_alpha",
    "timestamp": "2023-10-27T10:00:00Z",
    "intent_context": {"project_name": "MyEcommerceApp", "environment": "development"},
    "requested_tier": "free",
    "encryption_key_public": public_key
}

# Send to provider
resp = requests.post("https://api.neon.tech/asif/v1/provision", json=provision_payload)
print(resp.json())
```

## 2. Service Provider: Provision Endpoint (Node.js/Express)
```js
const express = require('express');
const app = express();
app.use(express.json());

app.post('/asif/v1/provision', (req, res) => {
  // Validate request, rate limits, etc.
  const { agent_id, encryption_key_public } = req.body;
  // ...provision account, generate credentials...
  // Encrypt credentials with agent's public key (pseudo-code)
  const encrypted = encryptWithPublicKey(encryption_key_public, { DATABASE_URL: 'postgres://...' });
  res.json({
    status: 'success',
    account_id: 'proj_889900',
    payload_encrypted: encrypted
  });
});

app.listen(3000);
```

## 3. Marketplace: Service Discovery (Python)
```python
import requests
resp = requests.get('https://marketplace.asif.org/discover?capability=push_notifications')
print(resp.json())
```
