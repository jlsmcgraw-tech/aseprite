# Issue-Based Task Proposals

This document captures four concrete tasks found while scanning the codebase.

## 1) Typo fix task

**Task:** Fix misspelled words in comments such as `circuntance` -> `circumstance` in `ink_processing.h`.

**Why:** Typos in internal comments reduce readability and make code search harder.

**References:**
- `src/app/tools/ink_processing.h` (multiple comments with `circuntance`)

## 2) Bug fix task

**Task:** Remove or refactor the global `tmpGradientBuffer` to avoid shared mutable state in gradient processing.

**Why:** The code explicitly marks this global buffer as non-thread-safe; concurrent rendering/tool operations could race.

**References:**
- `src/app/tools/ink_processing.h` (`static ImageBufferPtr tmpGradientBuffer; // TODO non-thread safe`)

## 3) Documentation discrepancy task

**Task:** Update `tests/README.md` to reflect the current CI behavior (tests are run in the same checked-out repo, not from a separately cloned tests directory).

**Why:** The README states that this directory is cloned by `build.yml`, but current workflow uses a regular `actions/checkout` of the repository and then executes `tests/run-tests.sh`.

**References:**
- `tests/README.md`
- `.github/workflows/build.yml`

## 4) Test improvement task

**Task:** Add a regression test that codifies and validates frame handle behavior after frame insertion/deletion (or update API semantics and tests accordingly).

**Why:** Existing test notes a known issue where retained frame objects are stale after frame list mutations.

**References:**
- `tests/scripts/frames.lua` (TODO about frame object/frame number consistency after add/delete)
