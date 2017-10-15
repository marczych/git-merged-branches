# git-merged-branches

`git-merged-branches` prints out the merge status of all local branches in a
git repository.

## Motivation

Sometimes you work on a repository for a few years and end up with hundreds of
branches in a local git repository. Which ones have been merged already? Which
ones are hiding useful code that you forgot you hadn't finished yet?

One solution is to use `git branch --merged origin/master`. However, that
doesn't work if branches have been rebased or squashed as part of being merged.
`git-merged-branches` instead uses `git cherry` to find equivalent commits on
the base branch to see if the branch in question has been merged.

## Usage

The script at `./git-merged-branches` can be executed directly or via `git` if
the script is on your `PATH`.

```bash
./git-merged-branches
git merged-branches
```

> NOTE: This command moves HEAD, commits squashed branches, and generally does
> disrespectful things to the reflog. This should not cause any permanent
> damage, though.

## Example

```bash
$ git merged-branches
Merged: feature-a
Merged: feature-b
Unmerged: feature-d
Merged: feature-y
```

The merged branches can be deleted by piping the output like so:

```bash
git merged-branches | grep Merged: | sed 's#^Merged: ##' | xargs git branch --delete --force
```

## License

[Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0)
