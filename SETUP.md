# Beyond setup

Beyond is a React/TypeScript interface with an Express research API. It does not use a database, account system, vector database, or job queue; results remain in the current page session.

## Run locally

Use the repository’s pinned pnpm toolchain, then run `pnpm dev`. The server listens on `PORT` (default 3000). `GET /api/health` reports provider availability without exposing credentials. `POST /api/analyze` returns JSON; `POST /api/analyze/stream` emits real research-stage events, a source-tagged profile preview before discovery begins, then the final report. The server accepts at most four concurrent analyses. Requests, provider response bodies, repository inspections, and README excerpts are bounded.

## Research providers

GitHub search and public repository inspection use the official GitHub REST API. Public unauthenticated requests work with lower rate limits; `GITHUB_TOKEN` is optional and should be stored as a server-only environment secret if a higher limit is needed. For each analysis, the app inspects at most five strongest discovered repositories, plus an explicitly supplied repository, using metadata and a capped README excerpt. It does not execute code or claim full functionality from a README or file’s presence.

Wider-web product and documentation discovery uses Tavily Search API. `TAVILY_API_KEY` must be configured as a protected server-side project secret. If Tavily is absent or unavailable, the report names that coverage gap and uses any valid GitHub evidence; it does not show synthetic records as live results.

Profile and comparison interpretation use WebDev’s managed server-side `invokeLLM` helper and the catalog-listed `gpt-5-mini` model with minimal reasoning. No separate user AI key is required. Profile extraction uses strict JSON-schema output; nested comparison synthesis uses JSON-object mode plus server-side field validation. If synthesis is unavailable or truncated, the app reports that limitation and falls back to a conservative same-problem/workflow shortlist and explicitly identified hypotheses.

## Input and interpretation

Only supported public GitHub owner/repository URLs on `github.com` are accepted; the app never fetches an arbitrary URL supplied by a user. GitHub API and Tavily are the only external sources fetched server-side. User prompts, repository text, and web snippets are untrusted evidence—not instructions. Provider response bodies are capped at 512 KiB, request bodies have a size limit, and provider reads have timeouts.

Similarity is a provisional heuristic using problem similarity (35%), feature overlap (35%), target-user similarity (15%), and technical approach similarity (15%). Dimensions without enough support are excluded and remaining weights are renormalized. It does not measure project quality or novelty. Text overlap in a README or snippet is not proof that a feature works; absence from inspected evidence is not proof that a capability is absent. Linked search records are discovery metadata, not independently crawled pages. Treat the three innovation directions as experiments, not guarantees of novelty or success.
