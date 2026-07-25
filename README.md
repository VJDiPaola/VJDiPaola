# Vincent DiPaola

**I build AI agents for revenue and operations workflows, plus the inspection machinery that decides whether their output is allowed to ship.**

Eleven years running NYC hospitality (Eleven Madison Park, Maialino), then five years carrying quota at Cision/PR Newswire on a $1.6M ARR portfolio, now building applied AI full time. That order shaped how I build. I have been the person who lives with a system after the demo ends, so what I ship comes with gates, evals, traces, and a named human who signs off.

One idea runs through all of it:

> **Autonomy is earned, not configured.**

The usual answer to "is this agent safe to deploy" is another approval step. Six months later the agent is wrapped in so much oversight that it can barely act, and the team quietly decides AI was overhyped. I would rather measure what an agent has earned and move the dial on evidence. Each project below builds one piece of that machinery.

---

## AI deployment

Shipping into a real workflow, with cost boundaries, honest metrics, and a human release decision.

### [software-factory](https://github.com/VJDiPaola/software-factory)
Spec in, gated and reviewed code out. Parallel builders work over disjoint file ownership, a deterministic gate decides what ships, one bounded repair gets a second try, and a human makes the release call. It reports **first-pass yield**, which counts only units clean on attempt 1, so a factory that repairs everything cannot report 100%.

> **Trade-off:** the reviewer model is structurally unable to clear a gate failure. It can slow a release down and never authorize one. There is a test asserting the override path does not exist.

`Python` · `deterministic gates` · `parallel agents` · `CI-asserted yield`

### [earned-autonomy](https://github.com/VJDiPaola/earned-autonomy)
A support agent whose tool permissions are earned. Every side-effecting action type starts at tier 0. An LLM-as-judge eval runner scores real tickets, a reflection agent reads those results through the Phoenix MCP server, and it files a promotion request citing trace IDs as evidence. A human approves, and the risk gate behaves differently on the very next tool call.

> **Trade-off:** promotions require human approval, demotions apply instantly. Asymmetric on purpose, because a wrongly trusted agent costs more than a slowly promoted one.

`Google ADK` · `Gemini 3.1 Pro` · `Arize Phoenix` · `FastAPI` · `Cloud Run`

### [auction-agent-evals](https://github.com/VJDiPaola/auction-agent-evals)
An offline eval suite for a real-time auction agent, built so tuning decisions came from measurement instead of intuition. Twenty A/B runs at N=300 to 400, each with a 95% confidence interval and a verdict.

Of those twenty experiments, **7 improved the agent, 6 made it measurably worse, and 7 changed nothing at all.** The one finding worth keeping: raising the bid valuation gained **+42.99 points per match (±2.60, 95% CI) at a 92% win rate.**

> **Trade-off:** I kept the negative and null results in the repo. Thirteen of twenty changes were not improvements, and publishing that is the only reason the one real win is worth believing.

`TypeScript` · `SpacetimeDB` · `parameter sweeps` · `Vickrey auction modeling`

---

## Agent orchestration

Multi-agent topologies someone else can read, reason about, and debug.

### [RefereeOS](https://github.com/VJDiPaola/RefereeOS)
Multi-agent preprint triage. Six specialized review stages read and write one shared evidence board, a reproducibility probe executes in a Daytona sandbox, and the output is a packet that prepares human review rather than a publication decision. It also scans for prompt-injection text before passing anything to a review agent. First place, Scientific Track, AG2 Hackathon.

> **Trade-off:** a shared evidence board instead of agent-to-agent chat. Slower and more verbose, and in exchange every claim has one inspectable source of truth and any stage can be rerun in isolation.

`AG2` · `Daytona` · `FastAPI` · `GPT-5.5` · `Gemini`

### [commons-copilot](https://github.com/VJDiPaola/commons-copilot)
Coordination for a room full of people, with no orchestrator. Independent agents scan a shared intent log, post matches and critiques, and leave a visible trail of how coordination emerged. The README is explicit about which paths are mock-backed and which touched the live network.

> **Trade-off:** no central planner. Nothing guarantees a match gets made, and nothing is a single point of failure either.

`Next.js` · `Spacebase1` · `local-first`

### [ADHD-OS](https://github.com/VJDiPaola/ADHD-OS)
A roster of specialized agents for task initiation, time management, and emotional regulation.

> **Trade-off:** a separate agent per function rather than one prompt with many jobs, so a bad response in one mode does not contaminate the others.

`Python` · `multi-agent`

---

## Enterprise workflows

GTM, renewals, and operations. My sales background does the most work here.

### [ContextOS](https://github.com/VJDiPaola/ContextOS)
CLI and core library for portable AI context. Import, validate, and export project context across Claude, ChatGPT, and Cursor, so the context you built up in one tool is not stranded there.

> **Trade-off:** a validated schema over free-form markdown. More friction to author, and it makes context diffable, testable, and portable.

`TypeScript` · `vitest` · `monorepo`

### [skill-forge](https://github.com/VJDiPaola/skill-forge)
A skill library for AI coding agents with a CI quality gate. 38 skills, one canonical source synced to four tools, and an 18-check eval harness that fails the build on a malformed skill. Skill libraries rot silently: a description stops describing a trigger, a cross-link dangles, a project name leaks into a general skill and starts misfiring elsewhere. None of it throws an error.

> **Trade-off:** three severity levels, but only errors fail the build. A gate that fails on style opinions gets switched off within a week.

`Python` · `GitHub Actions` · `PowerShell + Bash` · `schema validation`

### [sales-prompt-library](https://github.com/VJDiPaola/sales-prompt-library)
Reusable AI prompts for sales workflows, written while carrying quota and adopted by the team around me.

---

## Shipping next

- **An evidence-gated renewal agent for GTM teams.** Structured claims bound to source records, deterministic checks that can hard-stop a release, one bounded self-repair, and a human approval before anything leaves the system. Public in August.

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
