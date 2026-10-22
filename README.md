# security-a11y

A per-PR review skill for web services and front ends. It checks the changed
code of a pull request against the OWASP Top 10 (2021) and, when a changed file
is rendered UI (HTML, JSX/TSX, Vue, Svelte, templates, CSS), against
WCAG 2.1 AA. It reports only defects that the code demonstrates: each finding
carries a trigger or an impact, a `path:line` and a fix. It cites an A06
advisory only after an OSV lookup.

This repository holds the skill only. The domain checklists live here, and not
in the definition of a review agent, so that the team who owns the domain keeps
them current.

```
.agents/skills/security-a11y/
├── SKILL.md
└── references/accessibility.md   # WCAG 2.1 AA, read only for rendered UI
```

## Use it with code-guardian

The skill is a `## Review skills` row. The operator of the instance adds this
row to `work/CONFIG.md` in the direct session (that table is operator-only, so
no pull request can add it):

```
| skill | source | trigger | section |
| --- | --- | --- | --- |
| security-a11y | github.com/adigidh/security-a11y-skill | always | Security & Accessibility |
```

On a new instance, onboarding step 7 shows the table. Add the row there.

Before the row goes in, make sure that this command succeeds — onboarding runs
the same check for each row:

```sh
gh api --hostname github.com \
  "repos/adigidh/security-a11y-skill/contents/.agents/skills/security-a11y"
```

`trigger` is `always` because the skill applies the WCAG part by itself, only
when a changed file is rendered UI. The OWASP part still runs on other changes.
An extension list narrows it, but then a change with no matching file gets no
security check at all.

The agent installs the skill from the **default branch** of this repository, not
from a pull request branch. A change to the skill starts to apply after it
merges to `main`.

### Caveat — the host of the instance

An instance on a GitHub Enterprise host (for example `github.ibm.com`) needs the
`github.com/` prefix in `source`, as shown above, **and** a token that can read
this public repository on github.com. If the instance cannot reach github.com,
copy `.agents/skills/security-a11y/` into a repository on the instance's own
host and point `source` there instead.

## Use it with another agent

Any agent that reads skills from `.agents/skills/<name>/` can install this one.
The directory name must stay `security-a11y`: an installer mirrors that path
literally and matches it to the configured skill name.
