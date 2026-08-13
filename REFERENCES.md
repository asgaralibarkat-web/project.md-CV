# REFERENCES.md: Repository Inspection

## 1. Reference Repository: OpenAI Codex CLI
* Link: https://github.com/openai/codex

* Problem: Executing localized AI task instructions through a lightweight command-line interface.
* Structure: Separates CLI arguments, prompt execution, and file system handlers into discrete modules.
* One Useful Pattern: Direct file input parsing combined with explicit output destination flags.
* What I Will Not Copy: Complex multi-environment sandboxing and shell execution safety layers.

---

## 2. Reference Repository: GitHub Spec Kit
* Link: https://github.com/github/spec-kit

* Problem: Structuring software project milestones into clear, testable, text-based specifications.
* Structure: Top-level specification templates linking directly to task breakdowns and acceptance checks.
* One Useful Pattern: Explicit pass/fail criteria definitions to confirm milestone completion before code changes.
* What I Will Not Copy: Large multi-phase project tracking pipelines and automated issue management bots.
