# Common Review Patterns

Each pattern shows: problem description → before code → after code → principle.

---

## KISS violation — deep nesting / mixed concerns

**Problem**: Nested conditionals, mixed validation and transformation, hard to follow.

```python
# ❌ Before
def process_order(order):
    if order is not None:
        if order.get("items"):
            total = 0
            for item in order["items"]:
                if item.get("price") and item.get("qty"):
                    if item["qty"] > 0:
                        total += item["price"] * item["qty"]
            if total > 0:
                return {"status": "ok", "total": total}
    return {"status": "error"}
```

```python
# ✅ After — early returns, separated concerns
def calculate_total(items: list[dict]) -> float:
    return sum(
        item["price"] * item["qty"]
        for item in items
        if item.get("price") and item.get("qty", 0) > 0
    )

def process_order(order: dict | None) -> dict:
    if not order or not order.get("items"):
        return {"status": "error"}
    total = calculate_total(order["items"])
    if total <= 0:
        return {"status": "error"}
    return {"status": "ok", "total": total}
```

**Principle**: KISS — simpler control flow, single responsibility per function.

---

## YAGNI violation — speculative abstraction

**Problem**: Abstract base class + strategy pattern for a single concrete implementation.

```python
# ❌ Before — only one exporter ever exists
from abc import ABC, abstractmethod

class BaseExporter(ABC):
    @abstractmethod
    def export(self, data: list[dict]) -> bytes: ...

class ExporterFactory:
    @staticmethod
    def get(fmt: str) -> BaseExporter:
        if fmt == "csv":
            return CsvExporter()
        raise ValueError(fmt)

class CsvExporter(BaseExporter):
    def export(self, data: list[dict]) -> bytes:
        ...
```

```python
# ✅ After — inline until a second format is actually needed
import csv, io

def export_csv(data: list[dict]) -> bytes:
    buf = io.StringIO()
    writer = csv.DictWriter(buf, fieldnames=data[0].keys())
    writer.writeheader()
    writer.writerows(data)
    return buf.getvalue().encode()
```

**Principle**: YAGNI — reintroduce abstraction when the second implementation appears.

---

## DRY violation — duplicated validation

**Problem**: Same validation rule repeated in three layers.

```python
# ❌ Before
# serializer.py
def validate_email(data):
    if "@" not in data["email"]:
        raise ValueError("invalid email")

# service.py
def create_user(email, name):
    if "@" not in email:
        raise ValueError("invalid email")

# cli.py
def cmd_register(args):
    if "@" not in args.email:
        raise ValueError("invalid email")
```

```python
# ✅ After — single authoritative function
# validators.py
def validate_email(email: str) -> None:
    if "@" not in email:
        raise ValueError(f"Invalid email: {email!r}")

# All three layers import and call validate_email(email)
```

**Principle**: DRY — rule of three reached; extract one authoritative validator.

---

## SRP violation — class doing too much

**Problem**: One class loads files, parses content, validates data, and writes to DB.

```python
# ❌ Before
class UserImporter:
    def run(self, path: str):
        with open(path) as f:          # I/O
            raw = f.read()
        rows = csv.DictReader(...)      # parsing
        for row in rows:
            if "@" not in row["email"]: # validation
                continue
            db.execute("INSERT ...")    # persistence
```

```python
# ✅ After — one responsibility per unit
def read_csv(path: str) -> list[dict]: ...        # I/O
def parse_users(rows: list[dict]) -> list[User]: ... # parsing + validation
def save_users(users: list[User]) -> None: ...    # persistence

def import_users(path: str) -> None:
    rows = read_csv(path)
    users = parse_users(rows)
    save_users(users)
```

**Principle**: SRP — each function has one reason to change; easy to test in isolation.

---

## DIP violation — high-level logic coupled to concrete dependency

**Problem**: Business logic instantiates its own database client; untestable.

```python
# ❌ Before
class OrderService:
    def __init__(self):
        self.db = PostgresClient(host="localhost")  # concrete, hardcoded

    def get_order(self, order_id: str) -> dict:
        return self.db.query(f"SELECT * FROM orders WHERE id = '{order_id}'")
```

```python
# ✅ After — depend on a protocol, inject the collaborator
from typing import Protocol

class OrderRepo(Protocol):
    def get(self, order_id: str) -> dict: ...

class OrderService:
    def __init__(self, repo: OrderRepo) -> None:
        self.repo = repo

    def get_order(self, order_id: str) -> dict:
        return self.repo.get(order_id)

# In tests: pass a FakeOrderRepo(); in prod: pass PostgresOrderRepo()
```

**Principle**: DIP — high-level logic depends on an abstraction; concrete impl injected at the boundary.

---

## Tooling gap — no clear workflow

**Problem**: README has no install/lint/test commands; contributors guess.

**Fix**: Add to README or `Makefile`:
```
# Install
uv sync

# Lint
uv run ruff check .
uv run ruff format --check .

# Type check
uv run mypy .

# Test
uv run pytest
```

**Principle**: Engineering quality — one obvious command path for every common task.
