# LibreChat Agents Setup Guide

## What is this project?

**@librechat/agents** is a TypeScript library for building AI agents using LangGraph and various LLM providers. It's part of the LibreChat ecosystem and provides a framework for creating conversational AI agents with tool capabilities.

### Key Features:

- **Multi-LLM Support**: OpenAI, Anthropic Claude, Google Gemini, Mistral, Azure OpenAI, Ollama, DeepSeek, XAI, and more
- **Tool Integration**: Code execution, web search, file handling, and custom tools
- **Streaming Support**: Real-time streaming responses
- **Graph-based Architecture**: Built on LangGraph for complex workflow management
- **Memory Management**: Conversation history and context handling

## Prerequisites

- **Node.js**: Version 14.0.0 or higher (tested with v22.16.0)
- **npm**: Version 10.5.2 or higher

## Setup Instructions

### 1. Install Dependencies

```bash
npm ci
```

### 2. Configure Environment Variables

Copy the example environment file:

```bash
cp .env.example .env
```

Edit `.env` and add your API keys for the LLM providers you want to use:

```bash
# LLMS - Add keys for the providers you want to use
OPENAI_API_KEY=your_openai_api_key_here
MISTRAL_API_KEY=your_mistral_api_key_here
ANTHROPIC_API_KEY=your_anthropic_api_key_here

# Google (for Gemini)
GOOGLE_APPLICATION_CREDENTIALS=path_to_service_account.json
# OR
GOOGLE_API_KEY=your_google_api_key_here

# AWS Bedrock
BEDROCK_AWS_REGION=us-east-1
BEDROCK_AWS_ACCESS_KEY_ID=your_access_key
BEDROCK_AWS_SECRET_ACCESS_KEY=your_secret_key

# TOOLS (Optional)
TAVILY_API_KEY=your_tavily_search_key
NASA_API_KEY=your_nasa_api_key
```

### 3. Build the Project

```bash
npm run build
```

## Running Examples

The project includes many example scripts demonstrating different capabilities:

### Basic CLI Agent

```bash
npm run script -- --provider openAI --name "Your Name" --location "Your City"
```

### Simple Conversational Agent

```bash
npm run simple -- --provider anthropic --name "Assistant" --location "San Francisco"
```

### Code Execution Agent

```bash
npm run code_exec -- --provider openAI --name "Developer" --location "Seattle"
```

### Web Search Agent

```bash
npm run search -- --provider anthropic --name "Researcher" --location "Boston"
```

### Image Analysis Agent

```bash
npm run image -- --provider google --name "Analyst" --location "Austin"
```

### Streaming Example

```bash
npm run stream -- --provider anthropic --name "Streamer" --location "Portland"
```

## Available Providers

The following LLM providers are supported:

- **openAI**: OpenAI GPT models (requires OPENAI_API_KEY)
- **anthropic**: Anthropic Claude models (requires ANTHROPIC_API_KEY)
- **google**: Google Gemini models (requires GOOGLE_API_KEY or service account)
- **mistral**: Mistral AI models (requires MISTRAL_API_KEY)
- **azureOpenAI**: Azure OpenAI (requires Azure configuration)
- **ollama**: Local Ollama models (requires Ollama running locally)
- **deepseek**: DeepSeek models (requires DEEPSEEK_API_KEY)
- **xai**: xAI Grok models (requires XAI_API_KEY)
- **bedrock**: AWS Bedrock (requires AWS credentials)
- **vertexai**: Google Vertex AI (requires Google Cloud credentials)
- **openrouter**: OpenRouter (requires OPENROUTER_API_KEY)
- **perplexity**: Perplexity AI (requires PERPLEXITY_API_KEY)

## Script Parameters

All scripts accept these parameters:

- `--provider` (`-p`): LLM provider to use (default: openAI)
- `--name` (`-n`): User name for the conversation (default: Jo)
- `--location` (`-l`): User location (default: New York)
- `--help` (`-h`): Show help information

## Development

### Running Tests

```bash
npm test
```

### Linting and Formatting

```bash
npm run lint      # Fix linting issues
npm run format    # Format code with Prettier
```

### Development Build

```bash
npm run build:dev
```

## Project Structure

- `src/` - Source code
  - `scripts/` - Example scripts demonstrating various capabilities
  - `graphs/` - LangGraph implementations
  - `tools/` - Tool integrations (search, code execution, etc.)
  - `llm/` - LLM provider implementations
  - `types/` - TypeScript type definitions
- `dist/` - Built distribution files
- `config/` - Configuration files

## Troubleshooting

### Common Issues

1. **"API key not found" errors**: Make sure you've set the appropriate API key in your `.env` file for the provider you're using.

2. **Module resolution errors**: Try running `npm run reinstall` to clean and reinstall dependencies.

3. **TypeScript compilation errors**: Ensure you're using Node.js 14+ and run `npm run build` first.

4. **Experimental loader warnings**: These are normal and can be ignored - they're related to TypeScript path mapping.

### Getting API Keys

- **OpenAI**: https://platform.openai.com/api-keys
- **Anthropic**: https://console.anthropic.com/
- **Google**: https://console.cloud.google.com/
- **Mistral**: https://console.mistral.ai/
- **Tavily**: https://tavily.com/

## Use as Library

This project can also be used as a library in other projects:

```typescript
import { Run } from '@librechat/agents';

const agent = await Run.create({
  provider: 'openAI',
  // ... other configuration
});

const response = await agent.runStream({
  message: 'Hello, how can you help me?',
});
```

## Contributing

This is an open-source project under the MIT license. See the `LICENSE` file for details.
