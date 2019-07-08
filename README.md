# Git Commit Date Spoofing

Git allows _full_ control over "author date" and "committer date". These values can be set _arbitrarily_ when creating commits.

## Linux / macOS (bash/zsh)

```sh
GIT_AUTHOR_DATE="2019-07-08T13:21:24Z" \
GIT_COMMITTER_DATE="2019-07-08T13:21:24Z" \
git commit -m "changed dependency"
```

## Windows PowerShell

```ps
$env:GIT_AUTHOR_DATE="2019-07-08T13:21:24Z"
$env:GIT_COMMITTER_DATE="2019-07-08T13:21:24Z"

git commit -m "changed dependency"
```

## Example

```sh
curl -s https://api.github.com/repos/pcaversaccio/test-spoof-commit-date/commits/b91babe024462be201cf61a7b42e8a6771250b7c | jq '.commit | {author_date: .author.date, committer_date: .committer.date}'
```

will return

```json
{
  "author_date": "2019-07-08T13:21:24Z",
  "committer_date": "2019-07-08T13:21:24Z"
}
```

I pushed this commit however on 2026-04-10T08:37:05Z in reality.
