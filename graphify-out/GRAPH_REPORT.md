# Graph Report - graphify  (2026-09-09)

## Corpus Check
- Corpus is ~13,318 words - fits in a single context window. You may not need a graph.

## Summary
- 219 nodes · 571 edges · 26 communities (9 shown, 8 thin omitted)
- Extraction: 92% EXTRACTED · 8% INFERRED · 0% AMBIGUOUS · INFERRED: 44 edges (avg confidence: 0.94)
- Token cost: 0 input · 97,320 output

## Community Hubs (Navigation)
- Job Search Agent & Sources
- Resume Tailoring Agent
- API Routes & Config
- Data Models & Docx Rendering
- Project Overview & Stack
- Resume Upload & Parsing
- Session Storage
- Docx Editing
- Frontend API Client
- Project Metadata
- Dependency: duckduckgo-search
- Dependency: httpx
- Dependency: pydantic
- Dependency: pydantic-settings
- Dependency: pytest
- Dependency: python-multipart
- Dependency: uvicorn

## God Nodes (most connected - your core abstractions)
1. `Settings` - 41 edges
2. `ResumeProfile` - 37 edges
3. `SessionStore` - 27 edges
4. `JobListing` - 21 edges
5. `MatchResult` - 20 edges
6. `run_job_search()` - 19 edges
7. `JobSourceError` - 18 edges
8. `ContactInfo` - 16 edges
9. `tailor_resume()` - 13 edges
10. `score_resume_against_job()` - 11 edges

## Surprising Connections (you probably didn't know these)
- `In-place edit vs rebuild decision` --references--> `is_docx_well_formed()`  [EXTRACTED]
  docs/superpowers/specs/2026-09-02-job-search-agent-design.md → backend/parsing/resume_parser.py
- `Graceful job-source degradation` --references--> `JobSourceError`  [EXTRACTED]
  docs/superpowers/specs/2026-09-02-job-search-agent-design.md → backend/tools/jsearch_tool.py
- `Direct Python orchestration instead of AgentExecutor (testability)` --rationale_for--> `run_job_search()`  [EXTRACTED]
  docs/superpowers/plans/2026-09-02-job-search-agent.md → backend/agents/job_search_agent.py
- `Job Search Agent Implementation Plan` --references--> `Settings`  [EXTRACTED]
  docs/superpowers/plans/2026-09-02-job-search-agent.md → backend/config.py
- `Non-goals: no auth / multi-tenant persistence` --rationale_for--> `SessionStore`  [EXTRACTED]
  docs/superpowers/specs/2026-09-02-job-search-agent-design.md → backend/storage/session_store.py

## Import Cycles
- None detected.

## Hyperedges (group relationships)
- **Unified job-source error handling across tools** — backend_tools_jsearch_tool_jobsourceerror, backend_tools_ddg_tool_search_jobs_ddg, backend_tools_firecrawl_tool_scrape_job_page, backend_agents_job_search_agent_run_job_search [EXTRACTED 1.00]
- **Shared resume/job domain model set** — backend_models_resumeprofile, backend_models_joblisting, backend_models_matchresult, backend_models_rankedjob, backend_models_jobsearchresult [EXTRACTED 1.00]
- **Match scorer shared across both ReAct agents** — docs_superpowers_specs_2026_09_02_job_search_agent_design_jobsearchagent, docs_superpowers_specs_2026_09_02_job_search_agent_design_resumetailoragent, backend_tools_match_scorer_score_resume_against_job [EXTRACTED 1.00]

## Communities (26 total, 8 thin omitted)

### Community 0 - "Job Search Agent & Sources"
Cohesion: 0.16
Nodes (25): _profile_to_text(), run_job_search(), JobListing, search_jobs_ddg(), Client, scrape_job_page(), JobSourceError, Client (+17 more)

### Community 1 - "Resume Tailoring Agent"
Cohesion: 0.12
Nodes (26): _default_revise(), _profile_to_text(), _render_final(), tailor_resume(), MatchResult, score_resume_against_job(), Global Constraints (graceful degradation, round cap, mockable calls), Job Search Agent Implementation Plan (+18 more)

### Community 2 - "API Routes & Config"
Cohesion: 0.16
Nodes (21): TailorResult, get_settings(), Settings, health(), extract_profile(), BaseModel, post, search_jobs() (+13 more)

### Community 3 - "Data Models & Docx Rendering"
Cohesion: 0.19
Nodes (15): ContactInfo, EducationEntry, ExperienceEntry, JobSearchResult, BaseModel, RankedJob, ResumeProfile, render_profile_to_docx() (+7 more)

### Community 4 - "Project Overview & Stack"
Cohesion: 0.10
Nodes (22): Data flow (upload -> search -> tailor -> download), DuckDuckGo, FastAPI, Gemini 2.0 Flash, POST /jobs/search, POST /jobs/tailor, JSearch (RapidAPI), LangChain (+14 more)

### Community 5 - "Resume Upload & Parsing"
Cohesion: 0.24
Nodes (14): _extract_docx_text(), _extract_pdf_text(), extract_resume_text(), is_docx_well_formed(), post, upload_resume(), _make_docx_bytes(), test_extract_resume_text_from_docx() (+6 more)

### Community 6 - "Session Storage"
Cohesion: 0.20
Nodes (5): SessionStore, Non-goals: no auth / multi-tenant persistence, fixture, test_upload_resume_rejects_unsupported_file_type(), store()

### Community 7 - "Docx Editing"
Cohesion: 0.47
Nodes (8): append_bullets_after(), apply_paragraph_replacements(), _set_paragraph_text_preserving_style(), _make_docx_bytes(), _paragraph_texts(), test_append_bullets_after_inserts_new_bullets(), test_apply_paragraph_replacements_ignores_non_matching_keys(), test_apply_paragraph_replacements_replaces_matching_text()

### Community 8 - "Frontend API Client"
Cohesion: 0.44
Nodes (7): Client, search_jobs(), tailor_resume(), upload_resume(), test_search_jobs_posts_json_body(), test_tailor_resume_posts_json_body(), test_upload_resume_posts_multipart_file()

## Knowledge Gaps
- **21 isolated node(s):** `job-search-agent`, `POST /jobs/tailor`, `JSearch (RapidAPI)`, `DuckDuckGo`, `Flat-file session storage` (+16 more)
  These have ≤1 connection - possible missing edges or undocumented components. (Counts symbols only; 51 node(s) total have ≤1 connection when file, concept and rationale nodes are included.)
- **8 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Settings` connect `API Routes & Config` to `Job Search Agent & Sources`, `Resume Tailoring Agent`, `Data Models & Docx Rendering`, `Resume Upload & Parsing`, `Session Storage`?**
  _High betweenness centrality (0.154) - this node is a cross-community bridge._
- **Why does `ResumeProfile` connect `Data Models & Docx Rendering` to `Job Search Agent & Sources`, `Resume Tailoring Agent`, `API Routes & Config`, `Session Storage`?**
  _High betweenness centrality (0.107) - this node is a cross-community bridge._
- **Why does `SessionStore` connect `Session Storage` to `API Routes & Config`, `Data Models & Docx Rendering`, `Resume Upload & Parsing`?**
  _High betweenness centrality (0.091) - this node is a cross-community bridge._
- **Are the 11 inferred relationships involving `Settings` (e.g. with `run_job_search()` and `_default_revise()`) actually correct?**
  _`Settings` has 11 INFERRED edges - model-reasoned connections that need verification._
- **Are the 10 inferred relationships involving `ResumeProfile` (e.g. with `_profile_to_text()` and `run_job_search()`) actually correct?**
  _`ResumeProfile` has 10 INFERRED edges - model-reasoned connections that need verification._
- **Are the 5 inferred relationships involving `SessionStore` (e.g. with `search_jobs()` and `tailor()`) actually correct?**
  _`SessionStore` has 5 INFERRED edges - model-reasoned connections that need verification._
- **Are the 3 inferred relationships involving `JobListing` (e.g. with `run_job_search()` and `tailor_resume()`) actually correct?**
  _`JobListing` has 3 INFERRED edges - model-reasoned connections that need verification._