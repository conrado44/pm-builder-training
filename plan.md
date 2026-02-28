# PM-as-Builder: 12-Week Training Plan

A structured, weekend-based curriculum for product managers who want to go beyond prompting and actually operate in a codebase — fixing bugs, shipping POC features, and handing off to engineers with real context.

**Assumed background**: You've taken a few CS classes at some point (intro programming, maybe a databases course), but you haven't coded professionally. You're familiar with your company's systems at a high level but haven't worked in the codebase directly. You've used AI coding tools (Claude Code, Codex, Cursor, etc.) but mostly as a prompter — you don't always understand what the AI changed or why.

**Time commitment**: 4 hrs/week — 2 hrs Saturday, 2 hrs Sunday. 48 hours total over 12 weeks.

**Tools**: Claude Code (Opus 4.6) + OpenAI Codex (GPT-5.3). VS Code as IDE.

**Primary language**: Go (widely used in backend services). Secondary: Kotlin, JS/TS.

**End state**: You can (1) fix contained bugs in a repo with no external dependencies, (2) ship a simple feature as an alpha/POC, and (3) hand the feature to an engineer with clear context so they can build it properly at scale.

---

## Phase 1: Environment & Navigation (Weeks 1–3)
*Getting comfortable in the kitchen before you cook.*

---

### Week 1: Terminal & Git Fundamentals
**Start date**: ___________

#### Saturday (2 hrs): Terminal & Dev Environment Setup
- [ ] Install Homebrew, VS Code, Go, and verify your AI coding CLI works
- [ ] Terminal essentials — practice these until they're muscle memory:
  - `cd`, `ls`, `pwd`, `mkdir`, `rm`, `cp`, `mv`
  - `which`, `echo $PATH`, `export`
  - Tab completion, `ctrl+c`, `ctrl+r` (reverse search)
  - Piping: `|`, `>`, `>>` (just awareness, not mastery)
- [ ] Install the Go extension in VS Code
- [ ] Clone a small Go repo to practice with: `git clone https://github.com/golang/example`

**Exercise**: Navigate to 3 different directories using only the terminal. Create a folder, create a file in it, move it, delete it. Get comfortable.

#### Sunday (2 hrs): Git Fundamentals
- [ ] Core git concepts: working directory → staging area → commit → remote
- [ ] Practice the daily workflow:
  ```
  git clone <repo>
  git checkout -b my-branch
  # make a change
  git add <file>
  git commit -m "description of change"
  git push -u origin my-branch
  ```
- [ ] Understand `git status`, `git log --oneline`, `git diff`
- [ ] Create a personal GitHub repo (e.g., `pm-builder-exercises`) and push to it
- [ ] Use your AI coding tool to help: ask it "explain what `git rebase` does vs `git merge`" — but READ the answer, don't just nod

**Exercise**: Create a repo, make 3 commits on a branch, push it to GitHub. Look at it on github.com.

**✅ Week 1 Goal**: Can clone a repo, create a branch, make changes, commit, and push — from memory, not by copying commands.

---

### Week 2: Reading Code & Repo Navigation
**Start date**: ___________

#### Saturday (2 hrs): How Go Projects Are Structured
- [ ] Learn Go project layout:
  - `go.mod` — what is this? (like `package.json` for Go)
  - `main.go` / `cmd/` — entry points
  - `internal/` — private packages
  - `pkg/` — public packages (sometimes)
  - `*_test.go` — test files live next to source files
- [ ] Key Go syntax (just enough to read, not write):
  - Functions: `func doThing(input string) (string, error)`
  - Structs: like classes but simpler
  - Interfaces: contracts for behavior
  - Error handling: `if err != nil { return err }` (you'll see this everywhere)
  - Packages and imports
- [ ] Use your AI coding tool on the `golang/example` repo:
  - "Explain the structure of this repo"
  - "What does this function do?" (point it at a specific function)
  - "Where is the entry point?"

**Exercise**: Open 5 different `.go` files. For each one, write a 1-sentence summary of what it does (in plain English). Use your AI tool to verify.

#### Sunday (2 hrs): Navigating a Real Service
- [ ] Clone a real-world Go web service. Recommended: `https://github.com/go-chi/chi` (a popular HTTP router) or `https://github.com/gorilla/mux`
- [ ] Practice finding things:
  - VS Code: `Cmd+P` (find file), `Cmd+Shift+F` (search across files), `F12` (go to definition)
  - AI tool: "Where is the handler for the /users endpoint?", "What does this middleware do?"
  - Grep: `grep -r "func " --include="*.go"` (find all functions)
- [ ] Understand how to read a PR on GitHub — look at 3 merged PRs on the chi repo. What changed? Why?

**Exercise**: Given the chi/mux repo, find: (1) the main entry point, (2) where routes are defined, (3) a test file. Do it without your AI tool first, then verify with it.

**✅ Week 2 Goal**: Given an unfamiliar Go repo, can find the entry point, understand the directory structure, and locate where a specific feature lives — in under 10 minutes.

---

### Week 3: How Services Work (End-to-End)
**Start date**: ___________

#### Saturday (2 hrs): HTTP & API Fundamentals
- [ ] Core concepts:
  - HTTP methods: GET (read), POST (create), PUT (update), DELETE (delete)
  - Status codes: 200 (ok), 400 (bad request), 401 (unauthorized), 404 (not found), 500 (server error)
  - Request → Route → Handler → Response
  - JSON: how data is structured in requests/responses
  - Middleware: code that runs before/after every request (auth, logging, etc.)
- [ ] Build a tiny Go HTTP server with your AI tool:
  - Ask it: "Help me build a simple Go HTTP server with 3 endpoints: GET /health, GET /items, POST /items. Use chi router. Explain each part."
  - **CRITICAL**: Don't just let the AI write it. After it generates code, READ every line. Ask "why did you use `http.StatusOK` instead of just `200`?" Ask "what does `json.NewDecoder(r.Body)` do?"
- [ ] Run it locally: `go run main.go`, then test with `curl http://localhost:8080/health`

**Exercise**: After building the server, add a 4th endpoint (DELETE /items/{id}) yourself. Use your AI tool for help but try writing the first draft yourself, even if it's wrong.

#### Sunday (2 hrs): Databases & SQL Refresher
- [ ] SQL refresher:
  - `SELECT`, `INSERT`, `UPDATE`, `DELETE`
  - `JOIN`, `WHERE`, `GROUP BY`
  - Primary keys, foreign keys, indexes
- [ ] How Go services talk to databases:
  - Database drivers, connection strings
  - The pattern: Handler → Service/Logic layer → Repository/Data layer → SQL
  - ORM vs raw SQL (most Go services use `sqlx` or raw `database/sql`)
- [ ] Extend your Saturday server:
  - Add a SQLite database (simplest to set up)
  - Store items in the database instead of in memory
  - Your AI tool will help, but ask it to explain the repository pattern

**Exercise**: Write a SQL query that answers: "How many items were created in the last 7 days, grouped by type?" — first on paper, then verify.

**✅ Week 3 Goal**: Can trace a request from API endpoint → handler → database query → response. Can explain this flow to an engineer on a whiteboard.

---

## Phase 2: AI-Assisted Development (Weeks 4–7)
*Learning to drive both vehicles — and knowing when to use each.*

---

### Week 4: Claude Code Mastery
**Start date**: ___________

#### Saturday (2 hrs): Claude Code Power Features
- [ ] Deep dive into Claude Code's features:
  - **Plan mode**: `Shift+Tab` — use this before any non-trivial change
  - **CLAUDE.md**: Create a project-level file that gives Claude context about your repo
  - **Slash commands**: `/init`, `/compact`, and any custom ones
  - **Context management**: How to give Claude Code enough context without overwhelming it
  - **Multi-file edits**: How Claude handles changes across files
  - **Git integration**: Claude can stage, commit, create PRs
- [ ] Practice prompting patterns:
  - ❌ Bad: "Fix this bug"
  - ✅ Good: "In `handlers/payment.go`, the `ProcessPayment` function returns a 500 error when the amount is 0. It should return a 400 with the message 'amount must be positive'. The relevant test is in `handlers/payment_test.go`."
  - ❌ Bad: "Add a feature"
  - ✅ Good: "Add a new endpoint `GET /payments/{id}/receipt` that returns a JSON receipt. Follow the same pattern as the existing `GET /payments/{id}` endpoint in `handlers/payment.go`. The receipt should include: payment_id, amount, currency, timestamp, status."

**Exercise**: Write 5 prompts for hypothetical changes to your Saturday server from Week 3. Make each one specific enough that Claude Code could execute it without asking follow-up questions.

#### Sunday (2 hrs): Practice Session — Real Modifications
- [ ] Use Claude Code on an open-source Go project (pick one with "good first issues"):
  - Recommended: `https://github.com/cli/cli` (GitHub's own CLI, written in Go)
  - Or: `https://github.com/junegunn/fzf`
- [ ] Tasks to practice:
  1. "Explain the architecture of this project" (use plan mode)
  2. "Find where error messages are defined and add a new one"
  3. "Find a TODO comment in the codebase and implement it"
  4. "Write a test for function X"
- [ ] After each change, run `git diff` and **read every line of the diff**. Do you understand what changed? Could you explain it to an engineer?

**Exercise**: Use Claude Code to make 3 different modifications to the project. For each one, write a 2-sentence "PR description" explaining what changed and why.

**✅ Week 4 Goal**: Can use Claude Code to navigate a codebase, explain code, and make targeted edits — and can explain what changed to a human.

---

### Week 5: Codex Mastery
**Start date**: ___________

#### Saturday (2 hrs): Codex Setup & Workflow
- [ ] Set up Codex CLI (`codex` command) and the web UI (codex.openai.com or ChatGPT Codex)
- [ ] Understand the Codex model:
  - Cloud-based sandbox: Codex runs your code in a container, not on your machine
  - Task-based: You give it a task, it works autonomously, you review the result
  - Parallel execution: Can run multiple tasks simultaneously
  - Diff-based output: Shows you what it changed, you approve/reject
- [ ] Key differences from Claude Code:
  - Claude Code = pair programming (you drive, AI assists)
  - Codex = delegation (you assign, AI executes, you review)
  - Claude Code runs locally; Codex runs in the cloud
  - Claude Code is better for exploration; Codex is better for execution
- [ ] Run your first Codex task:
  - Point it at your Week 3 server project
  - "Add input validation to the POST /items endpoint. Return 400 if the name is empty or the price is negative."

**Exercise**: Give Codex and Claude Code the same task. Compare: Which was faster? Which produced better code? Which did you learn more from?

#### Sunday (2 hrs): Codex Parallel Workflows
- [ ] Practice Codex's strength — parallel task execution:
  - Task 1: "Add request logging middleware"
  - Task 2: "Add rate limiting to the API"
  - Task 3: "Add Swagger/OpenAPI documentation"
  - Run all 3 simultaneously, review each diff
- [ ] Practice the review workflow:
  - For each Codex output: Read the diff. Understand it. Approve or request changes.
  - If you don't understand something, ask Claude Code to explain it (this is a legit power combo)
- [ ] Build your personal mental model:
  - When do I use Claude Code? → Understanding code, complex multi-file changes, exploration, learning
  - When do I use Codex? → Well-defined tasks, parallel execution, quick fixes, boilerplate

**Exercise**: Define your personal "decision tree" for when to use Claude Code vs Codex. Write it down. (You'll refine it over the remaining weeks.)

**✅ Week 5 Goal**: Can use Codex for parallel task execution and knows when to reach for each tool. Has a written decision framework for Claude Code vs Codex.

---

### Week 6: Your First Real Bug Fix
**Start date**: ___________

#### Saturday (2 hrs): Finding & Understanding a Bug
- [ ] Go to GitHub and find a "good first issue" on a Go project:
  - Search: `https://github.com/search?q=language%3Ago+label%3A%22good+first+issue%22+state%3Aopen`
  - Pick one that's a bug fix (not a feature). Ideally something contained in 1-2 files.
  - Good candidates: CLI tools, small libraries, HTTP utilities
- [ ] Before touching code, UNDERSTAND the bug:
  - Read the issue description completely
  - Clone the repo
  - Use Claude Code: "Explain this repo's architecture" then "Help me understand issue #X. Where in the code does this bug likely live?"
  - Find the buggy code yourself (Claude Code can help, but YOU navigate)
  - Read the existing tests — does a test cover this case? If not, that's part of the fix.
- [ ] Write up your understanding:
  - What's the bug? (plain English)
  - Where does it live? (file + line number)
  - What's the expected behavior?
  - What's the actual behavior?
  - What's the fix? (plain English, before writing code)

**Exercise**: Write the bug analysis above BEFORE writing any code. This is the PM superpower — understanding the problem clearly before jumping to solutions.

#### Sunday (2 hrs): Fixing & Submitting
- [ ] Implement the fix:
  - Create a branch: `git checkout -b fix/issue-XXX`
  - Use Claude Code to implement: give it your analysis from Saturday
  - READ the diff carefully — do you understand every change?
  - Run tests: `go test ./...`
  - If tests fail, understand WHY before asking Claude to fix them
- [ ] Write a good PR:
  - Title: concise, starts with a verb ("Fix", "Add", "Update")
  - Description: What, Why, How, Testing
  - Link to the issue
- [ ] Submit the PR:
  - `git push -u origin fix/issue-XXX`
  - Create PR on GitHub (or use `gh pr create`)
  - Be ready for review comments — this is learning, not a test

**Exercise**: Submit the PR. If you get review comments, respond thoughtfully. Use Claude Code to understand the feedback, but write your OWN response (don't let Claude comment on the PR for you).

**✅ Week 6 Goal**: Has submitted a real PR fixing a real bug on an open-source project. Can explain the bug, the fix, and why it works.

---

### Week 7: Your First Feature
**Start date**: ___________

#### Saturday (2 hrs): Design Before Code
- [ ] Pick a small feature to build. Options:
  - **Option A**: Add a feature to your Week 3 server (e.g., search/filter, pagination, export to CSV)
  - **Option B**: Build a small CLI tool that solves a real problem you have (e.g., a Slack status updater, a meeting notes formatter, a JIRA ticket creator)
  - **Option C**: Find a "feature request" issue on an open-source project
- [ ] Apply PM thinking BEFORE coding:
  - What's the user story?
  - What are the acceptance criteria?
  - What's the simplest possible implementation? (MVP mindset)
  - What would you hand off to an engineer for v2?
- [ ] Write a mini-spec (1 page max):
  - What it does
  - API/interface design
  - Edge cases to handle
  - What you're explicitly NOT building (scope)
- [ ] Use Claude Code in plan mode to validate your approach:
  - "Here's what I want to build: [spec]. Review my approach and suggest improvements."

#### Sunday (2 hrs): Build & Ship
- [ ] Implement the feature using your AI tool of choice (or both):
  - If it's well-defined → Codex (fast execution)
  - If it requires exploration → Claude Code (better understanding)
- [ ] Test it:
  - Does it work for the happy path?
  - What happens with bad input?
  - Write at least 1 test
- [ ] Write handoff documentation:
  - "If an engineer were to productionize this, here's what they'd need to change..."
  - This is the unique PM-builder skill: shipping the POC AND knowing what corners you cut
- [ ] Push it. Create a PR or just push to your personal repo.

**Exercise**: Write the handoff doc. This is the artifact that makes a PM-builder valuable — you didn't just spec it, you built it AND know what needs to happen next.

**✅ Week 7 Goal**: Has shipped a feature end-to-end: spec → code → test → handoff doc. Can demo it to someone.

---

## Phase 3: Production Readiness (Weeks 8–10)
*Operating in the real environment with real stakes.*

---

### Week 8: Code Review Literacy
**Start date**: ___________

#### Saturday (2 hrs): Reading Code Reviews Like an Engineer
- [ ] What engineers care about in code review:
  - **Correctness**: Does it actually work? Edge cases?
  - **Error handling**: What happens when things fail? (In Go: `if err != nil`)
  - **Tests**: Are there tests? Do they cover the important cases?
  - **Naming**: Are variables/functions named clearly?
  - **Simplicity**: Is this the simplest solution? (YAGNI — You Ain't Gonna Need It)
  - **Performance**: Any obvious N+1 queries or unnecessary loops?
  - **Security**: SQL injection? Unvalidated input? Secrets in code?
- [ ] Go to GitHub, find 5 merged PRs on a Go project you know. Read the review comments.
  - What did reviewers flag?
  - Do you understand why they flagged it?
  - Use Claude Code to explain any comments you don't understand
- [ ] Common Go review patterns:
  - "This should return an error, not panic"
  - "Use `context.Context` for cancellation"
  - "This isn't concurrent-safe"
  - "Add a test for the error case"

**Exercise**: Read 5 PR review threads. For each reviewer comment, write whether you (a) understood it immediately, (b) understood it after Claude explained, or (c) still don't get it. Category (c) items are your study list.

#### Sunday (2 hrs): Responding to Reviews Intelligently
- [ ] Practice the review response workflow:
  1. Read the comment
  2. Understand what they're asking for (use Claude Code if needed)
  3. Decide: Do you agree? Is it a style preference or a real issue?
  4. Implement the fix yourself (with AI help)
  5. Write a response explaining what you changed and why
- [ ] The key skill: **Know what you changed and why**
  - ❌ "Fixed per your comment" (you're just a proxy for the AI)
  - ✅ "Good catch — the nil check was missing because `FindUser` can return nil when the user doesn't exist. Added the check and a test for that case."
- [ ] Go back to your Week 6 or Week 7 PR. Imagine an engineer left these comments. Use Claude Code to understand and implement fixes:
  - "This doesn't handle the case where the input is nil"
  - "Can you add a test for the error path?"
  - "This function is doing too much — split it into two"

**Exercise**: For each of the 3 simulated review comments above, implement the fix AND write the response comment. Focus on explaining the "why."

**✅ Week 8 Goal**: Can read code review comments, understand what engineers are asking for, and respond intelligently with real fixes — not just "the AI said to do this."

---

### Week 9: Testing & CI/CD
**Start date**: ___________

#### Saturday (2 hrs): Writing & Running Tests
- [ ] Go testing fundamentals:
  - Test files: `thing_test.go` next to `thing.go`
  - Test functions: `func TestDoThing(t *testing.T)`
  - `t.Errorf()`, `t.Fatalf()`, `t.Run()` for subtests
  - Table-driven tests (the Go way)
  - Running tests: `go test ./...`, `go test -v -run TestSpecific`
- [ ] Write tests for your Week 3 server:
  - Test the GET /health endpoint returns 200
  - Test POST /items with valid data returns 201
  - Test POST /items with invalid data returns 400
  - Test GET /items returns the items you created
- [ ] Use Claude Code to help write tests, but understand the pattern:
  ```go
  // Arrange: set up test data
  // Act: call the function
  // Assert: check the result
  ```

**Exercise**: Write 3 tests WITHOUT your AI tool first (they can be wrong). Then use your AI tool to fix them. Compare your version with the AI's — what did you miss?

#### Sunday (2 hrs): CI/CD & Build Systems
- [ ] What CI/CD is and why it matters:
  - CI: Continuous Integration — runs tests automatically on every push
  - CD: Continuous Deployment — deploys automatically when tests pass
  - GitHub Actions: the most common CI system for open-source
- [ ] Read a `.github/workflows/*.yml` file from an open-source project:
  - What triggers it? (push, PR, schedule)
  - What does it do? (lint, test, build, deploy)
  - How do you read CI output when it fails?
- [ ] Set up GitHub Actions on your personal repo:
  - Use Claude Code: "Add a GitHub Actions workflow that runs `go test ./...` on every push"
  - Push a change, watch it run, read the output
- [ ] Practice debugging a CI failure:
  - Intentionally break a test, push, watch CI fail
  - Read the error output, fix it, push again

**Exercise**: Break a test, push, read the CI failure, fix it, push the fix. Do this 3 times until the CI output feels readable.

**✅ Week 9 Goal**: Can write a basic Go test, run tests locally, set up CI, and debug a CI failure.

---

### Week 10: Multi-Language Comfort & Kotlin Basics
**Start date**: ___________

#### Saturday (2 hrs): Kotlin Fundamentals
- [ ] Why Kotlin matters in industry:
  - Android development
  - Backend services (JVM ecosystem)
  - Kotlin is like "modern Java" — cleaner syntax, null safety
- [ ] Key Kotlin concepts (reading, not writing):
  - `val` (immutable) vs `var` (mutable)
  - Null safety: `String?` means nullable, `?.` safe call, `!!` force unwrap
  - Data classes: `data class Payment(val id: String, val amount: Int)`
  - Functions: `fun processPayment(payment: Payment): Result`
  - When expressions (like switch/match)
  - Coroutines (async, like Go goroutines but different)
- [ ] Read Kotlin code with Claude Code:
  - Clone a Kotlin project (e.g., `https://github.com/square/okhttp` — a widely-used HTTP client)
  - "Explain the structure of this project"
  - "What does this class do?" (pick a few)
  - You don't need to write Kotlin — just read it and use AI tools to modify it

**Exercise**: Read 3 Kotlin files from OkHttp. Write a 1-sentence summary of each. Verify with Claude Code.

#### Sunday (2 hrs): Operating Across Languages
- [ ] Practice using AI tools in an unfamiliar language:
  - Pick a Kotlin or Java "good first issue" and work through it the same way as Week 6
  - The skill isn't "knowing Kotlin" — it's "being able to operate in any language with AI assistance"
- [ ] Quick exposure to other common backend tech:
  - JavaScript/TypeScript: Spend 30 min reading a small Node.js project
  - Rust: Just awareness — increasingly used for performance-critical infrastructure
  - Protocol Buffers / gRPC: How services talk to each other (ask Claude Code to explain)
- [ ] The meta-skill: When you encounter unfamiliar code in any language:
  1. Ask your AI tool to explain the file/function
  2. Identify the pattern (handler, service, model, test)
  3. Patterns are the same across languages — only syntax changes

**Exercise**: Use Claude Code to make a small change to a Kotlin project. Write the same "PR description" format you practiced in Week 4.

**✅ Week 10 Goal**: Not scared of Kotlin/Java code. Can use AI tools to read, understand, and modify code in languages you don't know well. Understands that patterns > syntax.

---

## Phase 4: Capstone & Reflection (Weeks 11–12)
*Putting it all together.*

---

### Week 11: Capstone Project
**Start date**: ___________

#### Saturday (2 hrs): Build Something Real
- [ ] Choose a capstone project — something that shows PM-as-builder skill:
  - **Option A**: Internal tool — a CLI or small web app that solves a real pain point at your company (e.g., a script that automates a manual process, a dashboard for tracking something)
  - **Option B**: Open-source contribution — a meaningful feature (not just a typo fix) to a project you care about
  - **Option C**: Developer tool — something related to AI-assisted development (e.g., a tool that helps PMs write better prompts, a script that summarizes PR review comments)
  - **Option D**: AI tool extension — build a custom slash command, MCP server, or task template for your AI coding tool of choice
- [ ] Spec it out (PM-style):
  - Problem statement (1 sentence)
  - User story (1 sentence)
  - Acceptance criteria (3-5 bullets)
  - Out of scope (3 bullets)
  - Technical approach (1 paragraph, validated with your AI tool)
- [ ] Start building. Use both tools. Track your decisions.

#### Sunday (2 hrs): Ship & Document
- [ ] Finish the project (keep scope small — shipping > perfection)
- [ ] Write the handoff doc:
  - What it does
  - How to run it
  - Architecture decisions and trade-offs
  - What an engineer would need to change for production
  - Known limitations
- [ ] Push to GitHub as a public repo
- [ ] Record a 2-minute demo video or write a short blog post

**Exercise**: Show the project to someone — an engineer friend, a PM peer, post it online. Get feedback.

**✅ Week 11 Goal**: Has a portfolio piece that demonstrates: I can identify a problem, spec it, build it, ship it, and write the handoff for an engineer to scale it.

---

### Week 12: Reflect & Plan Forward
**Start date**: ___________

#### Saturday (2 hrs): Build Your Narrative
- [ ] Document your journey:
  - Before: "I could write prompts but couldn't understand or verify the output"
  - After: "I can navigate a codebase, fix bugs, ship POC features, review code, and hand off to engineers with clear context"
  - Proof: Your GitHub activity, PRs, capstone project
- [ ] Articulate the "PM who builds" value proposition:
  - "The next generation of PMs needs to be technical enough to prototype, not just spec"
  - "I use Claude Code for deep exploration and complex changes, and Codex for parallel execution of well-defined tasks"
  - "My value isn't in the code I write — it's in knowing what to build, building a quick POC to validate, and writing the handoff doc so an engineer can scale it"

#### Sunday (2 hrs): Level-Set & Plan Forward
- [ ] Skills assessment — can you do these?
  - [ ] Clone a repo and navigate it confidently
  - [ ] Read Go/Kotlin code and understand what it does
  - [ ] Fix a contained bug with AI assistance
  - [ ] Ship a small feature end-to-end
  - [ ] Write and run tests
  - [ ] Respond to code review comments intelligently
  - [ ] Use Claude Code for exploration and complex tasks
  - [ ] Use Codex for parallel execution of defined tasks
  - [ ] Write handoff documentation for engineers
  - [ ] Explain your technical decisions to an engineer
- [ ] Plan your next 3 months:
  - What areas are still weak? Double down.
  - Set a goal: 1 PR per week (even small ones)
  - Consider: Start a blog or internal knowledge base about "PM-as-builder" practices

**Exercise**: Do a mock "explain your approach" session. Record yourself explaining: "Here's how I built [capstone project], the tools I used, the decisions I made, and what I'd do differently." Watch it back.

**✅ Week 12 Goal**: Has a clear narrative, a portfolio, and a forward plan. Can pass a "build something in an hour" exercise.

---

## Quick Reference: Tool Decision Tree

```
Need to understand unfamiliar code?
  → Claude Code (plan mode, ask it to explain)

Need to make a complex, multi-file change?
  → Claude Code (better context, keeps you in the loop)

Need to execute 3+ well-defined tasks quickly?
  → Codex (parallel execution, cloud sandbox)

Need to fix a specific, contained bug?
  → Either works. Codex if fast, Claude Code if you want to learn.

Need to write/review tests?
  → Claude Code (better at understanding intent and edge cases)

Need to understand a PR review comment?
  → Claude Code (ask it to explain, then YOU write the response)

Need to prototype a feature?
  → Start with Claude Code (explore, plan), finish with Codex (execute)
```

---

## Weekly Rhythm

| Day | Time | Activity |
|-----|------|----------|
| Saturday | 2 hrs | Learn new concept + guided practice |
| Sunday | 2 hrs | Apply it on real code + ship something |

**Saturday = Input.** Learn, read, explore.
**Sunday = Output.** Build, fix, ship.

---

## Resources

- **Go**: [Go by Example](https://gobyexample.com) — best reference, skip the tutorial and use as-needed
- **Git**: [Oh My Git!](https://ohmygit.org) — visual game for learning git
- **Claude Code docs**: `/help` in the CLI, or [docs.anthropic.com](https://docs.anthropic.com)
- **Codex docs**: [platform.openai.com/docs/codex](https://platform.openai.com/docs/codex)
- **Practice repos**: GitHub "good first issues" — search by language and label
- **The missing skill**: Reading code is more important than writing it. Spend 60% of your time reading, 40% writing.

---

## Ground Rules

1. **Don't just prompt — understand.** After every AI-generated change, read the diff and explain it to yourself.
2. **Break things intentionally.** The fastest way to learn is to make a change, see it break, understand why.
3. **Keep a learning journal.** 3 bullets after each session: what I learned, what confused me, what I want to explore next.
4. **Ship over perfection.** A bad PR that ships teaches you more than a perfect plan that doesn't.
5. **Your PM skills are a superpower.** Engineers often code first and think later. You think first — that's your edge.

---

## Contributing

This plan is open source. If you're a PM going through this journey:
- Open an issue to share what worked or didn't
- Submit a PR to improve the curriculum
- Share your learnings in the Discussions tab
- Adapt it for your own language/stack (Python, TypeScript, Rust, etc.)
