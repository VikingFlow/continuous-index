# CIX — Continuous Index (VikingFlowAI)
A minimal, deterministic, human-readable indexing system for stable long-form LLM workflows.  
CIX provides consistent timestamp anchors that make conversations, pods, memory systems and context retrieval predictable — even across multi-day or multi-week sessions.

---

## 🚀 Try CIX in 10 seconds
Copy & paste the code below into a file named `cix.py` and run:

```bash
python cix.py
```

---

## 🧩 Minimal Reference Implementation (PoC)

```python
from datetime import datetime
from uuid import uuid4

def generate_cix(category: str = "A", note: str = "") -> str:
    """
    Generate a simple Continuous Index (CIX) tag.
    Example:
    2025-W06-D03-T14:32:12 | #A-71f2 | User describes new architecture idea
    """
    now = datetime.utcnow()
    year = now.year
    week = now.isocalendar().week   # ISO week number
    day = now.day                   # calendar day (01–31)
    time_part = now.strftime("T%H:%M:%S")
    short_id = str(uuid4())[:4]     # short random suffix to avoid collisions

    base = f"{year}-W{week:02d}-D{day:02d}-{time_part} | #{category}-{short_id}"
    return f"{base} | {note}" if note else base


if __name__ == "__main__":
    print(generate_cix("A", "User describes new architecture idea"))
```

This reference code is intentionally minimal — it shows the structure clearly without dictating implementation details.  
Developers are encouraged to extend, fork, or integrate it into larger systems (Pods, ReScroll, context managers, etc.).

---

## ✨ Why CIX Exists
LLMs lose stability when conversations grow beyond the token window, forcing systems to:

- regenerate old content  
- lose long-term structure  
- hallucinate references  
- break continuity  

CIX introduces a deterministic index that enables:

- predictable context linking  
- sortable chronological events  
- stable referencing across pods  
- zero-guess navigation  

Think of it as anchor points for long-lived AI interactions.

---

## 📘 CIX Format (Human-Readable)

Example:

```
2025-W05-D03-T14:32:12 | #A1 | User introduces new architecture idea
2025-W05-D03-T14:33:45 | #A2 | Model summarizes modules
2025-W05-D03-T14:40:12 | #B1 | User explains Pods concept
```

Each entry is:

- deterministic  
- lexically sortable  
- timestamped by week & day  
- easy for both humans and machines to navigate  

---

## 🔧 How Developers Use CIX

1. Generate a CIX tag whenever an event occurs  
2. Store it alongside content (JSON, SQLite, flat file)  
3. Sort lexically → deterministic history  
4. Use tags as keys for navigation, retrieval or cross-pod referencing  

CIX is compatible with:

- Continuous Mode  
- Pods  
- ReScroll  
- Jump Navigation  
- Multi-LLM comparison workflows  
- Local indexing and memory systems  

---

## 📅 Roadmap

| Version | Feature |
|--------|---------|
| v0.2 | JSON store + CLI tool |
| v0.3 | Web viewer (Gradio or simple static UI) |
| v0.4 | Integration with ReScroll |
| v0.5 | Integration with Pods |
| v1.0 | Full VikingFlowAI context stack |

---

## 📄 License
Released under **Apache License 2.0** to ensure full open-source freedom with strong user protections.

---

## ✍️ Credits
**Concept & Architecture:** VikingFlowAI  
**Reference Code:** Generated with assistance from AI tools  
**Purpose:** Provide a clean, minimal starting point for deterministic LLM indexing systems.

