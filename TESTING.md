# Testing the Webhook Workflow

This document demonstrates how to test the "Webhook to Log Test" workflow.

## Test Setup

### Prerequisites
- n8n instance running and accessible
- Workflow "Webhook to Log Test" created and activated
- PowerShell or terminal access for testing

### Workflow Configuration

The webhook node is configured with:
- **HTTP Method**: POST
- **Path**: `test-webhook`
- **Response Mode**: Using 'Respond to Webhook' Node
- **Authentication**: None

## Testing Process

### Step 1: Activate the Workflow

1. Open your n8n instance in a web browser
2. Navigate to the "Webhook to Log Test" workflow
3. Click the toggle button in the top-right to activate the workflow
4. Ensure the workflow status shows as "Active"

### Step 2: Identify Test URLs

In the webhook node configuration, you'll see two URLs:

- **Test URL**: `http://your-n8n-instance:port/webhook-test/test-webhook`
- **Production URL**: `http://your-n8n-instance:port/webhook/test-webhook`

### Step 3: Execute Test

#### Using PowerShell (Windows)

```powershell
Invoke-RestMethod -Uri "http://your-n8n-instance:port/webhook-test/test-webhook" -Method POST -ContentType "application/json" -Body '{"test": "data", "timestamp": "2025-09-05T10:00:00Z", "source": "test-client"}'
```

#### Using cURL (Linux/macOS/Windows)

```bash
curl -X POST http://your-n8n-instance:port/webhook-test/test-webhook \
  -H "Content-Type: application/json" \
  -d '{"test": "data", "timestamp": "2025-09-05T10:00:00Z", "source": "test-client"}'
```

## Expected Results

### Successful Response

When the test is successful, you should receive:

```
status  message
------  -------
success Data logged successfully
```

### Workflow Execution

In the n8n interface, you should see:
1. A new execution entry in the workflow executions list
2. Data flowing through each node: Webhook → Log Data → Respond to Webhook
3. The webhook node showing the received data
4. The response node confirming the success message was sent

## Troubleshooting

### Common Issues

#### "Webhook not registered" Error
- Ensure the workflow is activated (toggle in top-right)
- Try using the test URL instead of production URL
- For test mode, click "Execute workflow" button before testing

#### Connection Refused
- Verify your n8n instance is running
- Check the correct port number
- Ensure firewall allows connections

#### Invalid JSON Error
- Verify the JSON payload syntax
- Ensure proper Content-Type header is set
- Check for proper escaping of quotes in your command

### Test Mode vs Production Mode

- **Test Mode**: Webhook only works for one call after clicking "Execute workflow"
- **Production Mode**: Webhook works continuously when workflow is active

## Integration with MCP

This workflow demonstrates the integration between:
- Claude Desktop (AI assistant)
- n8n MCP Server (workflow automation)
- GitHub MCP Server (version control)

The entire workflow creation, testing, and documentation process can be automated through Model Context Protocol servers, enabling seamless AI-assisted automation development.
