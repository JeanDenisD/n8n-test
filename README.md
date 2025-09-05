# n8n Test Repository

Test repository for n8n workflow exports and automation using Claude Desktop MCP integration.

## Workflow: Webhook to Log Test

**Description:** Simple workflow that receives webhook data, logs it, and responds with a success message.

**Workflow ID:** `XlmbDaOOPQQzA646`  
**Created:** 2025-09-05 09:59:58 UTC

### Workflow Structure

```
Webhook (POST) → Log Data → Respond to Webhook
```

### Nodes:

1. **Webhook**
   - Type: `n8n-nodes-base.webhook`
   - Method: POST
   - Path: `/test-webhook`
   - Mode: Response Node

2. **Log Data**
   - Type: `n8n-nodes-base.noOp`
   - Purpose: Logs incoming data for debugging

3. **Respond to Webhook**
   - Type: `n8n-nodes-base.respondToWebhook`
   - Response: JSON
   - Body: `{"status": "success", "message": "Data logged successfully"}`

### Usage

To test this workflow:

1. Activate the workflow in your n8n instance
2. Send a POST request to: `http://your-n8n-instance:port/webhook/test-webhook`
3. Check n8n logs to see the logged data
4. Receive success response

### Example cURL Test

```bash
curl -X POST http://n8n.onscopeconsulting.com:8452/webhook/test-webhook \
  -H "Content-Type: application/json" \
  -d '{"test": "data", "timestamp": "2025-09-05T10:00:00Z"}'
```

## Repository Structure

```
n8n-test/
├── README.md
└── workflows/
    └── webhook-to-log-test.json
```

## About

This repository demonstrates the integration between:
- n8n (workflow automation)
- Claude Desktop (AI assistant)
- GitHub (version control)

Using Model Context Protocol (MCP) servers for seamless automation workflow management.
