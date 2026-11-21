# PDA-upt-sem5-Projects

This is a git repo, using submodules, for tracking our work across 4 different projects covering each of these Parallel and Distributed Algorithms technologies: POSIX threads, OpenMP, CUDA, MPI.

## Structure

This repository is a **superproject**. Each technology lives in its own independent git repository, linked here as a **submodule**:

| Folder     | Technology    | Owner |
|------------|---------------|-------|
| `CUDA/`    | CUDA          | Christian |
| `OpenMP/`  | OpenMP        | TBD   |
| `MPI/`     | MPI           | TBD   |
| `Pthreads/`| POSIX threads | TBD   |

A submodule is just a pointer: the superproject records which commit of each submodule repo to check out. The actual work lives in the submodule repos and is pushed/pulled independently.

## Cloning this project (for everyone)

Submodules are **not** downloaded by a plain `git clone`. Use one of these:

```bash
# Option A: clone everything in one go
git clone --recurse-submodules https://github.com/ChrisMicea/PDA-upt-sem5-Projects

# Option B: if you already cloned without --recurse-submodules
git submodule update --init --recursive
```

## Adding your own submodule (for teammates)

Each person owns a separate repo for their technology. To link yours into this superproject:

1. **Create an empty repo on GitHub** for your work (no README/license — keep it empty to avoid merge conflicts), e.g. `PDA-upt-sem5-OpenMP`.

2. **Add it as a submodule** from the root of this superproject. Use the folder name that matches your technology (`OpenMP`, `MPI`, `Pthreads`):

   ```bash
   git submodule add https://github.com/<you>/PDA-upt-sem5-OpenMP OpenMP
   ```

   > ⚠️ Use `git submodule add`, **not** `git clone`. A plain `git clone` creates a nested repo that the superproject does not track, and no `.gitmodules` entry is created. If you already cloned by mistake, just run the same `git submodule add <url> <folder>` command over the existing folder — git will adopt it.

3. **Add your work inside the submodule folder** and push it to *your* repo:

   ```bash
   cd OpenMP
   # ... add your files ...
   git add .
   git commit -m "Initial OpenMP work"
   git push -u origin main
   cd ..
   ```

4. **Commit the submodule pointer** in this superproject and push:

   ```bash
   git add .gitmodules OpenMP
   git commit -m "Add OpenMP submodule"
   git push
   ```

## Working day-to-day

- **Inside your submodule folder** (`CUDA/`, `OpenMP/`, ...): commit and push as normal to your own repo.
- **After pushing new commits in a submodule**, update the pointer in the superproject so teammates get your latest commit:

  ```bash
  git add <YourFolder>
  git commit -m "Bump <YourFolder> submodule"
  git push
  ```

- **To pull everyone's latest submodule commits:**

  ```bash
  git pull
  git submodule update --init --recursive
  ```
