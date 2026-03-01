# Week 1, Saturday: Terminal & Dev Environment Mastery

## Context

This is the detailed lesson plan for Week 1, Saturday of the [12-week PM-as-Builder plan](~/Documents/pm-builder-12-week-plan.md). The original plan calls for installing tools + terminal essentials. Since your dev environment is already set up (Homebrew, Go 1.24.1, VS Code, Git 2.49.0, zsh, Claude Code), we skip installation entirely and use the full 2 hours for terminal mastery.

**Goal:** Move from "I can type commands I've been told to type" to "I understand what my terminal is, how it finds programs, and how to navigate confidently."

**Output:** A markdown file at `~/Documents/pm-builder-week1-saturday.md` containing the full lesson plan below.

---

## Schedule (2 hours)

| Time | Block | Activity |
|------|-------|----------|
| 0:00–0:15 | Reading 1 | What is your terminal and shell? |
| 0:15–0:35 | Exercise 1 | Audit your own machine (with Claude) |
| 0:35–0:50 | Reading 2 | Navigation and file manipulation commands |
| 0:50–1:10 | Exercise 2 | Navigation obstacle course (with Claude) |
| 1:10–1:15 | -- | Break |
| 1:15–1:25 | Reading 3 | PATH, environment variables, shell config |
| 1:25–1:45 | Exercise 3 | Trace your PATH and understand your .zshrc (with Claude) |
| 1:45–1:50 | Reading 4 | Piping and redirection |
| 1:50–2:05 | Exercise 4 | Piping drills (with Claude) |
| 2:05–2:15 | Exercise 5 | Clone golang/example and explore it (with Claude) |
| 2:15–2:25 | Exercise 6 | Capstone scavenger hunt (with Claude) |
| 2:25–2:30 | -- | Self-assessment checklist |

---

## Readings

### Reading 1: What Is Your Terminal and Shell? (15 min)

Read these in order:

1. **Mac Terminal Command Line Guide — main page** (5 min)
   https://mac.install.guide/terminal/
   Focus on: The distinction between Terminal (the app) and zsh (the shell running inside it). Read the main page only.

2. **Mac Terminal Guide — ".zshrc or .zprofile" page** (10 min)
   https://mac.install.guide/terminal/zshrc-zprofile
   Focus on: The four zsh config files (`.zshenv`, `.zprofile`, `.zshrc`, `.zlogin`), login vs. non-login shells, and why macOS treats every new Terminal window as a login shell. Don't memorize the load order — just understand these files exist and get loaded at different times.

**Key takeaways:**
- Terminal.app is just a window; zsh is the program interpreting your commands
- Every new Terminal window on macOS is a login shell
- `.zprofile` runs once per login (good for PATH); `.zshrc` runs for every interactive shell (good for aliases)

---

### Reading 2: Navigation and File Manipulation Commands (15 min)

1. **GitHub Mac Terminal Cheat Sheet** (10 min)
   https://github.com/0nn0/terminal-mac-cheatsheet
   Focus on: SHORTCUTS, CORE COMMANDS, FILE MANAGEMENT, DIRECTORY MANAGEMENT, and CHAINING COMMANDS sections.

2. **Terminal Cheat Sheet (web)** (5 min)
   https://terminalcheatsheet.com/
   Skim "The Basics" and "Modify Files and Folders" as reinforcement.

**Commands to know cold:**

| Command | What it does |
|---------|-------------|
| `pwd` | Print current directory |
| `ls` / `ls -la` | List files / list all with details |
| `cd dirname` | Move into a directory |
| `cd ..` / `cd ~` / `cd -` | Up one / home / previous directory |
| `mkdir name` / `mkdir -p a/b/c` | Create directory / nested directories |
| `touch file.txt` | Create an empty file |
| `cp source dest` / `cp -r` | Copy file / copy directory recursively |
| `mv source dest` | Move or rename |
| `rm file` / `rm -r dir` | Delete file / delete directory (permanent!) |
| `cat file` | Print file contents |
| `open .` | Open current directory in Finder |

---

### Reading 3: PATH, Environment Variables, and Shell Config (10 min)

1. **Mac Terminal Guide — "Mac Path" page** (5 min)
   https://mac.install.guide/terminal/path
   Focus on: What PATH is, how it's a colon-separated list, why order matters (shell searches left-to-right), how to add to it.

2. **OSX Hub — macOS Shell Configuration Guide** (5 min)
   https://osxhub.com/macos-shell-configuration-zsh-environment-variables/
   Skim: "Configuration File Hierarchy" and "PATH Management" sections only.

**Key mental model:** When you type `go` and hit Enter, your shell searches every directory in your PATH left-to-right and runs the first `go` it finds. On your machine, that's `/opt/homebrew/bin/go`. If `/opt/homebrew/bin` weren't in your PATH, you'd get "command not found."

---

### Reading 4: Piping and Redirection (5 min)

1. **GitHub Mac Terminal Cheat Sheet — PIPING COMMANDS section**
   https://github.com/0nn0/terminal-mac-cheatsheet

**The mental model in one paragraph:** Every command produces output (stdout). The pipe (`|`) feeds that output as input to the next command. The redirect (`>`) writes output to a file (overwriting). The append redirect (`>>`) adds to the end of a file. That's it. These three operators are what make the terminal powerful.

---

## Exercises (with Claude)

### Exercise 1: Audit Your Own Machine (20 min)

Paste this into Claude Code:

```
I'm learning terminal basics. I want to understand my own machine's setup. Please help me by running these commands one at a time, showing me the output, and explaining what each one means in plain English:

1. echo $SHELL
2. which zsh
3. which go
4. which brew
5. which git
6. echo $HOME
7. pwd
8. ls -la ~/
9. echo $PATH (break it apart by the colons and explain what each directory is for)
10. cat ~/.zprofile
11. cat ~/.zshrc
12. cat ~/.zshenv

After showing me all of these, give me a one-paragraph summary of "what my machine looks like" as a developer — where are my tools installed, what shell am I using, and what config files are active.
```

---

### Exercise 2: Navigation Obstacle Course (20 min)

Paste this into Claude Code:

```
I want to practice terminal navigation and file manipulation. Please give me a series of 10 challenges, one at a time. For each challenge:
1. Tell me what to do in plain English
2. Wait for me to tell you the command I would use
3. Tell me if I'm right or wrong, and if wrong, explain why and show the correct command
4. Then verify by actually running the command

Start with easy ones and get harder. The challenges should cover:
- cd, ls, pwd (first 3 challenges)
- mkdir, touch, creating nested structures (challenges 4-5)
- cp, mv, renaming (challenges 6-7)
- rm (challenge 8)
- Using ~ and .. and - for navigation (challenges 9-10)

Use /tmp/pm-builder-practice as the working directory so we don't mess up my real files. Create it first.
```

---

### Exercise 3: Trace Your PATH and Understand Your Shell Config (20 min)

Paste this into Claude Code:

```
I want to deeply understand PATH and environment variables on my machine. Walk me through these exercises interactively:

PART A - PATH forensics:
1. Show me my current PATH, split by colons so I can read it
2. For each directory in my PATH, tell me: does it exist? What important tools live there?
3. Run "which go" and "which git" and "which brew" — then show me that those paths are inside directories listed in my PATH
4. Show me what happens conceptually when I type "go version" — trace the PATH lookup

PART B - Environment variables:
5. Show me all my environment variables (run "env") and highlight the 5 most important ones for a developer, explaining each
6. Show me the difference between "export MY_VAR=hello" (session only) vs putting it in .zshrc (permanent)
7. Quiz me: ask me 3 questions about PATH and environment variables, let me answer, then correct me

PART C - Shell config files:
8. Read my ~/.zprofile, ~/.zshrc, and ~/.zshenv. For each one, explain line by line what it does and WHY it's in that particular file instead of one of the others
9. Explain why "eval "$(/opt/homebrew/bin/brew shellenv)"" is in .zprofile and not .zshrc
```

---

### Exercise 4: Piping Drills (15 min)

Paste this into Claude Code:

```
Teach me piping and redirection through 6 progressively harder challenges. For each one:
1. Describe what I need to accomplish
2. Let me try to write the command
3. Tell me if I'm right, then run it so I can see the output

Use /tmp/pm-builder-practice as our workspace.

Challenges should cover:
- Challenge 1: Use ls and pipe to wc -l to count files in a directory
- Challenge 2: Use cat and pipe to grep to search for a word in a file (create a sample file first)
- Challenge 3: Use echo and > to write text to a new file, then >> to append to it
- Challenge 4: Use ls -la, pipe to grep to find only directories
- Challenge 5: Use cat on a file, pipe to sort, pipe to uniq to get unique lines (create a file with duplicates first)
- Challenge 6: Combine: create a file that contains the sorted, unique output of another file

After all 6 challenges, explain the difference between | and > in one sentence.
```

---

### Exercise 5: Clone golang/example and Explore It (10 min)

Paste this into Claude Code:

```
Help me clone and explore the Go example repository. Walk me through step by step:

1. Clone it: git clone https://github.com/golang/example.git ~/Development/golang-example

2. After cloning, show me the directory structure and what Go files exist

3. Show me the contents of hello/hello.go and explain what each line does at a high level (I don't need to understand Go yet — just the structure)

4. Show me how to navigate around this repo using only cd, ls, and pwd:
   - Go into the hello directory
   - Go back to the repo root using cd ..
   - Jump back to home with cd ~
   - Get back to the repo using the full path

5. Open the repo in VS Code from the terminal with "code ."

This repo will be our playground for the rest of the 12-week course.
```

---

### Exercise 6: Capstone Scavenger Hunt (10 min)

Paste this into Claude Code:

```
I've been learning terminal basics for the past 2 hours. Give me a 10-question scavenger hunt to test what I've learned. For each question:
1. Ask me to find or do something using terminal commands
2. I'll tell you the command I'd use
3. Grade me pass/fail, explain if I got it wrong, and move on

Questions should cover ALL of today's topics:
- 2 questions on navigation (cd, ls, pwd)
- 2 questions on file operations (mkdir, cp, mv, rm, touch)
- 2 questions on PATH and which
- 2 questions on piping and redirection
- 1 question on environment variables
- 1 question on shell config files

Keep score. I need at least 7/10 to "pass" this week's lesson.
```

---

## Self-Assessment Checklist

After completing all exercises, check these off. If any answer is "no," redo the relevant exercise.

**Navigation:**
- [ ] I can tell my current directory without looking at the prompt (`pwd`)
- [ ] I can list all files including hidden ones (`ls -la`)
- [ ] I can navigate using both absolute and relative paths
- [ ] I know what `cd -` does and have used it
- [ ] I use Tab completion instinctively

**File Operations:**
- [ ] I can create nested directories in one command (`mkdir -p`)
- [ ] I know when I need `-r` and when I don't
- [ ] I understand that `rm` is permanent — there is no trash can

**PATH and Environment:**
- [ ] I can explain what PATH is and why it matters
- [ ] I can trace how my shell finds the `go` binary when I type `go version`
- [ ] I know which file sets up Homebrew's PATH (`~/.zprofile`)
- [ ] I know the difference between `.zprofile` and `.zshrc`
- [ ] I can check where any command lives using `which`

**Piping and Redirection:**
- [ ] I can explain the difference between `|`, `>`, and `>>`
- [ ] I can chain two commands with a pipe
- [ ] I can redirect output to a file

**Setup:**
- [ ] I have the golang/example repo cloned
- [ ] I can open any directory in VS Code from the terminal with `code .`

---

## Keyboard Shortcuts to Practice All Week

| Shortcut | What it does |
|----------|-------------|
| Tab | Autocomplete file/directory names |
| Ctrl+C | Kill the current command |
| Ctrl+R | Search command history |
| Ctrl+A | Jump to beginning of line |
| Ctrl+E | Jump to end of line |
| Ctrl+L | Clear screen |
| Up arrow | Scroll through previous commands |

---

## Delivery

1. Save this lesson plan to `~/Documents/pm-builder-week1-saturday.md`
2. Push it to `https://github.com/conrado44/pm-builder-training` (clone the repo if needed, add the file, commit, push)

---

## Verification

To verify the lesson is complete:
1. All 6 exercises completed with Claude Code
2. Scored 7/10 or better on the capstone scavenger hunt
3. All self-assessment checkboxes checked
4. golang/example repo cloned and openable in VS Code

## What's Next

**Tomorrow (Sunday):** Git Fundamentals — you'll use the terminal skills from today to learn git clone, branch, add, commit, push. The golang/example repo you cloned today will be your first practice repo.
