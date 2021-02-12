<img src="https://i.ibb.co/YbmYYyK/main-git-commands.png" align="center" alt="Main Git Commands" border="0">

<p align="center">
   <img alt="Stars" src="https://img.shields.io/github/stars/gabrieldejesus/git-commands?color=4A90E2&label=STARS&logo=3C424B&logoColor=3C424B&style=for-the-badge&labelColor=222222" />

   <img alt="Forks" src="https://img.shields.io/github/forks/gabrieldejesus/git-commands?color=4A90E2&label=FORKS&logo=3C424B&logoColor=3C424B&style=for-the-badge&labelColor=222222" />

   <img alt="Issues" src="https://img.shields.io/github/issues/gabrieldejesus/git-commands?color=4A90E2&label=ISSUES&logo=3C424B&logoColor=3C424B&style=for-the-badge&labelColor=222222" />

   <img alt="GitHub license" src="https://img.shields.io/github/license/gabrieldejesus/git-commands?color=4A90E2&label=LICENSE&logo=3C424B&logoColor=3C424B&style=for-the-badge&labelColor=222222" />

  <a href="https://github.com/gabrieldejesus">
    <img alt="Follow gabrieldejesus" src="https://img.shields.io/static/v1?label=Follow&message=gabrieldejesus&style=for-the-badge&color=4A90E2&labelColor=222222" />
  </a>
</p>

<h1 align="center">
 Main Git Commands
</h1>

<p align="center">
  <a href="README.md">English</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="README.pt.md">Português</a>&nbsp;&nbsp;&nbsp;
</p>

- Starting a Repository

  `git init`

---

- Listing Modified Files

  `git status`

---

- Undoing Changes

  - Unmonitored files

    `git checkout`

  - To delete new files that have not yet been added to the Stage

    `git clean -df`

  - Removing files from the Stage

    `git reset`

  - Undoing the last commit

    `git revert HEAD`

---

- Rename Commit

  `git commit —amend`

---

- Branches

  - Listing local Branches

    `git branch`

  - Also list the branches that are in the remote repository

    `git branch -a`

  - Going to another branch

    `git checkout my-branch`

  - If you add -b a new branch will be created

    `git checkout -b my-new-branch`

  - Excluding branches

    `git branch -d branch-name // normal`

    `git branch -D branch-name // forcing`

  - Renaming branches

    `git branch -m new-branch-name`

  - If you are on a branch and want to rename another one, you must first pass the current name of the branch you want to rename:

    `git branch -m current-name new-name`

  - Orphan Branch
    An orphaned branch has this name because it is not linked to the main branch, so
    their histories are not shared.

  ```shell
    Example:
         i --- j --- k <== branch 'my branch'
               /
       a --- b --- c --- d --- h --- l <== branch 'main'
           \ /
             and --- f --- g <== branch 'my other branch'

       1 --- 2 --- 3 --- 4 <== `orphaned 'branch
  ```

  This can be useful when you want to place more than one project in the same
  repository. A good example is when you have a project on Github and want to create
  a website to publicize your project. The application and the website are different things,
  therefore, their codes must be versioned separately.
  Having both in the same repository simplifies management.

  To create an orphaned branch just use the command:

  `git checkout --orphan my-branch-orphan`

---

- Viewing Commit History

  `git log`

  - History of one or more files

    `git log -p my-files`

  - Author's history

    `git log --author = name-author`

  - History by date

    `git log --after = "MMM DD YYYY"`

    `git log --before = "MMM DD YYYY"`

  - History Based on a message (commit)

    `git log --grep products`

    With this command we will have the history of commits in which the commit message
    has the word “products”. What we go through can be a regular expression,
    and we can spend more than one:

  Examples:

  Search for "products" OR "users"

  `git log --grep products --grep users`

  Search for "products" AND "users"

  `git log --grep products --and --grep users`

---

- Display branches in a more readable mode

  It is possible to have the history printed showing the branches of the repository with something
  more readable and in color with a command. We will have a result similar to this:

  ```shell
    * a102055 (HEAD -> master) commit 8
    | * 196d28e (branch-2) commit 7
    | * 07e073c commit 3
    | * 2b077ca new fie
    | | * c1369d8 (branch-3) commit 6
    | | * d11bdcd commit 5
    | | /
    | / |
    * | 2b22b75 commit 2
    | /
    * d5a12b0 .gitignore
    * 9535426 - commit 1
  ```

  The command is a little long:

  `git log --all --decorate --oneline --graph`

  To decorate everything we should write after the log.

  ```
    --all
    --decorate
    --oneline
    --graph
  ```

---

- Working on more than one thing without committing

  There may be times when you need to stop what you are doing and start working
  in another task. However, it may not be good to commit something that has not yet been
  finalized and then return to it, resulting in a commit that will be in the history
  but it has code that doesn't work. We can save these changes made
  even without having to perform a commit to later work on it again, which is
  called a Stash (something like "hide" or "accumulate").

  By doing this, your repository will return to the state of the last commit, and the changes
  previously made will be “hidden”.

  - Saving changes to a Stash

    `git stash`

  - You can still put a name on this stash

    `git stash push -m my-name-stash`

  - Listing Stash

    `git stash list`

  - Recovering modifications

    `git stash apply`

  This will retrieve the most recent stash code. If you want to recover a stash
  oldest, just look at the number of the stash that appears when we list it and pass
  for the following command:

  `git stash apply stash @ {2}`

  - Removing Stashes

    When we retrieve changes from a stash, it remains saved. To delete it
    from the stack, run the drop command next to the name of the stash you want to remove

    `git stash drop stash @ {5}`

---
