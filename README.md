# ollama-ai-provider-fork

A fork of [ollama-ai-provider](https://github.com/FabianMHz15/ollama-ai-provider) with enhanced streaming and tool calls support for the Vercel AI SDK.

## Features

- **Enhanced Streaming**: Improved streaming support for text and object generation
- **Tool Calls**: Enhanced tool call inference from streaming responses
- **Multimodal Support**: Text and image processing capabilities
- **Edge Runtime**: Compatible with both Node.js and Edge runtime environments
- **Type Safety**: Full TypeScript support with strict typing

## Installation

```bash
npm install ollama-ai-provider-fork
# or
pnpm add ollama-ai-provider-fork
# or
yarn add ollama-ai-provider-fork
```

## Quick Start

```typescript
import { ollama } from 'ollama-ai-provider-fork';
import { generateText } from 'ai';

const { text } = await generateText({
  model: ollama('llama3.1'),
  prompt: 'Hello, world!',
});

console.log(text);
```

## Usage Examples

### Text Generation with Streaming

```typescript
import { ollama } from 'ollama-ai-provider-fork';
import { streamText } from 'ai';

const { textStream } = await streamText({
  model: ollama('llama3.1'),
  prompt: 'Write a short story about AI.',
});

for await (const delta of textStream) {
  process.stdout.write(delta);
}
```

### Tool Calls

```typescript
import { ollama } from 'ollama-ai-provider-fork';
import { generateText } from 'ai';
import { z } from 'zod';

const { text } = await generateText({
  model: ollama('llama3.1'),
  tools: {
    weather: {
      description: 'Get weather information',
      parameters: z.object({
        location: z.string(),
      }),
    },
  },
  prompt: 'What is the weather like in Tokyo?',
});
```

### Object Generation

```typescript
import { ollama } from 'ollama-ai-provider-fork';
import { generateObject } from 'ai';
import { z } from 'zod';

const { object } = await generateObject({
  model: ollama('llama3.1'),
  schema: z.object({
    name: z.string(),
    age: z.number(),
    city: z.string(),
  }),
  prompt: 'Generate a person profile',
});
```

## Configuration

```typescript
import { createOllama } from 'ollama-ai-provider-fork';

const ollama = createOllama({
  baseURL: 'http://localhost:11434', // Ollama server URL
  headers: {
    'Custom-Header': 'value',
  },
});
```

## Development

This project uses pnpm workspaces and follows a monorepo structure:

```bash
# Install dependencies
pnpm install

# Build the package
pnpm build

# Run tests
pnpm test

# Run tests in specific environments
pnpm test:node
pnpm test:edge

# Lint code
pnpm lint

# Type check
pnpm type-check
```

## Project Structure

- `packages/ollama/` - Core AI provider package
- `examples/ai-core/` - Core AI functionality examples
- `examples/weather-ollama/` - Next.js weather app example

## Requirements

- Node.js 18+ or compatible runtime
- Ollama server running locally or accessible via network

## License

This project is licensed under the Apache 2.0 License. See [LICENSE](./LICENSE.md) and [NOTICE](./NOTICE.md) for details.

## Credits

This is a fork of Fabian Marquez’s fork of the original project [ollama-ai-provider](https://github.com/sgomez/ollama-ai-pr), which was originally created by sgomez.

