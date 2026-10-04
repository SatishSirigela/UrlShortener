# URL Shortener + Agentic SDLC Orchestration (Prototype)

## Run
1. Restore/build in Visual Studio using __Restore NuGet Packages__ and __Build Solution__.
2. Run the API.
3. Open Swagger UI.

## API
- `POST /api/urls` → create short URL
- `GET /{code}` → redirect
- `GET /api/urls/{code}/analytics` → click analytics
- `POST /api/orchestration/run/{scenario}` where scenario is `greenfield`, `brownfield`, or `ambiguous`

## Orchestration model
- Explicit dependency graph (DAG) with stage gates.
- Parallel/sync path: `testing` and `docs` run after implementation; `release` waits for both.
- Human approval checkpoints (`RequiresHumanApproval`) for high-impact stages.
- Bounded retries, rollback hook, safe-stop.
- Decision lineage + reliability metrics in execution report.

## Scenarios
- **Greenfield:** full path from requirements to release.
- **Brownfield:** adds approval on implementation-impact stage.
- **Ambiguous:** same flow, but intended to capture uncertainty in requirement normalization and gate outcomes.

## Limitations / trade-offs
- In-memory DB for speed; swap with SQL provider for persistence.
- Dev approval service auto-approves; replace with real approval workflow.
- Policy guardrails are extension points; integrate org security/compliance controls.
