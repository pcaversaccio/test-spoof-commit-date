# Git Commit Date Spoofing

Git allows _full_ control over "author date" ([`GIT_AUTHOR_DATE`](https://git-scm.com/docs/git-commit#_commit_information)) and "committer date" ([`GIT_COMMITTER_DATE`](https://git-scm.com/docs/git-commit#_commit_information)). These values can be set _arbitrarily_ when creating commits.

## Linux/macOS (bash/zsh)

```sh
~$ GIT_AUTHOR_DATE="2019-07-08T13:21:24Z" \
GIT_COMMITTER_DATE="2019-07-08T13:21:24Z" \
git commit -m "changed dependency"
```

## Windows PowerShell

```powershell
~$ $env:GIT_AUTHOR_DATE="2019-07-08T13:21:24Z"
~$ $env:GIT_COMMITTER_DATE="2019-07-08T13:21:24Z"
~$ git commit -m "changed dependency"
```

## Example

Let's inspect commit [`3e8db9983cffafb5342ae752fbee4af89dd3efa9`](https://github.com/pcaversaccio/test-spoof-commit-date/commit/3e8db9983cffafb5342ae752fbee4af89dd3efa9):

```sh
curl -s https://api.github.com/repos/pcaversaccio/test-spoof-commit-date/commits/3e8db9983cffafb5342ae752fbee4af89dd3efa9 | jq '.commit | {author_date: .author.date, committer_date: .committer.date}'
```

which returns:

```json
{
  "author_date": "2019-07-08T13:21:24Z",
  "committer_date": "2019-07-08T13:21:24Z"
}
```

The commit was actually pushed at 2026-04-10T09:11:50Z.
