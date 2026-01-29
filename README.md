# AI-Powered Document Ingestion & Structured Extraction Service
A production-style backend service that ingests unstructured documents (PDF/text) and extracts **validated, schema-constrained structured data** using an LLM-backed pipeline. Outputs are persisted in PostgreSQL (JSONB) with **schema versioning** to support evolving extraction formats.

## Status
Active development (2-week build).

## Why this exists
Document formats vary and rule-based parsing is brittle. This system uses an LLM for semantic extraction while enforcing reliability through:
- strict schema validation (Pydantic)
- chunking + aggregation
- retries + failure states
- schema versioning for backward compatibility

## Architecture (high level)
1. Upload document -> parse to text
2. Chunk text -> LLM extraction per chunk
3. Validate chunk outputs -> aggregate -> validate final output
4. Persist extraction (JSONB) tagged with schema version
5. Query APIs for documents, extractions, and schemas

## Tech Stack
- Python, FastAPI
- PostgreSQL (JSONB)
- Docker / Docker Compose
- Pydantic validation
- Pluggable LLM provider (local or hosted)

## API (planned)
- `POST /documents` (upload)
- `GET /documents/{id}`
- `GET /documents/{id}/extractions`
- `GET /schemas`

## Development
### Run locally
1. Copy env template:
   - `cp .env.example .env`
2. Start services:
   - `docker compose up --build`
3. API docs:
   - `http://localhost:8000/docs`

