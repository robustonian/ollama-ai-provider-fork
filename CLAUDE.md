# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

This project uses pnpm workspaces and follows a monorepo structure:

- `pnpm build` - Build the main package
- `pnpm dev` - Start development mode with file watching
- `pnpm test` - Run all tests (node and edge environments)
- `pnpm lint` - Run ESLint across TypeScript files
- `pnpm type-check` - Run TypeScript type checking
- `pnpm prettier-check` - Check code formatting
- `pnpm clean` - Remove build artifacts

For testing specific environments:
- `pnpm test:node` - Run tests in Node.js environment
- `pnpm test:edge` - Run tests in Edge runtime environment

For package-specific development (from workspace root):
- `pnpm --filter ollama-ai-provider <command>` - Run commands in the core package
- `cd packages/ollama && pnpm <command>` - Alternative approach for package-specific commands

## Architecture

This is a fork of the ollama-ai-provider with enhanced streaming and tool calls support. The project structure:

### Monorepo Structure
- **Root**: Contains workspace configuration and shared tooling
- **packages/ollama/**: Core AI provider package implementing Vercel AI SDK interface
- **examples/**: Demo applications showcasing different use cases
  - `ai-core/`: Core AI functionality examples
  - `weather-ollama/`: Next.js weather app with Ollama integration

### Core Package (packages/ollama/)
The main package exports an Ollama provider that implements the Vercel AI SDK interface:

- **Provider Entry**: `ollama-provider.ts` - Main provider factory and configuration
- **Language Model**: `ollama-chat-language-model.ts` - Chat completion implementation with streaming support
- **Embedding Model**: `ollama-embedding-model.ts` - Text embedding functionality
- **Tool Generation**: `generate-tool/infer-tool-calls-from-stream.ts` - Enhanced tool call inference from streaming responses
- **Message Conversion**: `convert-to-ollama-chat-messages.ts` - Transforms AI SDK messages to Ollama format
- **Utilities**: `utils/` - Response handling, text streaming, and helper functions
  - `response-handler.ts` - Handles Ollama API responses and error mapping
  - `text-line-stream.ts` - Streaming text processing utilities
- **Settings**: Chat and embedding model configuration interfaces
- **Error Handling**: `ollama-error.ts` - Custom error types for Ollama interactions

### Key Features
- Streaming text and object generation
- Tool calling with improved inference from streams
- Multimodal support (text + images)
- Edge runtime compatibility
- Comprehensive test coverage for both Node.js and Edge environments

## Technology Stack
- TypeScript with strict type checking
- Vitest for testing in multiple environments
- tsup for building with both CJS and ESM output
- ESLint + Prettier for code quality
- Husky for git hooks
- Vercel AI SDK (@ai-sdk/provider) for interface compliance

## Testing
Tests are split between Node.js and Edge runtime environments using separate Vitest configurations:

- **Node.js Tests**: `vitest.node.config.js` - Standard Node.js environment testing
- **Edge Runtime Tests**: `vitest.edge.config.js` - Edge runtime environment testing for platform compatibility

The package ensures compatibility across both platforms. Tests cover:
- Message conversion and formatting
- Tool call inference from streaming responses
- Language model chat completions
- Embedding model functionality
- Response handling and error mapping

Run individual test suites with:
- `pnpm test:node` - Node.js environment only
- `pnpm test:edge` - Edge runtime environment only

## Examples Structure

The `examples/` directory contains comprehensive demonstrations:

### ai-core/
Extensive examples of core AI functionality organized by use case:
- **Text Generation**: `generate-text/` - Various text generation patterns including tool calls, multimodal, and streaming
- **Object Generation**: `generate-object/` - Structured output generation with schemas and validation
- **Text Streaming**: `stream-text/` - Real-time text streaming with tool calls and completion handling
- **Object Streaming**: `stream-object/` - Streaming structured object generation
- **Embeddings**: `embed/` and `embed-many/` - Text embedding and similarity computations
- **Complex Patterns**: `complex/` - Advanced use cases like math agents and semantic routing
- **Middleware**: `middleware/` - Custom middleware for logging, caching, and request modification
- **Tools**: `tools/` - Tool definitions and implementations

### weather-ollama/
Next.js application demonstrating real-world integration with:
- Server actions for AI interactions
- React components for chat UI
- Weather tool integration
- Streaming responses in web applications