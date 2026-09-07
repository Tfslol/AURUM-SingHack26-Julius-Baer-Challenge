# Aurum — RM Intelligence Workbench

Aurum is a local-first Streamlit prototype for the **SingHacks 2026 Julius Baer
Wealth Intelligence** challenge. It helps a relationship manager move from
"what does my client's portfolio look like?" to "what should I know, and what
should I do next?" — while keeping the RM in control of every decision.

It runs on a synthetic dataset: 20 clients, 24 portfolios, 1,015 positions
across five dated snapshots ending 2026-08-26. No real client data is used.

## What it does

Aurum turns deterministic portfolio facts and controlled event data into
review leads the RM can act on:

- **Home** — a priority-ordered view of the book, plus a calendar of dated
  obligations (cash needs, KYC reviews, RM tasks) and mapped portfolio events.
- **Alignment & conflicts** — whether each portfolio still fits the client's
  intent (risk profile, mandate, objectives, events), with an evidence trail
  that resolves every claim to a CSV line or note section.
- **Command Center** — an ordered what/when/why/how action sequence per client,
  plus a manual allocation scenario preview.
- **Focus casebook** — three deeply prepared client cases with relationship
  context, call guidance, choice framing and auditable RM decisions.
- **Client deep dive** — allocation, snapshot history with price/FX/flow
  attribution, event mapping, alignment and a 60-second call brief.
- **Notes library** — searchable source RM notes.
- **Action record** — a local, auditable log of tasks, decisions and
  post-conversation reflections.

Optional AI drafting (OpenAI) rewrites a censored, pre-selected fact packet
into a call brief or recommendation draft. It cannot access files, calculate
numbers, or approve anything — Priscilla remains accountable.

## Quick start

Requires Python 3.11+ and [uv](https://docs.astral.sh/uv/).

```bash
uv sync                # install dependencies
uv run streamlit run app.py
```

Copy `.env.example` to `.env` and add your keys to enable the optional
features: `OPENAI_API_KEY` (alignment reports and AI drafts) and
`MARKETAUX_API_KEY` (live news). The app still runs without them; those
features simply stay disabled.

## How it works

```
data/*.csv + rm_notes.json   source of truth
        |
        v
src/singhacks26/             deterministic analytics + guardrailed AI
        |
        v
app.py                       Streamlit workbench
```

- `event_log.csv` is the authoritative source for anything that happened in
  2026; the model never free-associates about geopolitics.
- Live Marketaux news is a separate, dated feed. It is cached locally and only
  queried for held sectors using censored queries.
- Client data stays local. Only censored, pre-selected facts leave the machine.

## Repository layout

| Path                    | Purpose                                                |
| ----------------------- | ------------------------------------------------------ |
| `app.py`                | Streamlit entry point                                  |
| `src/singhacks26/`      | Package: analytics, AI guardrails, evidence resolution |
| `data/`                 | Synthetic dataset (CSV files + RM notes)               |
| `obsidian_vault/`       | Censored per-client context notes + local caches       |
| `scripts/`              | Data-prep and market-api utilities                     |
| `starter/quickstart.py` | Challenge-provided data orientation script             |
| `tests/`                | pytest suite                                           |
| `docs/`                 | Challenge spec, architecture, data dictionary          |

## Development

This project uses **uv** for environment and dependency management. Do not use
`pip`, `poetry`, `pipenv`, or `conda`.

```bash
uv run pytest                # run tests
uv run ruff check .          # lint
uv run ruff format .         # format
uv run ruff format --check . # check formatting
```

To add or remove dependencies, use `uv add <pkg>`, `uv add --group dev <pkg>`,
or `uv remove <pkg>`, and commit both `pyproject.toml` and `uv.lock`.

Collaboration conventions (branching and direct merges) are defined in
[`AGENTS.md`](AGENTS.md).