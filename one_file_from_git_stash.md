# Only extract a specific file from git stash

https://stackoverflow.com/questions/1105253/how-would-i-extract-a-single-file-or-changes-to-a-file-from-a-git-stash

git diff stash@{0}^1 stash@{0} -- <filename>

On the git stash manpage you can read (in the "Discussion" section, just after "Options" description) that:

A stash is represented as a commit whose tree records the state of the working directory, and its first parent is the commit at HEAD when the stash was created.

So you can treat stash (e.g. stash@{0} is first / topmost stash) as a merge commit, and use:

$ git diff stash@{0}^1 stash@{0} -- <filename>
Explanation: stash@{0}^1 means the first parent of the given stash, which as stated in the explanation above is the commit at which changes were stashed away. We use this form of "git diff" (with two commits) because stash@{0} / refs/stash is a merge commit, and we have to tell git which parent we want to diff against. More cryptic:
