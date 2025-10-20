# Client (Web App)

Purpose
- Front-end React + TypeScript UI for the AI Medical Assistant.
- Built with Vite, Tailwind CSS, and Stream Chat React integration.

Quick start
1. cd client
2. npm install
3. npm run dev
4. Build: npm run build

Important environment variables
- VITE_BACKEND_URL — URL of the backend API (used in [`ChatProvider`](client/src/providers/chat-provider.tsx))
- VITE_STREAM_API_KEY — Stream API key (used in [`ChatProvider`](client/src/providers/chat-provider.tsx))

Key files
- [client/package.json](client/package.json) — npm scripts, dependencies.
- [client/vite.config.ts](client/vite.config.ts) — Vite configuration.
- [client/src/providers/chat-provider.tsx](client/src/providers/chat-provider.tsx) — chat client creation and token provider; see symbol [`ChatProvider`](client/src/providers/chat-provider.tsx).
- [client/src/hooks/use-ai-agent-status.tsx](client/src/hooks/use-ai-agent-status.tsx) — hook used to monitor and control AI agent status; see symbol [`useAIAgentStatus`](client/src/hooks/use-ai-agent-status.tsx) and type [`AgentStatus`](client/src/hooks/use-ai-agent-status.tsx).
- [client/src/components/ai-agent-control.tsx](client/src/components/ai-agent-control.tsx) — UI control for connect/disconnect and status display; see symbol [`AIAgentControl`](client/src/components/ai-agent-control.tsx).
- [client/src/components/chat-interface.tsx](client/src/components/chat-interface.tsx) — main chat UI wiring and usage of the AI controls.
- [client/src/components/chat-sidebar.tsx](client/src/components/chat-sidebar.tsx) — channel list and navigation.
- [client/src/hooks/use-theme.ts](client/src/hooks/use-theme.ts) & [client/src/providers/theme-provider.tsx](client/src/providers/theme-provider.tsx) — theme handling.

Notes
- The client calls backend endpoints: `/start-ai-agent`, `/stop-ai-agent`, `/agent-status`, and `/token` (see server README).
- Ensure VITE_BACKEND_URL is set to the running server URL before starting the client.s