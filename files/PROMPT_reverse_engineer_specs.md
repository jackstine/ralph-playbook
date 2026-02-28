0a. Study `specs/*` with up to 250 parallel Sonnet subagents to learn existing specifications.
0b. Study `src/*` to understand the codebase. Use up to 500 parallel Sonnet subagents for reads/searches. Treat `src/lib` as the project's standard library for shared utilities and components.
0c. Study @IMPLEMENTATION_PLAN.md (if present) for context on completed and pending work.

1. For each topic assigned (or discovered), reverse-engineer the source code and produce an XML specification in `specs/`. Use Opus subagents for complex tracing. Ultrathink. Before writing a spec, search to confirm one doesn't already exist for that topic.
2. One topic per spec. Must pass the "one sentence without 'and'" test. Split if "and" joins unrelated capabilities.
3. **Two-phase process:** Phase 1 (Investigation) — trace every entry point, branch, code path to terminal. Map data flow, side effects, state mutations, error handling, concurrency, config-driven paths, implicit behavior. Phase 2 (Output) — zero implementation details. No function/class/variable names, file paths, library/framework references. A different team on a different stack must be able to reimplement from the spec alone.
4. **Document reality, not intent.** Bugs are features. Never add behaviors the code doesn't implement. Never suggest improvements. If a source comment contradicts the code, document the code's behavior and ignore the comment.
5. **Scope boundaries:** When tracing leaves the topic, stop. Document what crosses the boundary (sent/received) only. Test: "Could this change without changing my topic's outcomes?" If yes, it's across the boundary.
6. **Shared behavior:** Inline fully in every spec (self-contained). Tag with `<shared topic="...">` for cross-spec tracking. Shared behavior also gets its own canonical spec.
7. **XML format:** Root `<specification topic="...">` containing `<topic-statement>`, `<scope>` (with `<in-scope>` and `<boundary name="...">`), `<data-contracts>` (with `<contract>`/`<field>`), `<behavior>` (named kebab-case children with `order="N"`, nestable), `<state-transitions>`. Inline tags: `<notable reason="...">`, `<unreachable reason="...">`, `<shared topic="...">`, `<rationale source="comment">`. File naming: `specs/[max-3-words-kebab-case].xml`.
8. After completing a spec, update @IMPLEMENTATION_PLAN.md with findings using a subagent. When resolved, remove the item.
9. When specs are complete and validated, `git add -A` then `git commit` with a message describing which specs were added/updated. After the commit, `git push`.

99999. **Exhaustive checklist before finalizing:** Every entry point documented. Every branch traced to terminal. Every data contract. Every side effect in execution order. Every error path (caught/propagated/ignored). Every config-driven path. Concurrency outcomes. Unreachable paths tagged `<unreachable>`. Notable/surprising behavior tagged `<notable>`. Zero implementation details in output. If any item is missing, trace again.
999999. The code is the source of truth. If specs are inconsistent with the code, update the spec using an Opus subagent.
9999999. Keep @IMPLEMENTATION_PLAN.md current with learnings using a subagent — future work depends on this.
99999999. Single sources of truth, no duplicated specs. Update existing specs rather than creating new ones.
999999999. When you learn something new about the project, update @AGENTS.md using a subagent but keep it brief and operational only — no status updates or progress notes.
9999999999. Source comments explaining why behavior must be preserved (regulatory, compatibility, intentional) — capture rationale with `<rationale source="comment">`, strip implementation references. Stale comments are not spec.
99999999999. Document all configuration-driven paths, not just the currently active one.
999999999999. If you find inconsistencies in `specs/*` then use an Opus subagent with 'ultrathink' to update the specs.
