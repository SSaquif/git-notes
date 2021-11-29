# Git Notes

All things git

This is a work in progress

TODO (incomplete list):

1. Basics of branches, (check the workflow for now)
2. Git rebase
3. Git hooks

## Contents

<!-- toc -->

- [Git Notes](#git-notes)
  - [Contents](#contents)
  - [Creating Snapshots](#creating-snapshots)
    - [Initializing a repository](#initializing-a-repository)
    - [Viewing the status](#viewing-the-status)
    - [Staging (Adding) files](#staging-adding-files)
    - [Committing the Staged Files](#committing-the-staged-files)
    - [Skipping the staging area](#skipping-the-staging-area)
    - [Removing files](#removing-files)
    - [Renaming or moving files](#renaming-or-moving-files)
    - [Pushing to an Remote Repo](#pushing-to-an-remote-repo)
    - [View List of Remote Repos](#view-list-of-remote-repos)
    - [Adding & Removing Remote Repos](#adding--removing-remote-repos)
    - [Viewing the staged/unstaged changes](#viewing-the-stagedunstaged-changes)
    - [Viewing the history](#viewing-the-history)
    - [Viewing a commit](#viewing-a-commit)
    - [Unstaging files (undoing git add)](#unstaging-files-undoing-git-add)
    - [Discarding local changes](#discarding-local-changes)
    - [Restoring an earlier version of a file](#restoring-an-earlier-version-of-a-file)
    - [Reverting Commits](#reverting-commits)
  - [Git Submodules](#git-submodules)
    - [Adding a Submodule](#adding-a-submodule)
    - [Specifying Branch](#specifying-branch)
    - [Updating a Submoudle](#updating-a-submoudle)
    - [Removing a submodule](#removing-a-submodule)

<!-- tocstop -->

## Creating Snapshots

### Initializing a repository

```bash
git init
```

### Viewing the status

```bash
git status
git status -s # Short status
```

### Staging (Adding) files

```bash
git add file1.js           # Stages a single file
git add file1.js file2.js  # Stages multiple files
git add \*.js              # Stages with a pattern
git add .                  # Stages the current directory
```

Alternatively on VSCode you can use the `+` symbol in the source control tab to add files to the staging area

### Committing the Staged Files

```bash
git commit -m “Message”    # Commits with a one-line message
git commit                 # Opens the default editor to type msg
```

Alternatively you can write the commit message on VSCode. Go to the source control tab, then in the commit message text box (at the top) write your message and click the tick icon

### Skipping the staging area

```bash
git commit -am “Message”  # add + commit all changed files
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

### Pushing to an Remote Repo

```bash
git push <remote-name> <branch-to-push>
# example
git push origin master
```

You can also push from VSCode Source Control tab. Click on the `...` icon and then select `push`

### View List of Remote Repos

```bash
git remote -v
```

### Adding & Removing Remote Repos

```bash
git remote add <remote-name> <repo-url> # add
# example
git remote add origin <url u got from github, gitlab etc>

git remote rm <remote-name> # remove
# example
git remote rm origin
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

### Reverting Commits

[Stacko](https://stackoverflow.com/questions/23227927/how-do-i-move-master-back-several-commits-in-git)

In order to do it locally, you can do the following commands to go to master and move it to the old commit.

```bash
git checkout master
git reset --hard <old_commit_id>
```

If you then want to push it to the remote, you need to use the -f option.

```bash
git push -f origin master
```

## Git Submodules

### Adding a Submodule

```bash
git submodule add <ssh/url-link-to-repo>
# add into a nested folde
git submodule add <path_to_local_folder>/<ssh/url-link-to-repo>
```

### Specifying Branch

You can specify the branch to add and pull from in the `.gitmodules file` by adding the branch as below

```bash
[submodule "git-notes"]
	path = git-notes
	url = git@github.com:SSaquif/git-notes.git
	branch = main
```

### Updating a Submoudle

You can do update with remote switch

[Why we need --remote](https://stackoverflow.com/questions/47470271/what-does-remote-actually-do-in-git-submodule-update-remote), if we want to pull master

```bash
git submodule update                                  # Update using the revison being tracked
git submodule update --remote                         # update all
git submodule update --remote <path to the submodule> # path can be found in .gitmodules file
```

Note: (Need to verify this). Apparently another way is, you can go into the individual submodule from the parent/super repo and do a regular pull (fetch and merge) in those modules.

### Removing a submodule

[Video Tutorial](https://www.youtube.com/watch?v=6pGxk0B_Ino)

There are a few steps to it, see below

```bash
# Step 1: git remove
git rm <module_name>
# Step 2: remove form the '.git' folder, the folder is usually has same name as module
rm -rf .git/modules/module_folder
# Step 3: Remove it from the '.gitmodules' file. (This happens automatically now, but still check)
# Step 4: Add and commit changes
git commit -am 'Removed submodule <module name>'
```
