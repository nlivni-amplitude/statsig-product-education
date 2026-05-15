---
topic: org-and-project-settings
source_modules:
  - Statsig 3 / Module 4 — Org and Project Settings
amplitude_counterpart: "Amplitude Org / Workspace / Project (Target Apps has no direct Amplitude equivalent)"
audit_note: "Target Apps setup is shallow in the corpus."
---

# Org and Project Settings

How Statsig structures workspaces (Organization → Project → Team), member access, and Target Apps. Product capabilities only — covers what a customer needs to know to configure their workspace.

## Learning Objectives

### LO1. Understand Statsig's three-tier structure.

**Prompt:** *Describe Statsig's three constructs (Organization, Project, Team) and what each one isolates or shares.*

**Canonical answer:**
- **Organization** — the company. One per customer.
- **Project** — isolated workspace. Data, gates, experiments, dashboards do NOT cross project boundaries. Different projects = different metric universes.
- **Team** — a group within a project. Teams share project resources but can be assigned ownership of specific gates/experiments.

Default recommendation for most customers: **one organization, one project, multiple teams.** Data stays shared, cross-team collaboration is easy, single source of metric truth. Multiple projects only when there's a hard reason to isolate (regulatory, totally unrelated products).

---

### LO2. Use Target Apps to scope evaluations.

**Prompt:** *A customer has a web app, iOS app, and Android app in the same Statsig project. They want a feature only on iOS. How do Target Apps help, and what would go wrong without them?*

**Canonical answer:** **Target Apps** are scoped contexts within a project. You declare that a gate, experiment, or config only applies to a specific Target App (e.g., `ios-mobile`). When an SDK evaluates from a different app, it never sees that gate.

**Without Target Apps:** the gate evaluates everywhere. A "1% of all users" rollout includes web users who shouldn't see the iOS-only feature. Targeting by `platform == ios` works but is fragile.

Target Apps make scoping declarative — this gate exists for iOS, full stop. The SDK on web doesn't even see it. (Validated corpus is shallow on Target Apps — check current Statsig docs for setup specifics.)

---

### LO3. Understand member access and roles.

**Prompt:** *A customer is rolling Statsig out to many users. What kinds of roles can they assign, and what's the right default?*

**Canonical answer:** Statsig supports role-based access at the project level:
- **Admin** — configure org settings, billing, member management
- **Editor / Developer** — create/modify gates, experiments, configs
- **Viewer / Analyst** — read-only access to dashboards and results

Team-level scoping further restricts ownership so engineers don't accidentally modify another team's experiments.

**Right default:** least-privilege. Start most users as Viewers, escalate as needed. Easier to upgrade access than to revoke it after someone broke a config. SSO integration with the customer's identity provider (Okta, Azure AD, Google Workspace) is standard for any non-trivial deployment.

---

### LO4. Contrast Statsig's structure with Amplitude's.

**Prompt:** *How does Statsig's Org/Project/Team structure compare to Amplitude's Org/Workspace/Project? Where does the mapping work, where doesn't it?*

**Canonical answer:**

| Statsig | Amplitude | Notes |
|---|---|---|
| Organization | Org | 1:1 |
| Project | Workspace | Roughly 1:1 — both are isolated workspaces |
| Team | Project (in Amplitude) | Confusing name overlap. Amplitude's "Project" sits at the team-equivalent tier. |
| Target App | (no direct equivalent) | Amplitude uses a single Project surface — scoping happens by user property or environment tag, not as a first-class object. |

**Practical implication:** the Org → Project (Statsig) ↔ Workspace (Amplitude) mapping is clean. The "Team" / "Project" overlap is confusing — don't assume Amplitude "Project" = Statsig "Project." Target Apps don't migrate cleanly; in Amplitude you'd use user-property or environment-based filters to achieve similar scoping.
