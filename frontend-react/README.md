# Mentis Frontend (React + Vite)

A lightweight, modularized React frontend for the Mentis AI platform, migrated from Next.js to Vite for improved performance and reduced bundle size.

## 🚀 Key Improvements Over Previous Frontend

### 1. **Unified ExecutionPanel Component** ✨
- **Before**: Separate execution panels for each agent (AegisExecutionPanel, CustomAgentExecutionPanel, SophiaSourcePanel) - 2,282 lines total
- **After**: Single, reusable ExecutionPanel component - 1,196 lines (**46% code reduction**)
- **Benefits**:
  - Consistent UX across all agents
  - Single source of truth for execution monitoring
  - Easy to maintain and extend
  - Type-safe with full TypeScript support

### 2. **Lightweight Build System**
- **Before**: Next.js (heavy, server-focused)
- **After**: Vite (fast, client-focused)
- **Benefits**:
  - ⚡ Lightning-fast hot module replacement (HMR)
  - 📦 Smaller bundle sizes
  - 🔧 Simpler configuration
  - 🎯 Focused on what we actually use (no SSR overhead)

### 3. **Proper Modularization**
- Clean separation of concerns
- Feature-based component organization
- Centralized state management
- Reusable UI components

## 📁 Project Structure

```
frontend-react/
├── src/
│   ├── components/          # React components
│   │   ├── ui/             # Base UI components (26 components)
│   │   ├── shared/         # Shared components (ExecutionPanel, etc.)
│   │   ├── chat/           # Chat-related components (15 components)
│   │   ├── agents/         # Agent-specific components
│   │   ├── knowledge/      # Knowledge base components
│   │   ├── flows/          # Flow builder components
│   │   ├── capabilities/   # Capabilities management
│   │   ├── hub/            # Hub (codebases, buckets)
│   │   ├── settings/       # Settings components
│   │   ├── tasks/          # Task management
│   │   ├── layout/         # Layout components (Header, Sidebar, Footer)
│   │   ├── markdown/       # Markdown rendering
│   │   ├── dialogs/        # Dialog components
│   │   └── providers/      # Provider components
│   ├── pages/              # Page components
│   │   ├── auth/           # Login, Register
│   │   ├── chat/           # Main chat interface
│   │   ├── knowledge/      # Knowledge management
│   │   ├── flows/          # Flow builder
│   │   ├── capabilities/   # Capabilities
│   │   ├── custom-agents/  # Custom agents
│   │   ├── hub/            # Hub
│   │   ├── tasks/          # Tasks
│   │   ├── workspace/      # Workspace
│   │   ├── library/        # Library
│   │   └── settings/       # Settings pages
│   ├── hooks/              # Custom React hooks (14 hooks)
│   ├── context/            # React Context providers
│   │   ├── ThemeProvider.tsx    # Dark/light mode
│   │   ├── ChatContext.tsx      # Chat state
│   │   └── OrganizationContext.tsx
│   ├── store/              # Zustand stores (4 stores)
│   │   ├── authStore.ts
│   │   ├── chatStore.ts
│   │   ├── knowledgeStore.ts
│   │   └── taskStore.ts
│   ├── lib/                # Utilities and libraries
│   │   ├── api.ts          # API client with SSE support
│   │   ├── types.ts        # TypeScript type definitions
│   │   ├── utils.ts        # Helper utilities
│   │   ├── constants.ts    # App constants
│   │   └── ...             # Other utilities
│   ├── App.tsx             # Main app component
│   ├── main.tsx            # Entry point
│   └── index.css           # Global styles
├── public/                 # Static assets
├── package.json            # Dependencies
├── vite.config.ts         # Vite configuration
├── tsconfig.json          # TypeScript configuration
└── tailwind.config.js     # Tailwind CSS configuration
```

## 🛠️ Tech Stack

- **React 18** - UI library
- **TypeScript** - Type safety
- **Vite** - Build tool and dev server
- **React Router 6** - Client-side routing
- **TanStack Query** - Server state management
- **Zustand** - Client state management
- **Tailwind CSS** - Styling
- **Radix UI** - Accessible component primitives
- **React Hook Form + Zod** - Form handling and validation
- **Monaco Editor** - Code editing
- **React Flow** - Flow visualization
- **Plotly.js** - Data visualization
- **React Markdown** - Markdown rendering

## 📦 Installation

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

## 🔧 Configuration

### Environment Variables

Create a `.env` file in the root directory:

```env
VITE_API_URL=http://localhost:8000
```

### API Integration

The frontend connects to the backend API at the URL specified in `VITE_API_URL`. The API client (`src/lib/api.ts`) handles:

- **Authentication** - JWT tokens stored in localStorage
- **Server-Sent Events (SSE)** - Real-time streaming for AI responses
- **REST API** - Standard CRUD operations
- **WebSocket** - Live updates

## 🎯 Key Features

### 1. All 5 AI Agents

- **Sophia** - Knowledge Base AI (document Q&A)
- **Aegis** - Research Agent (live research streaming)
- **Analytica** - Data Analytics (bucket analysis)
- **Clavis** - Code Analysis (codebase Q&A)
- **Custom Agents** - User-created agents

### 2. Unified Execution Panel

The new `ExecutionPanel` component works with all agents:

```tsx
import { ExecutionPanel } from '@/components/shared'

<ExecutionPanel
  messages={messages}
  parsedSources={sources}
  isStreaming={isStreaming}
  agentType="aegis"  // or "custom", "sophia", "generic"
  tabs={{ logs: true, output: true, sources: true, files: true }}
  progress={progressInfo}
  onResearchComplete={handleComplete}
/>
```

### 3. Knowledge Base Management

- Upload documents
- Create knowledge bases
- Query with Sophia
- Source tracking and citation

### 4. Flow Builder

- Visual flow creation with React Flow
- Node-based workflow design
- Execution history
- Flow templates

### 5. Custom Agents

- Create custom AI agents
- Configure capabilities
- Custom interface types (chat, form, JSON, API, wizard)
- Execution monitoring

### 6. Hub

- Manage codebases for Clavis
- Manage data buckets for Analytica
- Knowledge base browser

### 7. Task Management

- Background task tracking
- Progress monitoring
- Task history

### 8. Settings

- Profile management
- Organization settings
- Team members
- API keys
- Analytics

## 🎨 Theming

The app supports dark/light/system themes via the custom ThemeProvider:

```tsx
import { useTheme } from '@/context/ThemeProvider'

function MyComponent() {
  const { theme, setTheme } = useTheme()

  return (
    <button onClick={() => setTheme('dark')}>
      Switch to dark mode
    </button>
  )
}
```

## 🔐 Authentication

Authentication is handled by the `AuthProvider`:

```tsx
import { useAuth } from '@/components/auth/AuthProvider'

function MyComponent() {
  const { user, login, logout, isLoading } = useAuth()

  return (
    <div>
      {user ? (
        <button onClick={logout}>Logout</button>
      ) : (
        <button onClick={() => login(email, password)}>Login</button>
      )}
    </div>
  )
}
```

## 🔔 Toast Notifications

Toast notifications are available via the `useToast` hook:

```tsx
import { useToast } from '@/hooks/use-toast'

function MyComponent() {
  const { toast } = useToast()

  const handleClick = () => {
    toast({
      title: "Success!",
      description: "Your changes have been saved.",
      variant: "default",
    })
  }

  return <button onClick={handleClick}>Save</button>
}
```

## 📚 Component Documentation

### ExecutionPanel

See `src/components/shared/USAGE.md` for comprehensive usage guide and examples.

See `src/components/shared/DESIGN.md` for design decisions and architecture.

## 🚀 Deployment

### Build

```bash
npm run build
```

This creates an optimized production build in the `dist/` directory.

### Serve

The built files are static and can be served by any web server:

```bash
# Preview locally
npm run preview

# Or use any static file server
npx serve dist
```

### Docker

```dockerfile
FROM node:18-alpine as build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

## 🔍 Development

### Code Organization

- **Components**: Organized by feature/domain
- **Pages**: One component per route
- **Hooks**: Custom React hooks for reusable logic
- **Context**: Global state providers
- **Store**: Zustand stores for persistent state
- **Lib**: Utilities, types, constants, API client

### Best Practices

1. **Use TypeScript** - All new code should be properly typed
2. **Extract reusable logic** - Create custom hooks
3. **Keep components small** - Single responsibility
4. **Use the unified ExecutionPanel** - Don't create agent-specific execution panels
5. **Follow existing patterns** - Check similar components for guidance

## 🐛 Troubleshooting

### Build Errors

If you encounter build errors:

```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install

# Clear Vite cache
rm -rf node_modules/.vite
```

### Import Errors

All imports use the `@/` alias for the `src/` directory:

```tsx
// Good
import { Button } from '@/components/ui/button'
import { useAuth } from '@/components/auth/AuthProvider'

// Bad
import { Button } from '../../../components/ui/button'
```

### API Connection Issues

Make sure your backend is running and `VITE_API_URL` is set correctly in `.env`.

## 📝 Migration Notes

### From Next.js Frontend

This frontend replaces the Next.js version with the following changes:

1. **No Next.js specific code**:
   - ❌ `'use client'` directives
   - ❌ `next/link` → ✅ `react-router-dom`
   - ❌ `next/navigation` → ✅ `react-router-dom`
   - ❌ `next/image` → ✅ Regular `<img>` tags
   - ❌ `next-themes` → ✅ Custom `ThemeProvider`

2. **All functionality preserved**:
   - ✅ All 5 AI agents
   - ✅ Knowledge base management
   - ✅ Flow builder
   - ✅ Custom agents
   - ✅ Task management
   - ✅ Settings
   - ✅ Dark mode
   - ✅ Authentication
   - ✅ Real-time streaming
   - ✅ WebSocket support

3. **Improvements**:
   - ✅ Unified ExecutionPanel (46% code reduction)
   - ✅ Faster build times with Vite
   - ✅ Smaller bundle sizes
   - ✅ Better modularization
   - ✅ Cleaner architecture

## 📄 License

Copyright © 2024 Mentis. All rights reserved.

## 🤝 Contributing

This is a proprietary project. Please contact the development team for contribution guidelines.

## 📧 Support

For issues or questions, please contact the development team.

---

**Built with ❤️ using React + Vite**
