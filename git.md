# Git

Version Control System used extensively for file tracking a change management

# Config

### Setup file locations

<code>[path]/etc/gitconfig</code> - System level configuration</br>
<code>~/.gitconfig</code> - User level configuration</br>
<code>.git/config</code> - Local repo level configuration</br>

### Settings

<code>git config --system [options]</code> - System level configuration</br>
<code>git config --global [options]</code> - User level configuration</br>
<code>git config --local [options]</code> - Local repo level configuration</br>

### First time setup

<code>git config --global user.name [name]</code> - Name used on all commits</br>
<code>git config --global user.email [email]</code> - Email used on all commits</br>
<code>git config --global core.editor [editor]</code> - Default editor</br>
<code>git config --global init.defaultBranch [name]</code> - Set the default branch name to [name]</br>

### View config

<code>git config --list</code> - Show all settings</br>
<code>git config [setting]</code> - Show single setting (e.g user.name)</br>

### Aliases

<code>git config --global alias.[name] [args]</code> - create an [alias] that runs 'git [args]'</br>
<code>git config --global --unset alias.[alias]</code> - unsets the alias [alias]</br>

### Alias Example

<code>git config --global alias.history "log --oneline --graph --decorate --all"</code> - 'git history' now runs the provided arguments</br>

### Status

<code>git status</code> - View repo current status</br>

# Creating a new repo

<code>git init</code> - initialize a new repository</br>
<code>git clone [url]</code> - clone an existing repository</br>
<code>git clone [url] [name]</code> - clone an existing repository in directory called [name]</br>
<code>git clone --branch [branch] depth 1 [url] </code> - clone only the latest commit from [branch]</br>

# Adding and removing files

<code>git add [file]</code> - add [file] to staging area</br>
<code>git add .</code> - add all modified files in the current directory to staging area</br>
<code>git rm -f [file]</code> - forcefully deletes the file from source control and disk **!!**</br>
<code>git rm --cached [file]</code> - stops tracking the file in source control</br>

### View tracked files

<code>git ls-files</code> - shows what files are tracked in the repository</br>

# Committing

<code>git commit -m "message"</code> - commit staged changes with a "message"</br>
<code>git commit -a -m "message"</code> - commit all tracked files without staging first with a "message"</br>
<code>git commit --amend</code> - redo a commit in the event of an error <a href="https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things">Git Book - Undoing Things</a></br>

### Commit history

<code>git log</code> - shows all commits in the repos history</br>
<code>git log --stat</code> - shows all commits with additions/removals</br>
<code>git log -p -[n]</code> - shows [n] most recent commits and the patches (changes) made</br>
<code>git log --pretty=oneline</code> - shows all commits as hashes and messages</br>
<code>git log -S [string]</code> - shows all commits that changed the given value [string]</br>
<code>git log --oneline --graph --decorate --all</code> - shows all commits as a graph of branches</br>

### Reflog

<code>git reflog</code> - view the history of the HEAD pointer

### File differences

<code>git diff</code> - shows what's been changed but not staged for all files</br>
<code>git diff [path]</code> - shows what's been changed but not staged in file at [path] </br>
<code>git diff [path] [path2]</code> - shows the difference between file at [path] and file at [path2]</br>
<code>git diff --staged</code> - shows what will go into your next commit</br>
<code>git show</code> - shows last commit data including a diff</br>

# Checking out

<code>git checkout [hash]</code> - changes the HEAD to a previous commit identified by [hash]</br>
<code>git checkout [branch]</code> - changes the HEAD to point to [branch]</br>
<code>git checkout -- [file]</code> - reverts a modified file back to last commit state **!!**</br>

# Revert and Restore

<code>git revert [hash]</code> - reverts the effect of a commit as a new commit</br>
<code>git restore [file]</code> - revert modifications to [file]</br>
<code>git restore --staged [file]</code> - unstage changes to [file]</br>

# Reset

<code>git reset HEAD [file]</code> - same as <code>git restore --staged [file]</code></br>
<code>git reset --soft [hash]</code> - resets HEAD back to commit [hash] - does not change the index</code></br>
<code>git reset --mixed [hash]</code> - resets HEAD back to commit [hash] - clears the index</code></br>
<code>git reset --hard [hash]</code> - resets HEAD back to commit [hash] - clears the index and working directory **!!**</code></br>

# Working remotely

### Remote locations

<code>git remote -v</code> - view the current remote names and locations</br>
<code>git remote add [name] [url]</code> - set a remote location with a [name] at [url]</br>
<code>git remote rm [name]</code> - removes a remote location [name]</br>
<code>git remote show [name]</code> - view remote tracking information</br>
<code>git remote rename [old_name] [new_name]</code> - set a remotes name to [new_name]</br>
<code>git remote set-url [name] [url]</code> - update a remote location with a [name] to [url]</br>

### Pushing and pulling

<code>git fetch</code> - fetch the latest remote commits and branches without merging</br>
<code>git fetch [remote]</code> - fetch the latest commits from [remote] without merging</br>
<code>git fetch -p</code> - prune any remote tracked branches that are no longer found locally</br>
<code>git pull</code> - pull the latest commits from remote to current tracked branch and try to merge</br>
<code>git pull [remote] [branch]</code> - pull the latest commits from [remote] [branch] and try to merge</br>
<code>git push</code> - push your latest commits from HEAD to tracked remote branch</br>
<code>git push [remote] [branch]</code> - push your latest commits on [branch] to [remote]</br>

# Branches

<code>git checkout -b [name]</code> - create branch [name] from the current branch and point HEAD to it</br>
<code>git checkout [branch]</code> - changes the HEAD to point to [branch]</br>

</br>

<code>git branch</code> - lists branches</br>
<code>git branch -a</code> - lists branches with remotes</br>
<code>git branch [name]</code> - create branch [name] from the current branch</br>
<code>git branch -d [name]</code> - delete branch [name]</br>

### Set remote branch tracking

<code>git pull --set-upstream-to=[remote]/[remote_branch] [branch]</code> - track local [branch] with [remote]/[remote_branch]</br>
<code>git push --set-upstream [remote] [branch]</code> - track local [branch] with [remote]</br>
<code>git push -u [remote] [branch]</code> - shorthand for <code>--set-upstream</code></br>

### Delete remote branch

<code>git push [remote] --delete [branch]</code> - delete [branch] from [remote]</br>

### Merging

<code>git merge [branch]</code> - merge [branch] into the current branch you are on (auto fast forward if possible)</br>
<code>git merge [branch] --no-ff</code> - merge [branch] into the current branch you are on with a merge commit</br>

# Rebasing

<code>git rebase [branch]</code> - rebase the branch you are on into [branch]</br>

# Tagging

<code>git tag</code> - list tags</br>
<code>git tag -l [string]</code> - list tags matching string</br>
<code>git tag [tag]</code> - creates a lightweight tag and tags the commit at HEAD</br>
<code>git tag -a [tag] -m [message]</code> - creates an annotated [tag] with a [message] and tags the commit at HEAD</br>
<code>git tag -a [tag] [hash]</code> - creates an annotated [tag] with a [message] and tags the commit at [hash]</br>
<code>git tag [tag] [branch]</code> - creates a lightweight [tag] on the latest commit in [branch]</br>
<code>git tag -f [tag] [commit]</code> - moves the [tag] to the [commit] (omitting [commit] tags HEAD)</br>

### View tag data

<code>git show [tag]</code> - shows tag data and the commit that was tagged</br>

### Remote tags

<code>git push [remote] [tag]</code> - pushes a [tag] to a [remote] (tags are not included in <code>git push</code> by default)</br>
<code>git push --force [remote] [tag]</code> - force pushes a [tag] to a [remote], overwriting existing tag</br>

### Delete tags

<code>git tag -d [tag]</code> - deletes [tag]</br>
<code>git push [remote] --delete [tag]</code> - deletes [tag] from remote server</br>

# Stashing

<code>git stash</code> - stash modified files off current branch</br>
<code>git stash list</code> - list stashed modifications</br>
<code>git stash pop</code> - bring changes back to current branch</br>

# .gitignore file

### Stop tracking already committed file

<code>git rm --cached [file]</code> - stops tracking the file in source control</br>
<code>git commit -m "stopped tracking file"</code> - commit the change</br>
<code>Add file to .gitignore</code> - ignore the file</br>
<code>**!!** IF CENTRALLY STORED THIS DELETES THE FILE FOR OTHER USERS ON THEIR NEXT PULL **!!**</code></br>

### Ignoring files

<pre>
# ignore all .a files
*.a

# but do track lib.a, even though you're ignoring .a files above
!lib.a

# only ignore the TODO file in the current directory, not subdir/TODO
/TODO

# ignore all files in any directory named build
build/

# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

# ignore all .pdf files in the doc/ directory and any of its subdirectories
doc/**/*.pdf

# ignore all directories matching dir/ in the entire project
**/dir/
</pre>
