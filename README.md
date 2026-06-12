# CP CPP Starterkit

A ready-to-use C++20 competitive programming setup.

It gives you:

- `cpnew` to create a problem folder from a URL
- `cprun` to compile and test locally
- sample download through `oj`
- a clean `practice/` structure
- VS Code and Zed tasks

## Quick Start

Fork this repo, then clone your fork:

```sh
git clone <your-fork-url>
cd <repo-name>
./scripts/setup
```

Open a new terminal after setup.

Start solving:

```sh
mkdir -p practice/cp31/900
cd practice/cp31/900
cpnew "https://codeforces.com/problemset/problem/1904/A"
cd cf_1904_A
cprun
```

## Requirements

- `uv`
- `g++`
- `python3`
- `bash`

`setup` installs `oj` and adds the helper scripts to `PATH`.

## Daily Commands

Create a problem:

```sh
cpnew "<problem-url>"
```

Create with a custom folder name:

```sh
cpnew "<problem-url>" my_problem
```

Run tests:

```sh
cprun
```

Run a specific file:

```sh
cprun solution.cpp
```

## How To Organize

Use folders however you like. A practical structure is:

```text
practice/
`-- cp31/
    |-- 800/
    |   `-- cf_1903_A/
    `-- 900/
        |-- cf_1878_C/
        |-- cf_1883_B/
        `-- cf_1904_A/
```

Each problem folder contains:

```text
cf_1904_A/
|-- main.cpp
|-- notes.md
`-- test/
    |-- sample-1.in
    `-- sample-1.out
```

If you create a problem under `practice/cp31/900/`, `notes.md` also records:

```yaml
sheet: "cp31"
rating: 900
```

## What Happens On `cpnew`

`cpnew`:

- makes a folder name from the URL
- copies `templates/main.cpp`
- downloads samples with `oj download`
- creates `notes.md`

Supported directly for naming/metadata:

- Codeforces
- AtCoder
- Library Checker
- yukicoder
- Aizu Online Judge
- Kattis

Other `oj`-supported sites can still work through fallback naming.

## What Happens On `cprun`

`cprun`:

- compiles with C++20
- runs `oj test` if `test/` exists
- runs with `input.txt` if present
- writes `output.txt` and `debug.log` for manual runs
- writes `main.cprun.md` when tests fail

Use `cerr` or the provided `dbg(x)` macro for debug output.

## Pull Starterkit Updates

Your fork keeps your solutions. This repo stays as the starterkit upstream.

After setup, remotes should look like:

```text
origin    <your-fork-url>
upstream  git@github.com:sambuaneesh/cp-cpp-starterkit.git
```

To pull starterkit updates:

```sh
git fetch upstream
git merge upstream/main
git push origin main
```

`setup` adds `upstream` automatically when it looks like you are in a fork. It does not fetch or merge anything.

## Manual Testing

For quick testing without sample files:

```text
input.txt
```

Then run:

```sh
cprun
```

Output files:

```text
output.txt
debug.log
```

These are ignored by git.

## Customize

Edit your template:

```text
templates/main.cpp
```

Edit compiler flags or test behavior:

```text
scripts/cprun
```

Editor tasks:

```text
.vscode/tasks.json
.zed/tasks.json
```

## Supported Sites

Sample downloading and testing comes from `oj`.

Useful references:

- <https://github.com/online-judge-tools/oj>
- <https://github.com/online-judge-tools/api-client#supported-websites>
