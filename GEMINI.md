# JobsPipe

JobsPipe answers questions about who is hiring, from live job postings collected across 30+ job boards, public employment services and company career sites and normalized into one schema.

- Use `search` to find postings by role, place and date, and `fetch` to read one in full by the id a search returned. Both cite the original posting.
- Use `search_jobs` when a question needs more than a role and a place: location, salary, seniority, skills, visa stance, language, work arrangement, source and more. All filters combine with AND.
- Use `search_documentation` to check what a filter accepts before guessing.
- To watch for new postings over time, save the search with `create_signal` instead of re-running it on a timer; signals fire on first match only and cost no job credits. Check `list_signals` first so a watch is not saved twice.
- `get_account_info` shows the connected account, its plan and remaining credits; searches draw on that plan.

On first use Gemini CLI opens the JobsPipe sign-in page; a free account is enough to start.
