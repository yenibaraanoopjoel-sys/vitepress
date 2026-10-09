# VitePress Development Environment Setup

This document records the setup and verification steps for developing and contributing to VitePress:

## 1. Prerequisites
- Node.js >= 18.0.0
- pnpm >= 9.0.0

## 2. Installation & Verification
- Workspace dependencies installed via `pnpm install`
- Type checking verified with `pnpm run typecheck`
- Unit tests executed using `npm run test:unit`
- Local dev documentation server tested via `pnpm run docs:dev`

## 3. Contributing Workflow
- Create a feature or bugfix branch off `main`
- Ensure all unit tests pass before submitting
- Follow Conventional Commits format for commit messages
