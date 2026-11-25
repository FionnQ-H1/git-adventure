# Workshop Instructions

Follow along with the screen at the front. Wherever you see `your-username`, put your own GitHub username instead.

If you get stuck, put your hand up and a helper will come over.

---

## Before you start

### 1. Accept the invite

Go to the repo's invitations page (the link is on the screen) and click **Accept invitation**. You can't push (upload) anything until you do this.

### 2. Tell Git who you are

You only do this once per laptop. Open a terminal (Command Prompt / PowerShell on Windows, Terminal on Mac) and type:

```bash
git config --global user.name "Your Name"
git config --global user.email "the-email-you-use-on-github@example.com"
```

### 3. Clone the repo

**Clone** means download a copy of the repo that stays connected to GitHub.

```bash
git clone https://github.com/FionnQ-H1/git-adventure.git
cd git-adventure
```

`cd` (change directory) moves you into the folder you just downloaded.

> **Laptop not cooperating?** Use the browser backup instead. On the repo page, click the green **Code** button, then the **Codespaces** tab, then **Create codespace on main**. A code editor opens in your browser with a terminal at the bottom. Skip steps 2 and 3 and carry on from Round 1.

---

## Round 1: Write your own scene

Everyone writes a different file in this round, so there are no conflicts yet.

### 1. Make a branch

A **branch** is your own copy of the project to work on, so you don't change anyone else's work.

```bash
git switch -c your-username-scene
```

`-c` means create a new branch and switch to it.

### 2. Write your scene

1. Open the `git-adventure` folder in your code editor. In VS Code: **File → Open Folder**.
2. Copy `scenes/TEMPLATE.md`: right-click it, **Copy**, then right-click the `scenes` folder and **Paste**.
3. Rename the copy with your username at the front, so nobody else picks the same name. For example: `scenes/your-username-the-printer.md`.
4. Write what happens. Give it at least two choices. Choices can point to scenes that don't exist yet.

### 3. Commit

A **commit** is a saved snapshot of your changes with a short message saying what you did.

```bash
git add scenes/your-username-the-printer.md
git commit -m "Add the printer scene"
```

`git add` picks which files go into the snapshot. `git commit` saves it.

### 4. Push

**Push** means upload your commits to GitHub.

```bash
git push -u origin your-username-scene
```

`-u origin your-username-scene` tells Git where this branch lives on GitHub. You only need it the first time you push a new branch.

> **Asked for a password?** Your normal GitHub password won't work here. Switch to the Codespace (see "Laptop not cooperating?" above) and redo Round 1 there.

### 5. Open a Pull Request

A **Pull Request** (PR) is you asking for your branch to be added into `main`.

1. Go to the repo on GitHub. A yellow bar says your branch had recent pushes. Click **Compare & pull request**.
2. Give it a title, e.g. "Add the printer scene".
3. Click **Create pull request**.
4. Click **Merge pull request**, then **Confirm merge**.

---

## Round 2: Link your scene into the story

Nothing in the story points to your scene yet. In this round you add a choice that leads to it.

### 1. Get the latest version of main

Everyone else's scenes are on GitHub now, but not on your laptop.

```bash
git switch main
git pull
```

`git pull` downloads the newest commits from GitHub.

### 2. Make a new branch

```bash
git switch -c your-username-link
```

### 3. Add a choice

1. Open any existing scene: `start.md`, or one of the files in `scenes/`.
2. Under **What do you do?**, add a line pointing to your scene. In a file inside `scenes/`:
   ```
   - [Run to the printer](your-username-the-printer.md)
   ```
   In `start.md`, the link needs `scenes/` in front:
   ```
   - [Run to the printer](scenes/your-username-the-printer.md)
   ```

### 4. Commit, push, open a PR

```bash
git add .
git commit -m "Link the printer scene"
git push -u origin your-username-link
```

`git add .` adds every file you changed. The `.` means "everything in this folder".

Then open and merge a Pull Request the same way as Round 1.

> **GitHub says "This branch has conflicts that must be resolved"?** Someone else edited the same lines before you. Go to **Fixing a merge conflict** at the bottom of this page.

---

## Round 3: Chaos

At the top of `start.md` there's a line:

```
Your name is: Alex
```

Everyone is going to change that exact line at the same time.

### 1. Get the latest main and make a branch

```bash
git switch main
git pull
git switch -c your-username-hero
```

### 2. Change the name

Open `start.md` and change `Alex` to any name you want.

### 3. Commit and push

```bash
git add start.md
git commit -m "Rename the hero"
git push -u origin your-username-hero
```

### 4. Open a Pull Request, but DON'T merge yet

Open the PR, then wait. One PR gets merged on the screen. After that, every other PR shows a **conflict**, because two people changed the same line and Git can't decide which one to keep. Fix yours with the steps below.

---

## Fixing a merge conflict

A **merge conflict** happens when two branches change the same line and Git needs a person to choose.

### 1. Bring the latest main into your branch

Stay on your own branch and run:

```bash
git fetch origin
git merge origin/main
```

`git fetch` downloads what's new on GitHub without changing your files. `git merge origin/main` tries to combine GitHub's `main` with your branch.

Git will say:

```
CONFLICT (content): Merge conflict in start.md
```

### 2. Open the file

You'll see something like this:

```
<<<<<<< HEAD
Your name is: Sparky
=======
Your name is: Gandalf
>>>>>>> origin/main
```

- Between `<<<<<<< HEAD` and `=======` is **your** version.
- Between `=======` and `>>>>>>> origin/main` is **the version already on main**.

### 3. Choose

Delete the marker lines (`<<<<<<<`, `=======`, `>>>>>>>`) and leave the line the way you want it. You can keep yours, keep theirs, or combine them:

```
Your name is: Sparky the Gandalf
```

Save the file.

### 4. Finish the merge

```bash
git add start.md
git commit -m "Fix merge conflict in start.md"
git push
```

Go back to your Pull Request. The conflict warning is gone, so you can click **Merge pull request**.

---

## Command cheat sheet

| What you want to do | Command |
|---|---|
| Download a repo | `git clone URL` |
| Make a new branch and switch to it | `git switch -c branch-name` |
| Switch to an existing branch | `git switch branch-name` |
| See what you've changed | `git status` |
| Pick files for the snapshot | `git add file-name` (or `git add .` for everything) |
| Save the snapshot | `git commit -m "message"` |
| Upload a new branch | `git push -u origin branch-name` |
| Upload more commits to it | `git push` |
| Download the newest commits | `git pull` |
| Bring main into your branch | `git fetch origin` then `git merge origin/main` |