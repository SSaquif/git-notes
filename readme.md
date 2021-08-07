# Git Notes

All things git

## Contents

<!-- toc -->

- [Git Notes](#git-notes)
  - [Contents](#contents)
  - [Creating Snapshots](#creating-snapshots)
    - [Initializing a repository](#initializing-a-repository)
    - [Staging files](#staging-files)
    - [Viewing the status](#viewing-the-status)
    - [Committing the staged files](#committing-the-staged-files)
    - [Skipping the staging area](#skipping-the-staging-area)
    - [Removing files](#removing-files)
    - [Renaming or moving files](#renaming-or-moving-files)
    - [Viewing the staged/unstaged changes](#viewing-the-stagedunstaged-changes)
    - [Viewing the history](#viewing-the-history)
    - [Viewing a commit](#viewing-a-commit)
    - [Unstaging files (undoing git add)](#unstaging-files-undoing-git-add)
    - [Discarding local changes](#discarding-local-changes)
    - [Restoring an earlier version of a file](#restoring-an-earlier-version-of-a-file)
  - [Sumodules](#sumodules)
    - [Adding a Submodule](#adding-a-submodule)
    - [Updating a Submoudle](#updating-a-submoudle)
    - [Removing a submodule](#removing-a-submodule)

<!-- tocstop -->

## Creating Snapshots

### Initializing a repository

```bash
git init
```

### Staging files

```bash
git add file1.js           # Stages a single file
git add file1.js file2.js  # Stages multiple files
git add \*.js              # Stages with a pattern
git add .                  # Stages the current directory
```

### Viewing the status

```bash
git status
git status -s # Short status
```

### Committing the staged files

```bash
git commit -m “Message”    # Commits with a one-line message
git commit                 # Opens the default editor to type msg
```

### Skipping the staging area

```bash
git commit -am “Message”
```

### Removing files

```bash
git rm file1.js           # Removes from working directory and staging area
git rm --cached file1.js  # Removes from staging area only
```

### Renaming or moving files

```bash
git mv file1.js file1.txt
```

### Viewing the staged/unstaged changes

```bash
git diff            # Shows unstaged changes
git diff --staged   # Shows staged changes
git diff --cached   # Same as the above
```

### Viewing the history

```bash
git log              # Full history
git log --oneline    # Summary
git log --reverse    # Lists the commits from the oldest to the newest
```

### Viewing a commit

```bash
git show 921a2ff       # Shows the given commit
git show HEAD          # Shows the last commit
git show HEAD~2        # Two steps before the last commit
git show HEAD:file.js  # Shows the version of file.js stored in the last commit
```

### Unstaging files (undoing git add)

```bash
git restore --staged file.js # Copies the last version of file.js from repo to index
```

### Discarding local changes

```bash
git restore file.js            # Copies file.js from index to working directory
git restore file1.js file2.js  # Restores multiple files in working directory
git restore .                  # Discards all local changes (except untracked files)
git clean -fd                  # Removes all untracked files
```

### Restoring an earlier version of a file

```bash
git restore --source=HEAD~2 file.js
```

## Sumodules

### Adding a Submodule

```bash
git submodule add shh/url-link-to-repo
```

### Updating a Submoudle

Or you can do update with remote swtich

```bash
git submodule update --remote                         # update all
git submodule update --remote <path to the submodule> # path can be found in .gitmodules file
```

Note: (Need to verify this). Apparently another way is, you can go into the individual submodule from the parent/super repo and do a regular pull (fetch and merge) in those modules.

### Removing a submodule

Need to learn This
