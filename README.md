# CP Journey Template

A small competitive programming workspace for C++20 practice.

Clone it, run one setup command, and start solving problems with a consistent folder structure, template file, sample downloader, local tester, notes file, and editor tasks.

## Use This Template

This repository is meant to be the upstream template.

Each user should fork it and solve problems in their own fork. That keeps personal solutions separate while still allowing template updates to be pulled later.

1. Fork this repository on GitHub.
2. Clone your fork:

```sh
git clone <your-fork-url>
cd <repo-name>
```

3. Run setup:

```sh
./scripts/setup
```

4. Open a new terminal or source the shell rc file printed by setup.
5. Create practice folders under `practice/`.
6. Start problems with `cpnew`.

The setup script also configures `upstream` automatically when the repo looks like a fork or personal clone. It does not fetch or merge upstream updates.

Check remotes:

```sh
git remote -v
```

Expected setup:

```text
origin    <your-fork-url>
upstream  git@github.com:sambuaneesh/cp-cpp-starterkit.git
```

## Pull Template Updates

When this template gets updates, pull them into your fork:

```sh
git fetch upstream
git merge upstream/main
```

Then push the updated fork:

```sh
git push origin main
```

If you prefer a linear history, use rebase instead of merge:

```sh
git fetch upstream
git rebase upstream/main
git push origin main
```

Use either merge or rebase consistently.

To keep updates easy, put your solutions under `practice/` and avoid changing shared files unless you are intentionally customizing them:

```text
scripts/
templates/
.vscode/
.zed/
README.md
```

Template updates usually touch shared files like scripts, editor tasks, and documentation. Your daily solutions should mostly live under `practice/`, so updates should merge cleanly most of the time.

## Requirements

- `uv` - used to install `oj`
- `g++` - used to compile C++20 solutions
- `python3` - used by `cprun` to generate failure reports
- `bash` - used by the helper scripts

## Setup

Run once after cloning:

```sh
./scripts/setup
```

The setup script installs or updates `oj` with:

```sh
uv tool install --upgrade git+https://github.com/sambuaneesh/oj.git
```

It also adds these directories to `PATH`:

- this repository's `scripts/` directory, so `cpnew` and `cprun` work from any problem folder
- uv's tool bin directory, so `oj` is available from the terminal

It also adds the starterkit as `upstream` when appropriate. To use a different upstream URL:

```sh
CP_TEMPLATE_UPSTREAM_URL=<template-repo-url> ./scripts/setup
```

After setup, open a new terminal or source the shell rc file printed by the script.

To skip automatic `PATH` changes:

```sh
./scripts/setup --no-path
```

## Daily Usage

Create a problem folder:

```sh
cpnew "<problem-url>"
```

Create a problem folder with a custom name:

```sh
cpnew "<problem-url>" my_problem_name
```

Run the current solution from inside a problem folder:

```sh
cprun
```

Run a specific C++ file:

```sh
cprun solution.cpp
```

## What This Gives You

`cpnew` creates a ready-to-use problem folder:

- creates a clean folder name from the problem URL
- copies `templates/main.cpp`
- downloads samples into `test/` using `oj download`
- creates `notes.md` with problem metadata
- detects common judges for notes and folder names

`cprun` handles local testing:

- compiles with `g++ -std=c++20 -O2 -pipe -Wall -Wextra -Wshadow -DLOCAL`
- runs `oj test` when a `test/` directory exists
- supports `input.txt` for quick manual testing
- writes `output.txt` and `debug.log` for manual runs
- creates `main.cprun.md` when sample tests fail
- tries to split multi-testcase samples and show the failing testcase clearly
- captures `cerr` / `dbg()` output in the failure report

## Repository Layout

```text
.
|-- practice/          # Put solved problems here
|-- scripts/
|   |-- cpnew          # Create a problem folder from a URL
|   |-- cprun          # Compile and test a solution
|   `-- setup          # Install oj and configure PATH
|-- templates/
|   `-- main.cpp       # Default C++20 template
|-- .vscode/           # VS Code tasks/settings
|-- .zed/              # Zed tasks
|-- .clangd
|-- .clang-format
`-- README.md
```

## Example Organization

One practical way to organize practice is by sheet, rating, and problem:

```text
practice/
`-- cp31/
    |-- 800/
    |   `-- cf_1903_A/
    |       |-- main.cpp
    |       |-- notes.md
    |       `-- test/
    |           |-- sample-1.in
    |           `-- sample-1.out
    `-- 900/
        |-- cf_1878_C/
        |-- cf_1883_B/
        `-- cf_1904_A/
```

From inside a rating folder, create a new problem:

```sh
cd practice/cp31/900
cpnew "https://codeforces.com/problemset/problem/1904/A"
```

This creates:

```text
practice/cp31/900/cf_1904_A/
|-- main.cpp
|-- notes.md
`-- test/
    |-- sample-1.in
    `-- sample-1.out
```

Because the folder is under `practice/cp31/900/`, `notes.md` also gets:

```yaml
sheet: "cp31"
rating: 900
```

## Supported Sites

This repository uses `oj` for downloading samples and running tests. According to the official `online-judge-tools` documentation, `oj` is designed for downloading sample cases, testing solutions, logging in, and submitting code.

The `online-judge-tools/api-client` support table lists sample-case support for:

- Aizu Online Judge
- Anarchy Golf
- AtCoder
- AtCoder Problems virtual contests
- CodeChef
- Codeforces
- CS Academy
- Facebook Hacker Cup
- Google Code Jam
- Google Kick Start
- HackerRank
- Kattis
- Library Checker
- PKU JudgeOnline
- Sphere Online Judge
- Topcoder archived problems
- Toph
- yukicoder

This template has explicit folder-name and metadata handling for:

- Codeforces
- AtCoder
- Library Checker
- yukicoder
- Aizu Online Judge
- Kattis

Other `oj`-supported URLs still work through the fallback folder-name logic.

References:

- `oj` project: <https://github.com/online-judge-tools/oj>
- `oj` getting started: <https://github.com/online-judge-tools/oj/blob/master/docs/getting-started.md>
- supported websites table: <https://github.com/online-judge-tools/api-client#supported-websites>

## Notes Workflow

Each problem folder gets a `notes.md` file:

```yaml
---
title: "cf_1903_A"
link: "https://codeforces.com/problemset/problem/1903/A"
judge: "codeforces"
status: "unsolved"
created_at: "YYYY-MM-DD"
folder: "cf_1903_A"
contest_id: "1903"
problem_id: "A"
---
```

Use it to track approach, mistakes, status, and review notes.

If a problem is created inside a path like `practice/cp31/800/`, `cpnew` also adds:

```yaml
sheet: "cp31"
rating: 800
```

## Editor Tasks

VS Code and Zed tasks are included.

They call `scripts/cprun` directly from this repository, so editor runs do not depend on the shell loading the updated `PATH`.

Default task:

- compile and test the current file

Sanitizer task:

- compile with address and undefined behavior sanitizers
- useful for catching memory errors and undefined behavior during debugging

## Manual Tests

For quick one-off testing, create `input.txt` in a problem folder:

```text
1
5
```

Then run:

```sh
cprun
```

The script writes:

- `output.txt`
- `debug.log`

These files are ignored by git.

## Failure Reports

When sample tests fail, `cprun` writes:

```text
main.cprun.md
```

The report includes:

- failed sample summary
- expected output
- actual output
- isolated testcase rerun when possible
- stderr / `dbg()` output

If testcase splitting is wrong for a problem, add one of these files in the problem folder:

```text
.cprun-case-lines
.cprun-no-t
```

Use `.cprun-case-lines` when each testcase has a fixed number of input lines.

Use `.cprun-no-t` when isolated reruns should not prepend `T = 1`.

## Customization

Edit the default C++ template:

```text
templates/main.cpp
```

Change compiler flags in:

```text
scripts/cprun
```

Add or change editor tasks in:

```text
.vscode/tasks.json
.zed/tasks.json
```

## Starting Your Own Journey

Fork this repository or use it as a template.

Recommended first steps:

1. Update this README title if you want a personal name.
2. Edit `templates/main.cpp` to match your coding style.
3. Run `./scripts/setup`.
4. Create folders under `practice/`.
5. Start problems with `cpnew`.
6. Test solutions with `cprun`.
