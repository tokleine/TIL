# Interactive Git Rebase to Edit Commit History

## tl;dr
Use `git rebase -i <commit-id>^` to interactively edit, reorder, squash, or delete commits starting from the commit before `<commit-id>`.

## Description
Today I needed to clean up my messy commit history (mostly to fix some commit messages, while keeping the commits otherwise untouched) before merging a feature branch. 

The solution is interactive rebase with the `^` symbol to include the target commit:

```bash
git rebase -i abc1234^
```

The `^` means "start from the parent of this commit", so if you want to edit commit `abc1234`, you need `abc1234^` to include it in the rebase.

This opens your editor with something like:
```
pick abc1234 Add user authentication
pick def5678 Fix typo in auth
pick ghi9012 Add missing import
pick jkl3456 Update documentation
```

You can then change `pick` to e.g.:
- **reword** - Edit the commit message  

For example, to squash the typo fix:
```
reword abc1234 Add user authentication
pick def5678 Fix typo in auth
pick ghi9012 Add missing import
pick jkl3456 Update documentation
```

Save and close the editor, and Git will prompt you to update the commit message of `abc1234` and not touch the rest.

Just use `git rebase -i <commit>^` and clean up that history! 😊
