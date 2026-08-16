# Vincent DiPaola

**I build AI agents for revenue and operations workflows, plus the inspection machinery that decides whether their output is allowed to ship.**

Eleven years running NYC hospitality (Eleven Madison Park, Maialino), then five years carrying quota at Cision/PR Newswire on a $1.6M ARR portfolio, now building applied AI full time. That order shaped how I build. I have been the person who lives with a system after the demo ends, so the work I want judged on lives with gates, evals, traces, and a named human who signs off.

One idea runs through the systems below:

> **Autonomy is earned, not configured.**

The usual answer to "is this agent safe to deploy" is another approval step. Six months later the agent is wrapped in so much oversight that it can barely act, and the team quietly decides AI was overhyped. I would rather measure what an agent has earned and move the dial on evidence.

Not every public repo is production. Seeded builders, fixture demos, and mock adapters are labeled in those READMEs.

---

## Policy-bound systems

Deterministic code decides. Models propose. Open these first.

### [SpendForge](https://github.com/VJDiPaola/SpendForge)
An AI agent proposes a purchase. Typed code decides whether it happens. The model never holds payment authority. One policy engine, integer money, fail-closed gates, and a receipt you can inspect. The public demo is fixture-first; live Rain and live OpenAI were proven on separate paths and labeled as such.

> **Trade-off:** the public deployment does not spend real money. Passing policy is not the same as buying.

`TypeScript` · `deterministic policy` · `163 tests` · `CI verify`

### [software-factory](https://github.com/VJDiPaola/software-factory)
Spec in, gated and reviewed code out. Parallel builders work over disjoint file ownership, a deterministic gate decides what ships, one bounded repair gets a second try, and a human makes the release call. It reports **first-pass yield**, which counts only units clean on attempt 1, so a factory that repairs everything cannot report 100%. Builders in this repo are seeded recordings, not live LLM calls.

> **Trade-off:** the reviewer model is structurally unable to clear a gate failure. It can slow a release down and never authorize one. There is a test asserting the override path does not exist.

`Python` · `deterministic gates` · `CI-asserted yield`

---

## Measured and shipped

Eval discipline, a skill linter, a live product, and a personal tool. Not the same maturity as the two above.

### [auction-agent-evals](https://github.com/VJDiPaola/auction-agent-evals)
ScrabbleBot strategy for TheEcho — a real-time letter-auction bot — plus an offline Monte Carlo eval harness. Not an LLM-agent eval framework. Twenty A/B runs at N=300 to 400, each with a 95% confidence interval and a verdict.

Of those twenty experiments, **7 improved the agent, 6 made it measurably worse, and 7 changed nothing at all.** The one finding worth keeping: raising the bid valuation gained **+42.99 points per match (±2.60, 95% CI) at a 92% win rate.**

> **Trade-off:** I kept the negative and null results in the repo. Thirteen of twenty changes were not improvements, and publishing that is the only reason the one real win is worth believing.

`TypeScript` · `SpacetimeDB` · `parameter sweeps` · `Vickrey auction modeling`

### [skill-forge](https://github.com/VJDiPaola/skill-forge)
A 19-check CI gate for AI coding-agent skills. Skill libraries rot silently: a description stops describing a trigger, a cross-link dangles, a project name leaks into a general skill. None of it throws an error. The skills in the tree are the test corpus. The product is the harness.

> **Trade-off:** three severity levels, but only errors fail the build. A gate that fails on style opinions gets switched off within a week. Grade A is a linter grade, not proof the skills make agents better.

`Python` · `GitHub Actions` · `schema validation`

### [earned-autonomy](https://github.com/VJDiPaola/earned-autonomy)
A support agent whose tool permissions are earned. Every side-effecting action type starts at a low tier. An LLM-as-judge scores traces, a reflection agent files a promotion request citing Phoenix trace IDs, and a human approves. Demotions apply immediately. Hosted demo of the loop; the repo does not yet have CI tests that reproduce it from a cold clone.

> **Trade-off:** promotions require human approval, demotions apply instantly. Asymmetric on purpose, because a wrongly trusted agent costs more than a slowly promoted one.

`Google ADK` · `Arize Phoenix` · `FastAPI` · `Cloud Run`

### [ADHD-OS](https://github.com/VJDiPaola/ADHD-OS)
A personal CLI for ADHD executive function: start the task, calibrate time, reality-test the spiral. Local SQLite, crisis keywords that bypass the model, CI on the code paths that do not need API keys. Not an ops or eval platform.

> **Trade-off:** a separate agent per function rather than one prompt with many jobs, so a bad response in one mode does not contaminate the others. Routing quality is not eval-gated.

`Python` · `Google ADK` · `personal product`

### [ResumeTailor](https://github.com/VJDiPaola/LinkedIn-Resume-Builder)
A shipped Next.js app at [resumetailor.teamvince.com](https://resumetailor.teamvince.com). Job posting in, structured resume and LinkedIn copy out, through a signed-session proxy, rate limits, and Zod contracts. Product engineering, not agent infrastructure.

> **Trade-off:** one model call, no persistence. The interesting part is the request path, not the prompt.

`TypeScript` · `Next.js` · `Vitest` · `live`

---

## Prototypes and talks

Hackathon snapshots and early tooling. Useful for velocity. Not how I deploy agents.

### [RefereeOS](https://github.com/VJDiPaola/RefereeOS)
Hackathon prototype for preprint triage. Six review stages write one shared evidence board; a Daytona probe runs when credentials exist; the output prepares human review rather than a publication decision. Fixture-driven by default.

> **Trade-off:** a shared evidence board instead of agent-to-agent chat. Slower and more verbose, and in exchange every claim has one inspectable source of truth.

`AG2` · `Daytona` · `FastAPI` · `hackathon prototype`

### [commons-copilot](https://github.com/VJDiPaola/commons-copilot)
Hackathon demo of room coordination. The app UI and agent loop use a local mock adapter; Demo Mode is a scripted timeline. Separate scripts touched the live Spacebase1 network and are labeled as such.

> **Trade-off:** no central planner. Nothing guarantees a match gets made, and nothing is a single point of failure either.

`Next.js` · `mock-backed demo`

---

## Shipping next

- **An evidence-gated renewal agent for GTM teams.** Structured claims bound to source records, deterministic checks that can hard-stop a release, one bounded self-repair, and a human approval before anything leaves the system.

---

## Writing

I write up what I build at [teamvince.com](https://teamvince.com).

- [Your Agent Doesn't Need More Guardrails. It Needs a Track Record.](https://teamvince.com/blog/agent-track-record-not-guardrails)
- [Every Approval Prompt Was Making You a Worse Operator](https://teamvince.com/blog/approval-fatigue-fake-control)
- [Running Four Coding Agents in Parallel](https://teamvince.com/blog/parallel-coding-agents)
- [From Restaurants to AI: What Hospitality Taught Me](https://teamvince.com/blog/from-restaurants-to-ai)
- [Earned Autonomy: An AI Agent That Earns Its Permissions](https://teamvince.com/blog/earned-autonomy-eval-gated-agent)

---

Brooklyn, NY · [teamvince.com](https://teamvince.com) · [LinkedIn](https://linkedin.com/in/vincent-dipaola) · vincentjdipaola@gmail.com
