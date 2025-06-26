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
- **Language Model**: `ollama-chat-language-model.ts` - Chat completion implementation
- **Embedding Model**: `ollama-embedding-model.ts` - Text embedding functionality
- **Tool Generation**: `generate-tool/` - Enhanced tool call inference and streaming
- **Message Conversion**: `convert-to-ollama-chat-messages.ts` - Transforms AI SDK messages to Ollama format
- **Utilities**: `utils/` - Response handling, text streaming, and helper functions

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
Tests are split between Node.js and Edge runtime environments using separate Vitest configurations. The package ensures compatibility across both platforms.