# Ollama Provider Fork for the Vercel AI SDK

The **[Ollama Provider Fork](https://github.com/robustonian/ollama-ai-provider-fork)** for the [Vercel AI SDK](https://sdk.vercel.ai/docs)
contains enhanced language model support for the Ollama APIs with improved streaming and tool calls support, plus embedding model support for the Ollama embeddings API.

## Requirements

This provider requires Ollama >= 0.5.0

## Setup

The Ollama provider fork is available in the `ollama-ai-provider-fork` module. You can install it with

```bash
pnpm add @robustonian/ollama-ai-provider-fork
```

## Provider Instance

You can import the default provider instance `ollama` from `@robustonian/ollama-ai-provider-fork`:

```ts
import { ollama } from '@robustonian/ollama-ai-provider-fork';
```

## Example

```ts
import { ollama } from '@robustonian/ollama-ai-provider-fork';
import { generateText } from 'ai';

const { text } = await generateText({
  model: ollama('phi3'),
  prompt: 'Write a vegetarian lasagna recipe for 4 people.',
});
```

## Enhanced Features

This fork includes:
- Enhanced streaming support
- Improved tool calls functionality 
- Better inference from streaming responses
- Comprehensive test coverage for Node.js and Edge environments

## Documentation

Please check out the **[Ollama provider documentation](https://github.com/robustonian/ollama-ai-provider-fork)** for more information.
