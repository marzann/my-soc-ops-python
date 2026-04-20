# Soc Ops — Agent Instructions

**Soc Ops** is a Social Bingo game (FastAPI + Jinja2 + HTMX). Workshop project — see [`workshop/`](workshop/).

## ⚠️ Mandatory Development Checklist

Run these before every commit. All must pass.

```bash
uv run ruff check .    # Lint — zero errors required
uv run ruff format .   # Format
uv run pytest          # All tests must pass
```

## Commands

```bash
uv run uvicorn app.main:app --reload   # Dev server → http://127.0.0.1:8000
```

## Architecture

```
app/
├── main.py          # FastAPI routes — all return HTMLResponse via Jinja2
├── models.py        # Pydantic models: GameState (StrEnum), BingoSquareData (frozen)
├── game_logic.py    # Pure functions: generate_board(), toggle_square(), check_bingo()
├── game_service.py  # GameSession dataclass — in-memory, no DB
├── data.py          # QUESTIONS list + FREE_SPACE constant
├── templates/       # Jinja2; components/ are HTMX swap targets
└── static/          # Custom CSS utilities + JS
tests/               # class-based pytest; test_api.py (TestClient) + test_game_logic.py
```

## Conventions

- **Immutability**: `BingoSquareData` is frozen; game logic returns new lists, never mutates
- **HTMX**: New interactive features return rendered HTML partials, not JSON
- **Types**: Type hints everywhere; `snake_case`; line-length 88; Python 3.13
- **CSS**: See [frontend-design.instructions.md](.github/instructions/frontend-design.instructions.md) and [css-utilities.instructions.md](.github/instructions/css-utilities.instructions.md)

## Customizations

TDD agents: [`.github/agents/`](.github/agents/) · Quiz generator: [`quiz-master.agent.md`](.github/agents/quiz-master.agent.md) · General rules: [`general.instructions.md`](.github/instructions/general.instructions.md)
