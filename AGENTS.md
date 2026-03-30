# AGENTS.md - Developer Guidelines

## Project Overview

Next.js static site deployed to GitHub Pages at snetcher.github.io/snetcher.

## Build / Lint / Test Commands

### Running the Project

```bash
# Development server
npm run dev

# Build for production (outputs to /out)
npm run build

# Preview production build
npm run preview
```

### Linting

```bash
# Run linter
npm run lint
```

### GitHub Pages Deployment

Deployment happens automatically via GitHub Actions on push to main.
Manual build output is in `/out` directory.

## Code Style Guidelines

### TypeScript Conventions

- Use TypeScript with strict mode
- Prefer `const` over `let`; avoid `var`
- Use ES6+ features: arrow functions, destructuring, spread operator, async/await
- Explicitly type function parameters and return types
- Use interfaces for object shapes, types for unions/aliases
- Avoid `any`; use `unknown` when type is truly unknown

### Naming Conventions

| Element | Convention | Example |
|---------|------------|---------|
| Files | kebab-case | `user-service.ts` |
| Components | PascalCase | `UserProfile.tsx` |
| Functions | camelCase | `getUserData()` |
| Variables | camelCase | `isActive` |
| Constants | UPPER_SNAKE | `MAX_RETRY_COUNT` |
| Interfaces | PascalCase | `UserInterface` |

### Import Organization

1. External libraries (React, Next.js, etc.)
2. Internal modules (paths aliased with `@/` )
3. Relative imports
4. Type imports

```typescript
import { useState } from 'react'
import Link from 'next/link'
import { Button } from '@/components/ui'
import { UserCard } from './UserCard'
import type { User } from '@/types'
```

### Formatting

- Use **2 spaces** for indentation
- Use semicolons in JavaScript
- Use single quotes for strings

### Component Guidelines

- Use functional components with hooks
- Keep components small
- Define prop types with TypeScript interfaces
- Destructure props in function signature

```typescript
interface UserCardProps {
  user: User
  onSelect?: (id: string) => void
}

export function UserCard({ user, onSelect }: UserCardProps) {
  return (
    <div onClick={() => onSelect?.(user.id)}>
      <span>{user.name}</span>
    </div>
  )
}
```

## File Structure

```
src/
├── app/              # Next.js app router
│   ├── layout.tsx    # Root layout
│   ├── page.tsx      # Home page
│   └── globals.css   # Global styles
├── public/          # Static assets
├── out/             # Build output (gitignored)
└── package.json
```

## Git Conventions

- Use meaningful commit messages
- Follow conventional commits: `type(scope): description`
- Types: feat, fix, docs, style, refactor, test, chore
