#git

The deletion process also uses `git rm` (since git1.8.5 October 2013).

## Summary

The 3-steps removal process would then be:

```
0. mv a/submodule a/submodule_tmp

1. git submodule deinit -f -- a/submodule
2. rm -rf .git/modules/a/submodule
3. git rm -f a/submodule
# Note: a/submodule (no trailing slash)

# or, if you want to leave it in your working tree and have done step 0
3.   git rm --cached a/submodule
3bis mv a/submodule_tmp a/submodule

```

## Explanation

`rm -rf`: This is mentioned in [Daniel Schroeder](https://stackoverflow.com/users/2753241/daniel-schroeder)'s [answer](https://stackoverflow.com/a/26505847/6309), and summarized by [Eonil](https://stackoverflow.com/users/246776/eonil) in [the comments](https://stackoverflow.com/questions/1260748/how-do-i-remove-a-git-submodule/16162000?noredirect=1#comment41729982_16162000):

> This leaves .git/modules/<path-to-submodule>/ unchanged.So if you once delete a submodule with this method and re-add them again, it will not be possible because repository already been corrupted.
> 

---

`git rm`: See [commit 95c16418](https://github.com/git/git/commit/95c16418f0375e2fc325f32c3d7578fba9cfd7ef):

> Currently using "git rm" on a submodule removes the submodule's work tree from that of the superproject and the gitlink from the index.But the submodule's section in .gitmodules is left untouched, which is a leftover of the now removed submodule and might irritate users (as opposed to the setting in .git/config, this must stay as a reminder that the user showed interest in this submodule so it will be repopulated later when an older commit is checked out).
> 

> Let "git rm" help the user by not only removing the submodule from the work tree but by also removing the "submodule.<submodule name>" section from the .gitmodules file and stage both.
> 

---

`git submodule deinit`: It stems from [this patch](http://git.661346.n2.nabble.com/PATCH-v3-submodule-add-deinit-command-td7576946.html):

> With "git submodule init" the user is able to tell git they care about one or more submodules and wants to have it populated on the next call to "git submodule update".But currently there is no easy way they can tell git they do not care about a submodule anymore and wants to get rid of the local work tree (unless the user knows a lot about submodule internals and removes the "submodule.$name.url" setting from .git/config together with the work tree himself).
> 

> Help those users by providing a 'deinit' command.This removes the whole submodule.<name> section from .git/config either for the given submodule(s) (or for all those which have been initialized if '.' is given).Fail if the current work tree contains modifications unless forced.Complain when for a submodule given on the command line the url setting can't be found in .git/config, but nonetheless don't fail.
> 

This takes care if the (de)initialization steps (`.git/config` and `.git/modules/xxx`)

Since git1.8.5, the `git rm` takes *also* care of the:

- '`add`' step which records the url of a submodule in the `.gitmodules` file: it is need to removed for you.
- the submodule **[special entry](https://stackoverflow.com/questions/1992018/git-submodule-update-needed-only-initially/2227598#2227598)** (as illustrated by [this question](https://stackoverflow.com/q/16574625/6309)): the git rm removes it from the index:`git rm --cached path_to_submodule` (no trailing slash)That will remove that directory stored in the index with a special mode "160000", marking it as a submodule root directory.

If you forget that last step, and try to add what was a submodule as a regular directory, you would get error message like:

```
git add mysubmodule/file.txt
Path 'mysubmodule/file.txt' is in submodule 'mysubmodule'
```