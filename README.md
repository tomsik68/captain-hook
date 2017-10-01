# Captain hook

Captain Hook is a simple system to manage your git hooks.

## Concept

The key concept is, that you have a central collection of your git hooks stored in ~/git-hooks . 
Rather than copying and/or manually combining these hooks in each of your repositories,
Captain Hook lets you symlink & combine your scripts to produce sensible git hooks.

### How Captain Hook combines hooks

When git calls Captain Hook, it will search appropriate script directory(based on hook type) and try to execute every script forwarding all arguments from git. If any of the scripts fails, Captain Hook exits forwarding the return code of your script to git. Captain Hook only executes scripts up to the first script that fails.

For more concrete & in-depth explanation, check `hookrun` script.

## Quick Start

Prerequisite: Our collection contains a script `check-diff` which can be used as a pre-commit hook(as specified by git).

+ `mkdir new_project && cd new_project`
+ `git init`
+ `hook init`
+ `hook add pre-commit check-diff`

The hook is now setup, so that every time git runs its `pre-commit` hook, Captain Hook will call your script check-diff. The best part is, that your script is just a symlink, so modifying your hook will update all your repositories!

## Installation

### General steps

Just clone this repo to somewhere, fix `CPTHOOK_DIR` and `HOOKS_DIR` in `hook` script and make sure `hook` script is in your `PATH`.

### Example installation

+ `cd ~`
+ `git clone https://github.com/tomsik68/captain-hook.git`
+ `echo 'export PATH="PATH:$HOME/captain-hook"' >> ~/.bashrc`
+ `cd captain-hook && mkdir hooks`
