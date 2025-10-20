# Server (API & Agent Host)

Purpose
- Express-based API that manages AI agent bot users and hosts agent implementations.
- Creates bot Stream clients, issues tokens, and loads agent implementations that listen to channel messages.

Quick start
1. cd server
2. npm install
3. Set required environment variables (see list below)
4. npm run dev (or npm run build && npm start)

Exposed API endpoints (defined in [server/src/index.ts](server/src/index.ts))
- GET / — health + activeAgents
- POST /start-ai-agent — start an AI agent for a channel (see handler in [server/src/index.ts](server/src/index.ts))
- POST /stop-ai-agent — stop and dispose an AI agent
- GET /agent-status — returns "connected" | "connecting" | "disconnected"
- POST /token — issues Stream tokens for clients

Key files & symbols
- [server/src/index.ts](server/src/index.ts) — main Express server and API handlers; the endpoints above are implemented here.
- [server/src/serverClient.ts](server/src/serverClient.ts) — server-side Stream client and exported symbol [`serverClient`](server/src/serverClient.ts).
- [server/src/agents/createAgent.ts](server/src/agents/createAgent.ts) — factory that creates agent instances; see symbol [`createAgent`](server/src/agents/createAgent.ts).
- [server/src/agents/openai/OpenAIAgent.ts](server/src/agents/openai/OpenAIAgent.ts) — OpenAI-based agent implementation; class [`OpenAIMedicalAgent`](server/src/agents/openai/OpenAIAgent.ts).
- [server/src/agents/groq/rag.ts](server/src/agents/groq/rag.ts) and [server/src/agents/groq/GroqAiAgent.ts](server/src/agents/groq/GroqAiAgent.ts) — GROQ-backed agent implementations; see [`GroqMedicalAgent`](server/src/agents/groq/GroqAiAgent.ts).
- [server/src/agents/types.ts](server/src/agents/types.ts) — shared AIAgent typing and platform enums.

Required environment variables
- STREAM_API_KEY
- STREAM_API_SECRET
- OPENAI_API_KEY (for OpenAI agent)
- GROQ_API_KEY (if using GROQ agent)
- TAVILY_API_KEY (GROQ agent integrations)
- PINECONE_API_KEY (if using Pinecone in RAG pipelines)
- TWILIO_ACCOUNT_SID, TWILIO_AUTH_TOKEN (if Twilio is used)

Behavior notes
- The server maintains an in-memory `aiAgentCache` and `pendingAiAgents` (see [server/src/index.ts](server/src/index.ts)).
- Agents must implement `init`, `dispose`, and `getLastInteraction()` as per the AIAgent interface in [server/src/agents/types.ts](server/src/agents/types.ts).
- Long-running agent resources are cleaned up on idle (inactivity threshold logic in [server/src/index.ts](server/src/index.ts)).

Security
- Keep `STREAM_API_SECRET` and other secrets out of version control.
- The server issues short-lived tokens via POST /token (see implementation in [server/src/index.ts](server/src/index.ts)).