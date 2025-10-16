# n8n Automations Starter

A comprehensive starter repository for building, managing, and sharing n8n workflow automations. This repository provides scaffolded documentation, example workflows, and best practices for automation development.

## 📋 Introduction

**n8n** is a powerful workflow automation tool that allows you to connect various services and automate repetitive tasks. This starter repository helps you:

- Organize your n8n workflows systematically
- Document automation logic and dependencies
- Share reusable workflow templates
- Maintain consistent standards across projects
- Troubleshoot common issues efficiently

### What's Included

- Pre-configured workflow templates
- Node reference documentation
- Best practices and design patterns
- Troubleshooting guides
- Prompt templates for AI-assisted workflow creation

## 🔧 Node Reference Table

Common nodes used in this repository and their purposes:

| Node Type | Category | Use Case | Documentation |
|-----------|----------|----------|---------------|
| **HTTP Request** | Core | Make API calls to external services | [Docs](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.httprequest/) |
| **Webhook** | Core | Trigger workflows via HTTP requests | [Docs](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.webhook/) |
| **Schedule Trigger** | Core | Run workflows on a schedule | [Docs](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.scheduletrigger/) |
| **Set** | Core | Manipulate data structure | [Docs](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.set/) |
| **IF** | Core | Conditional branching logic | [Docs](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.if/) |
| **Code** | Core | Execute custom JavaScript/Python | [Docs](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.code/) |
| **Gmail** | App | Send and receive emails | [Docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.gmail/) |
| **Google Sheets** | App | Read/write spreadsheet data | [Docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googlesheets/) |
| **Slack** | App | Send messages and interact with Slack | [Docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.slack/) |
| **OpenAI** | App | AI-powered text generation and analysis | [Docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.openai/) |

### Adding Custom Nodes

To extend functionality:
1. Navigate to **Settings > Community Nodes**
2. Search for the desired node package
3. Install and restart n8n
4. Update this table with new node references

## 🔄 Workflows

### Workflow Organization

Workflows in this repository follow a consistent naming convention:

```
[CATEGORY]-[PURPOSE]-[VERSION].json
```

Example: `data-sync-crm-to-sheets-v1.json`

### Available Workflow Templates

#### 1. **Data Synchronization**
- **File**: `workflows/data-sync-template.json`
- **Purpose**: Sync data between two systems on a schedule
- **Triggers**: Schedule Trigger (daily at 9 AM)
- **Key Nodes**: HTTP Request, Set, Google Sheets

#### 2. **Webhook Processor**
- **File**: `workflows/webhook-processor-template.json`
- **Purpose**: Receive and process incoming webhook data
- **Triggers**: Webhook
- **Key Nodes**: Webhook, IF, Code, HTTP Request

#### 3. **Email Automation**
- **File**: `workflows/email-automation-template.json`
- **Purpose**: Automated email sending with dynamic content
- **Triggers**: Schedule Trigger / Webhook
- **Key Nodes**: Gmail, Set, IF

#### 4. **AI Content Generator**
- **File**: `workflows/ai-content-generator-template.json`
- **Purpose**: Generate content using AI based on templates
- **Triggers**: Manual / Webhook
- **Key Nodes**: OpenAI, Set, HTTP Request

### Importing Workflows

1. Download the workflow JSON file from this repository
2. Open your n8n instance
3. Navigate to **Workflows > Import from File**
4. Select the downloaded JSON file
5. Configure credentials and environment-specific settings
6. Test and activate the workflow

## 💡 Prompt Templates

Use these prompts to accelerate workflow development with AI assistance:

### General Workflow Creation

```
Create an n8n workflow that:
- Triggers: [describe trigger condition]
- Processes: [describe data processing steps]
- Outputs: [describe desired output]
- Error handling: [specify error handling requirements]
```

### Data Transformation

```
I need to transform data in n8n from:
Input format: [provide sample JSON]
To output format: [provide desired JSON]
Using: [Set node / Code node]
```

### API Integration

```
Help me create an n8n HTTP Request node configuration for:
- API endpoint: [URL]
- Authentication: [type]
- Method: [GET/POST/PUT/DELETE]
- Request body: [structure]
- Expected response: [structure]
```

### Debugging and Optimization

```
My n8n workflow is experiencing: [describe issue]
Workflow structure: [provide overview]
Error message: [paste error]
What I've tried: [list attempted solutions]
Help me troubleshoot and optimize this workflow.
```

### Code Node Script Generation

```
Generate JavaScript code for an n8n Code node that:
- Input: [describe input data structure]
- Processing logic: [describe what needs to happen]
- Output: [describe expected output format]
- Handle edge cases: [list potential issues]
```

## 🛠️ Troubleshooting Notes

### Common Issues and Solutions

#### 1. **Workflow Not Triggering**

**Symptoms**: Workflow doesn't execute on schedule or webhook

**Solutions**:
- ✅ Verify the workflow is **activated** (toggle in top-right corner)
- ✅ Check trigger node configuration (schedule format, webhook URL)
- ✅ Review execution logs in **Executions** tab
- ✅ Ensure n8n instance is running and accessible
- ✅ For webhooks, verify the URL is correct and accessible externally

#### 2. **Authentication Errors**

**Symptoms**: "Authentication failed" or 401/403 errors

**Solutions**:
- ✅ Recreate credentials in **Credentials** menu
- ✅ Verify API keys/tokens haven't expired
- ✅ Check OAuth2 redirect URLs are configured correctly
- ✅ Ensure credentials are assigned to the correct nodes
- ✅ Test credentials using the **Test** button

#### 3. **Data Mapping Issues**

**Symptoms**: Data not passing correctly between nodes

**Solutions**:
- ✅ Use **expression editor** to inspect available data
- ✅ Check for correct JSON path syntax: `{{ $json.field_name }}`
- ✅ Verify input data structure matches expectations
- ✅ Use **Set node** to restructure data before passing forward
- ✅ Enable **Output Raw Data** in node settings to see actual structure

#### 4. **Rate Limiting / Timeout Errors**

**Symptoms**: 429 errors or timeout messages

**Solutions**:
- ✅ Implement **delay** between batch operations
- ✅ Add **error handling** with retry logic
- ✅ Increase timeout settings in HTTP Request nodes
- ✅ Use pagination for large data sets
- ✅ Check API provider's rate limit documentation

#### 5. **Code Node Errors**

**Symptoms**: JavaScript execution failures

**Solutions**:
- ✅ Use `console.log()` to debug (visible in execution logs)
- ✅ Access input data via `$input.all()` or `$input.first()`
- ✅ Return data in correct format: `return [{ json: { result: value } }]`
- ✅ Handle null/undefined values properly
- ✅ Check for syntax errors in the code

#### 6. **Workflow Performance Issues**

**Symptoms**: Slow execution or timeouts

**Solutions**:
- ✅ Minimize the number of items processed per execution
- ✅ Use **batching** to split large operations
- ✅ Optimize database queries and API calls
- ✅ Reduce unnecessary data transformations
- ✅ Consider using **Execute Workflow** node to split into sub-workflows

### Debugging Best Practices

1. **Enable Save Executions**: Settings > Executions > Save successful executions
2. **Use Pin Data**: Pin sample data to nodes for consistent testing
3. **Test Incrementally**: Build workflows step-by-step, testing each node
4. **Check Logs**: Review execution logs for detailed error information
5. **Version Control**: Export workflows regularly to track changes

### Getting Help

- 📚 [Official n8n Documentation](https://docs.n8n.io/)
- 💬 [n8n Community Forum](https://community.n8n.io/)
- 🐛 [GitHub Issues](https://github.com/n8n-io/n8n/issues)
- 📺 [n8n YouTube Channel](https://www.youtube.com/c/n8n-io)

## 🚀 Getting Started

1. **Install n8n** (if not already installed):
   ```bash
   npm install -g n8n
   ```

2. **Start n8n**:
   ```bash
   n8n start
   ```

3. **Clone this repository**:
   ```bash
   git clone https://github.com/donnydom/n8n-automations-starter.git
   ```

4. **Import workflows** from the `workflows/` directory

5. **Configure credentials** for the services you'll be using

6. **Customize and activate** workflows based on your needs

## 📁 Repository Structure

```
n8n-automations-starter/
├── README.md                          # This file
├── workflows/                         # Workflow JSON exports
│   ├── data-sync-template.json
│   ├── webhook-processor-template.json
│   ├── email-automation-template.json
│   └── ai-content-generator-template.json
├── docs/                             # Additional documentation
│   ├── node-reference.md
│   ├── best-practices.md
│   └── advanced-patterns.md
└── examples/                         # Example use cases
    ├── crm-integration/
    ├── social-media-automation/
    └── data-processing/
```

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork this repository
2. Create a feature branch
3. Add your workflow or documentation
4. Submit a pull request with a clear description

## 📄 License

This project is licensed under the MIT License - feel free to use and modify as needed.

## ⭐ Acknowledgments

- Built with [n8n](https://n8n.io/) - Fair-code licensed workflow automation tool
- Inspired by the n8n community and their shared workflows

---

**Ready to automate?** Start by importing one of the template workflows and customize it for your needs!
