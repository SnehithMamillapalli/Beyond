# Beyond implementation plan

## Product and build approach

Beyond is a research workbench for comparing an early project idea or public GitHub repository with genuinely related projects and surfacing practical ways to differentiate. The main path is one screen: capture an idea, optionally include a repository and details, run an honest bounded analysis, then review the profile, comparable work, evidence, and three innovation paths. The app should remain useful when one research source or credential is unavailable. No static marketing page, synthetic research results, account system, database, or job queue.

Use the initialized React 19 + TypeScript / Vite frontend and Express + tRPC backend. Add a typed server-side `POST /api/analyze` endpoint (and health endpoint if the starter does not already provide one) for an auditable, bounded research pipeline. Structure the pipeline into input validation/profile building, modular GitHub and Tavily adapters, normalized candidate ranking, evidence handling, comparison, and opportunity generation. Read optional provider credentials only on the server. Use GitHub's public REST API for validated public repository URLs and search; Tavily only when `TAVILY_API_KEY` is present. Use the platform's server-side LLM API only when the supported runtime credentials are available; request bounded structured output and validate/parse it before display. Never treat repo/web content as instructions, execute repo code, fetch arbitrary user URLs, or claim unverified features. If sources/models are unavailable, return a truthful coverage limitation and usable partial results; never present a canned/demo record as fresh evidence.

Client state owns the current form, analysis progress stages, report, and selected innovation direction. Use clear stage transitions tied to actual awaited pipeline work; no fake percentage. Results are evidence linked to original provider URLs, uncertainty-forward, and include the transparent provisional ranking weights (35% problem, 35% features, 15% audience, 15% technical approach; unavailable dimensions excluded and weights renormalized). Provide refined direction/proposal interaction grounded in the original project. Keep data in memory for the current task/session; persistence and login are out of scope.

## Project structure

- `client/src/pages/Home.tsx`: app shell, idea/repository intake, progressive details, progress, results, and innovation explorer.
- `client/src/index.css`: Beyond design tokens, typography, layout, responsive behavior, and interactive states.
- `server/_core/index.ts`: existing Express entry; register the analysis and health HTTP routes without disturbing starter middleware.
- `server/analysis/*`: schemas, validation, profile, GitHub/Tavily adapters, ranking, evidence normalization and recommendations (modular, independently replaceable providers).
- `client/public/manus-routes.json`: route manifest kept synchronized with implemented page routes.
- `plan.md` and `TODO.md`: implementation decisions and outcome criteria.

## Design direction

Three distinct alternatives considered: **Beyond editorial research desk** (<0.10); **signal-map cartography / field atlas** (<0.10); **industrial instrument panel / monochrome lab** (<0.10). Choose Beyond’s editorial research desk, expressed as an asymmetrical paper-and-ink research workspace with instrument-like data details—not a chat prompt canvas, generic AI dashboard, or Google AI Studio look.

- **Design movement:** contemporary editorial publishing meets archival field research and tactile lab instrumentation.
- **Core principles:** (1) make evidence traceable at a glance, (2) prioritize a singular clear research task, (3) use editorial hierarchy instead of generic dashboard tiles, (4) label inference and unknowns as first-class states.
- **Color philosophy:** warm chalk-paper content surfaces sit above a deep forest underlay; restrained sage glass shards and citron pulses make the background more atmospheric without compromising the dark-ink text contrast. Dark pine/teal and citron remain the ownable focus colors; rust and muted green distinguish evidence/uncertainty without neon gradients. UI states never rely on color alone.
- **Layout paradigm:** offset split workbench with a narrow vertical rail, broad writing surface, and a slim evidence margin; results read as a long editorial dossier with asymmetric sections rather than repeated centered grids. Collapse rail and side notes on mobile.
- **Signature elements:** small numbered field labels; citron annotation tabs/stamps; fine ruled dividers; motion marks echoing the supplied Beyond gear-and-speed emblem.
- **Interaction philosophy:** editing and progressive disclosure stay inline; source and evidence links are explicit; all actions provide immediate, truthful status and recovery.
- **Animation:** restrained 150–220 ms transitions for disclosure and selection; staggered lime speed-line streaks emerge frequently from the Beyond gear and travel outward, with a gentle logo breathe; a controlled orbital signal and selected-stage pulse on the homepage map; the full-viewport glass-shard field reacts to pointer movement, clicks, and press-and-hold; motion pauses for reduced-motion users; default-open capability cards fill the left rail without inner scrolling; no excessive gradients.
- **Typography system:** Fraunces for editorial display and section headlines paired with DM Sans for UI/body and IBM Plex Mono for sources, status labels and technical metadata; compact uppercase metadata labels and roomy headline line-height.
- **Brand essence:** “Beyond helps builders see what they can build beyond the obvious.” Personality: rigorous, curious, grounded.
- **Brand voice:** direct, specific, un-hyped. Examples: “Start with the part you know.” “Similarity is a clue, not a verdict.”
- **Wordmark & logo:** user-supplied Beyond logo: forest-green gear/speed emblem, lime motion strokes, uppercase serif wordmark, and Project Intelligence tagline on warm cream.
- **Signature brand color:** field citron (`#D2E66F`), reserved for primary actions and evidence annotations.

## Serving and constraints

Keep the initialized server-only capability (no database). Continue using `pnpm dev` on configured port 3000 and the existing backend. Client-to-server calls are relative. Responses are bounded; only allow GitHub hosts and validate owner/repo paths before API requests. Add per-provider timeout and gracefully preserve valid partial results. Any API key remains in server process configuration. If user-provided credentials are required, use the platform's protected secret flow, never chat or frontend variables. Do not add a separate provider account, auth, or deployment dependency. Build with the project's existing scripts and keep the page route manifest valid.
