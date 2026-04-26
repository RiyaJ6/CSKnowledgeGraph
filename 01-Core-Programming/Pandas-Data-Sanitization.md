# Pandas: Deterministic Data Sanitization

**Tags:** #python #pandas #data-engineering #preprocessing
**Linked Nodes:** [[ReAct-Loop-Architecture]], [[Zero-Fail-Debugging]]

## The Golden Rule of AI Systems
**Garbage In = Hallucinations Out.** You cannot feed a raw, messy CSV file to a Large Language Model and expect a deterministic result. The data must be sanitized, normalized and strictly typed before it ever reaches the context window.

## The Sanitization Protocol

### 1. Handling Null Architectures
Never allow an LLM to guess what a missing value means. Explicitly handle `NaN` values at the ingestion layer.
```python
import pandas as pd
df = pd.read_csv('university_constraints.csv')
df.dropna(subset=['course_id'], inplace=True) # Drop critical missing data
df['prerequisites'].fillna('None', inplace=True) # Impute non-critical data
```

### 2. Type Enforcement
LLMs process strings but your Python backend needs strict data types to execute logic.
```python
# Force strict integer types to prevent runtime comparison errors
df['credit_hours'] = pd.to_numeric(df['credit_hours'], errors='coerce').fillna(0).astype(int)
```
