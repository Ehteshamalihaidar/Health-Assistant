# Health-Assistant 

Repository overview
- client/ — React frontend (Vite + Tailwind + Stream Chat)
  - README: [client/README.md](client/README.md)
- server/ — Express backend and AI agent host
  - README: [server/README.md](server/README.md)
- rag/ — notebooks and RAG experiments
  - README: [rag/README.md](rag/README.md)

Getting started (development)
1. Install dependencies for both projects:
   - cd server && npm install
   - cd ../client && npm install
2. Start the server (server must be running for client to function):
   - cd server
   - Ensure env vars from [server/README.md](server/README.md) are set
   - npm run dev
3. Start the client:
   - cd client
   - Ensure VITE_BACKEND_URL points to the running server
   - npm run dev

Where to look for integration points
- Client calls backend endpoints in [client/src/hooks/use-ai-agent-status.tsx](client/src/hooks/use-ai-agent-status.tsx) via [`useAIAgentStatus`](client/src/hooks/use-ai-agent-status.tsx).
- Server creates and manages agent instances in [server/src/index.ts](server/src/index.ts) using [`createAgent`](server/src/agents/createAgent.ts) and the server Stream client from [server/src/serverClient.ts](server/src/serverClient.ts).
- Agent implementations:
  - OpenAI: [server/src/agents/openai/OpenAIAgent.ts](server/src/agents/openai/OpenAIAgent.ts) — [`OpenAIMedicalAgent`](server/src/agents/openai/OpenAIAgent.ts)
  - GROQ / RAG: [server/src/agents/groq/rag.ts](server/src/agents/groq/rag.ts) and [server/src/agents/groq/GroqAiAgent.ts](server/src/agents/groq/GroqAiAgent.ts) — [`GroqMedicalAgent`](server/src/agents/groq/GroqAiAgent.ts)

Contributing
- Follow TypeScript + ESLint rules in [client/eslint.config.js](client/eslint.config.js).
- Keep secrets out of git; use .env files or a secrets manager.
- Add tests near the code they validate. Use the existing project structure for new features.

Contact / Troubleshooting
- Check server logs (console) for agent lifecycle messages (start/stop/dispose) — handlers live in [server/src/index.ts](server/src/index.ts).
- If agents do not appear in channels, verify that tokens are issued by POST /token and that the server `aiAgentCache` contains the created bot user.
