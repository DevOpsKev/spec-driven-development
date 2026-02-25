# Spec Driven Development

**A practitioner methodology for AI-native software engineering where specifications — not code — are the primary artifact.**

Most AI coding workflows are variations on the same theme: prompt, hope, patch, repeat. When it works, it feels like magic. When it doesn't, you're debugging code you didn't write, can't verify against requirements that were never written down, and burning hours on error recovery instead of building.

Spec-Driven Development (SDD) inverts this. You spend your cognitive budget on specifications — structured documents that capture intent, define scope, and include mandatory verification checks. The agent spends compute on execution. The specification is the artifact. Code is a side effect.

This skill teaches AI coding agents the full SDD methodology: a two-loop workflow with eight steps, an explicit decision gate between planning and execution, four types of structured context, provenance tracking, and a library of practitioner-discovered principles and anti-patterns. It was developed through months of real production use — building an [entire book about the methodology](https://sddbook.com) using the methodology itself.

This isn't theory. Every principle in this skill was learned by hitting the problem it prevents.

**Author:** [Kevin Ryan](https://kevinryan.io) — DevOps and Platform Engineering specialist with 30 years of experience delivering for enterprise clients. Currently writing *Specification Driven Development: AI Native Software Engineering*.

**Links:**
- 📖 [sddbook.com](https://sddbook.com) — The book on SDD
- 🌐 [kevinryan.io](https://kevinryan.io) — Author's website
- 📦 [Tessl Registry](https://tessl.io/registry) — Browse and install the skill

---

## What's in This Skill

```
spec-driven-development/
├── SKILL.md                          # Core methodology (234 lines)
├── tile.json                         # Tessl package manifest
├── LICENSE                           # CC-BY-4.0
└── references/
    ├── principles.md                 # 18 practitioner-discovered principles
    └── anti-patterns.md              # 6 spec failure modes with fixes
```

| File | What it teaches the agent |
|------|--------------------------|
| **SKILL.md** | The two-loop workflow, step 6 decision gate, spec format, four context types, provenance, and when NOT to use SDD |
| **references/principles.md** | Deep explanations of every principle — "the spec is cheap, execution is expensive", "the bug is always in the spec", "mandatory means mandatory", and 15 more |
| **references/anti-patterns.md** | How to diagnose and fix broken specs — the novel spec, the implicit spec, the mega-spec, the unverifiable spec, the deferred debt spec, the prompt-dependent spec |

The skill uses progressive disclosure as recommended by the [Agent Skills Specification](https://agentskills.io/specification). The `name` and `description` frontmatter is loaded at startup for skill discovery (~100 tokens). The full SKILL.md body is loaded when activated (<500 lines). Reference files are loaded only when the agent needs deeper context.

---

## Installing the Skill

### Prerequisites

- [Node.js](https://nodejs.org/) (for the Tessl CLI)
- A Tessl account ([sign up free](https://tessl.io/signup))
- An MCP-compatible coding agent (Claude Code, Cursor, Windsurf, etc.)

### Step 1: Install Tessl CLI

```bash
npm install -g @tessl/cli
```

### Step 2: Authenticate

```bash
tessl login
```

### Step 3: Initialise Tessl in your project

From your project's root directory:

```bash
tessl init
```

This creates a `.tessl/` directory and configures your agent. You will be prompted to select your agent platform (Claude Code, Cursor, etc.). Accept the defaults unless you have specific requirements.

### Step 4: Install the skill

```bash
tessl install WORKSPACE/spec-driven-development
```

Replace `WORKSPACE` with the published workspace name. Alternatively, install a specific version:

```bash
tessl install WORKSPACE/spec-driven-development@1.0.0
```

### Step 5: Verify installation

The skill is now available to your agent. You can verify by checking:

```bash
ls .tessl/tiles/
```

You should see the skill's directory with `SKILL.md` and the `references/` folder.

### Updating

When new versions are published, update with:

```bash
tessl install WORKSPACE/spec-driven-development
```

This fetches the latest version automatically.

---

## Using the Skill

Once installed, the skill activates automatically when your agent detects relevant context — starting a new feature, structuring a development workflow, or when you explicitly reference spec-driven development.

### Quick Start: Your First Spec

Include "use spec-driven development" in your prompt:

```
I need to add user authentication to this project. Use spec-driven development.
```

The agent will follow the SDD workflow:

1. Ask clarifying questions to build a brief
2. Expand the brief into a full specification
3. Present the spec for your review and iteration
4. Execute in plan mode first
5. Present the plan for validation (the step 6 decision gate)
6. Execute only after approval
7. Validate results against the spec's mandatory checks

### The Decision Gate in Practice

The most important moment in any SDD execution is step 6 — reviewing the plan. When the agent presents a plan, ask yourself:

- Does the plan reveal anything missing from the spec?
- Are all verification checks from the spec present in the plan?
- Has the agent reduced scope or skipped requirements?

If the plan reveals a spec problem, tell the agent to update the spec and regenerate the plan. Do not patch the plan directly. The spec is the artifact.

### When to Use SDD

SDD works best for:

- Build pipelines and infrastructure
- Data contracts and API definitions
- Repeatable generation tasks (READMEs, documentation, configuration)
- Any task where you need to verify the output against explicit requirements
- Multi-step features where the agent needs structured guidance

### When NOT to Use SDD

Not everything benefits from specification. Skip SDD when:

- You are writing pure creative content (a blog post, a preface)
- The task is simple enough that a single prompt handles it
- You are the entire loop — intent, creation, and validation
- Adding a spec would be ceremony, not value

---

## Publishing the Skill to Tessl

If you want to publish your own version of this skill (or fork and customise it), follow these steps.

### Prerequisites

- [Node.js](https://nodejs.org/)
- Tessl CLI installed: `npm install -g @tessl/cli`
- A Tessl account: `tessl login`

### Step 1: Create a workspace

```bash
tessl workspace create
```

Follow the prompts to name your workspace. This becomes your publisher prefix (e.g. `myworkspace/spec-driven-development`).

### Step 2: Update tile.json

Edit `tile.json` and replace the workspace placeholder with your workspace name:

```json
{
  "name": "myworkspace/spec-driven-development",
  "version": "1.0.0",
  "summary": "A practitioner methodology for AI-native software engineering where specifications are the primary artifact and code is a generated side effect.",
  "private": false,
  "skills": {
    "spec-driven-development": {
      "path": "SKILL.md"
    }
  }
}
```

### Step 3: Validate structure

Lint checks the skill's structure and frontmatter against the Agent Skills specification:

```bash
tessl skill lint .
```

Fix any errors before proceeding.

### Step 4: Review against best practices

The review command scores your skill against Anthropic's best practices for agent consumption:

```bash
tessl skill review .
```

This checks description quality, content actionability, progressive disclosure, and conciseness. Address any warnings or suggestions — higher scores mean better discoverability in the Tessl Registry.

### Step 5: Create evaluation scenarios

Evaluation scenarios test whether the skill actually changes agent behaviour. Generate them automatically:

```bash
tessl skill eval generate .
```

This creates an `evals/` directory with scenario files. Review and edit these — you are the authority on what success looks like for your skill. Each scenario contains:

- `task.md` — a task the agent should perform
- `criteria.json` — what success looks like
- `capability.txt` — which skill capability is being tested

### Step 6: Run evaluations

```bash
tessl skill eval run .
```

This runs agents with and without the skill on your scenarios and scores the results. You will receive a URL to monitor progress and view results in the Tessl web UI.

### Step 7: Publish (private)

Publish as private first to test with your own team:

```bash
tessl skill publish .
```

By default, skills are published as private — only members of your workspace can install them.

### Step 8: Test the published skill

Install your published skill in a test project:

```bash
tessl install myworkspace/spec-driven-development
```

Run a real task using SDD to confirm the skill activates correctly and the agent follows the methodology.

### Step 9: Make it public

Once you are satisfied with the skill's quality:

1. Go to the [Tessl Registry](https://tessl.io/registry) in your browser
2. Navigate to your workspace and find your skill
3. Click on the skill to view its details
4. Select **Actions** → **Make Public**
5. Click **Request to Make Public**

Tessl will review and contact you about the status. Once approved, republish:

```bash
tessl skill publish . --public
```

### Publishing updates

When you update the skill:

1. Edit `SKILL.md` or the reference files
2. Increment the version in `tile.json` following [semantic versioning](https://semver.org/):
   - **Patch** (1.0.0 → 1.0.1): typo fixes, clarifications
   - **Minor** (1.0.0 → 1.1.0): new principles, new sections, backward-compatible additions
   - **Major** (1.0.0 → 2.0.0): restructured workflow, breaking changes to methodology
3. Validate: `tessl skill lint .`
4. Publish: `tessl skill publish .`

Users update to the latest version with:

```bash
tessl install myworkspace/spec-driven-development
```

---

## The Book

This skill is a companion to *Specification Driven Development: AI Native Software Engineering* by Kevin Ryan.

The book covers the full methodology in depth — the history, the theory, the practice, case studies, and the emerging ecosystem of spec-driven tools. The skill is the machine-readable distillation; the book is the human-readable explanation.

The book itself was built using SDD. The repository that produces it demonstrates the methodology through visible infrastructure: specifications, provenance files, MCP servers, and a CI/CD pipeline that generates multiple formats from the same source. The commit hash on the repository matches the commit hash on the book's copyright page. Full provenance from source to artifact, verifiable by anyone.

📖 **[sddbook.com](https://sddbook.com)**

---

## Licence

This work is licensed under [Creative Commons Attribution 4.0 International (CC-BY-4.0)](http://creativecommons.org/licenses/by/4.0/).

You are free to share and adapt this material for any purpose, including commercially, as long as you give appropriate attribution.
