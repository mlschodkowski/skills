# Autonoma kit (v2)

Same jobs as the root catalog. Different bar.

`taste/autonoma-principles.md` is the shared design philosophy and
technical standard: form should follow from purpose, context,
constraints, and use. The taste skills apply it. Other procedures should
not name it; they should just do their job.

Central question: does the form of the thing follow from the thing
itself?

Use only the path the work needs. Do not run the folders as a pipeline.

## Layout

```text
taste/     how work should feel
build/     decide, slice, implement, debug
check/     review the change
ops/       commit, handoff, docs, tooling
```

### taste/

- `autonoma-code` — durable code that fits its surroundings; add structure only when use requires it
- `autonoma` — prose and documents whose form follows what the reader must understand
- `autonoma-ui` — interfaces that disappear behind the task
- `ponytail` — intensity mode for the laziest solution that still works

### build/

- `grill-me` — pressure-test a design with focused question rounds
- `hyperplan` — hostile architecture and delivery review
- `oracle` — final `GO`, `GO_WITH_CAVEATS`, or `NO_GO`
- `slice-it-vertically` — thinnest end-to-end increment with a visible result
- `brainstorming` — shape an unclear idea before a plan
- `architecture-design` — domain, boundaries, and module shape
- `tdd` — public behavior contracts and red-green-refactor
- `diagnose` — repro loop for hard bugs

### check/

- `code-review` — review a diff as a behavior change
- `over-engineering-review` — diff-only complexity cut list
- `over-engineering-audit` — repo-wide complexity cut list
- `ponytail-review` / `ponytail-audit` — ponytail-flavored over-engineering review and audit
- `shortcut-debt` — harvest deliberate-limit markers into a ledger

### ops/

- `git-commit` — scoped commits
- `git-pr` / `github` — pull requests and stacked PR workflows
- `handoff` — compact context for another agent or session
- `adr` — architecture decision record
- `research` — cited primary-source findings
- `writing-for-agents` — documents an agent must apply reliably
- `evidence-barrier` — shared evidence before cross-boundary writes
- `to-questionnaire` — collect facts or decisions from a specific person

## Use

Name a procedure to run it. Some fire from a matching request; others
wait until you ask (`grill-me`, `tdd`, `hyperplan`, `oracle`,
`code-review`, `over-engineering-review`, `over-engineering-audit`,
`shortcut-debt`, `to-questionnaire`, `ponytail`).

## Lineage

Autonoma is not a visual style. It gathers traditions that treat design
as a consequence of use rather than an opportunity for display:

- **Super Normal** (Jasper Morrison & Naoto Fukasawa) — ordinary objects
  whose design disappears into use
- **Dieter Rams** — useful, understandable, honest, long-lasting, and
  as little design as possible
- **Don Norman** — discoverability, feedback, conceptual models, and
  making intended use apparent
- **Swiss typography / Tschichold** — hierarchy and form determined by
  information and the medium
- **Orwell / Strunk & White** — concrete exact words; prefer the
  standard to the offbeat
- **Shaker design** — utility, honest construction, restraint
- **Wabi-sabi / shibui** — material character, restraint, qualities that
  deepen with prolonged use
- **Christopher Alexander** — wholeness, context, patterns that belong
  in their surroundings
- **Unix philosophy** — small focused parts, simple interfaces,
  composition, economy
- **Hyrum's Law** — every observable behavior eventually becomes a
  dependency
- **Adaptability** (Rams/Vitsœ-style) — make change cheap instead of
  predicting every future configuration
- **Material honesty & constraint-driven design** — do not disguise how
  something works; let constraints remove ornamental choices

## Maintenance

Keep each procedure short and independently useful. One home per fact.
Preserve exact identifiers and commands. Check a change against a real
task before treating it as done.
