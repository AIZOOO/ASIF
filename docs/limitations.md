# ASIF Limitations & Integration Notes

## Current Limitations
- **LLM Runtime Support**: Only LLMs/platforms that support tool/function calling and MCP can use ASIF autonomously. Not all LLMs (e.g., vanilla ChatGPT web) support this yet.
- **MCP Server Requirement**: An MCP server must be running and accessible to the LLM agent.
- **Security Model**: Secure handoff relies on correct implementation of SPIFFE, key management, and sandboxing (WASM). Any weakness here can expose secrets.
- **Marketplace Centralization**: If the ASIF Marketplace is centralized, it can become a single point of failure or trust bottleneck.
- **Service Provider Adoption**: Providers must implement the ASIF protocol endpoints and manifest. Adoption may lag.

## Practical Integration Notes
- **LLM Configuration**: LLMs must be configured to accept tool schemas from MCP and emit tool calls. This may require custom deployment or API access.
- **Tool Schema Design**: Tool schemas must be clear, unambiguous, and machine-readable (JSON Schema recommended).
- **Human-in-the-Loop**: For high-risk actions (e.g., financial transfers), OPA or policy engines should enforce human approval.
- **Ephemeral Credentials**: Always use short-lived, scoped credentials for provisioned services.

## Research Directions
- Improving LLM tool-use reliability and error handling
- Decentralized/federated marketplace models
- Stronger confidential computing and sandboxing for agent code
- Automated policy learning for OPA guardrails
