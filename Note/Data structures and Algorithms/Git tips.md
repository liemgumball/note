# Why `.gitignore` Doesn't Stop Already-Tracked Files

## Problem
Sometimes, after adding a file (e.g., `.obsidian/workspace.json`) to `.gitignore`, Git still shows changes to that file when running `git status`.

## Why?
- **`.gitignore` only prevents new, untracked files from being added to Git.**
- If a file was already committed in the past, Git will **continue tracking changes** to that file, even if it's now in `.gitignore`.

## Solution: Stop Tracking Without Deleting the File

To stop Git from tracking a file (but keep the file on disk):

```bash
git rm --cached <file_path>
```


> [!info] Like a deleted status for git
> Seeing the ==Stop tracking== like creating a `deleted file` change of git for the file with actually delete the file.

## Related

- [[Shell cmd, Git, HTML, CSS]]
- [[Git begin]]
