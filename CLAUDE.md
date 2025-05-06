# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Build Commands
- `pnpm dev` - Start development server
- `pnpm build` - Build for production
- `pnpm preview` - Preview production build locally
- `pnpm astro check` - Type-check the codebase
- `pnpm astro --help` - Show all available Astro commands

## Code Style Guidelines
- **TypeScript**: Use strict mode with null checks enabled
- **Components**: Follow Astro component patterns (.astro files)
- **Imports**: Use named imports; maintain clean import sections
- **Formatting**: Use 2-space indentation
- **Naming**: Use camelCase for variables/functions, PascalCase for components
- **Content**: Follows schema defined in content.config.ts
- **Node Version**: Use Node 22 as specified in .nvmrc
- **Package Manager**: Use pnpm v10.0.0 for consistent dependency management

Refer to Astro documentation for best practices: https://docs.astro.build/