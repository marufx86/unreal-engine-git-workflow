# Unreal Engine Git Workflow Guide

A practical guide for Unreal Engine teams to avoid the most common Git mistake — accidentally overwriting your teammates' work.

Written from real team experience. Feel free to use this in your own project.

---

## The Problem

If you've ever heard *"why is my map modified? I didn't touch it"* — this guide is for you.

Unreal Engine silently marks files as "modified" in the background, even when you didn't intentionally change them. Opening a level, editing a shared material, or even just letting Unreal auto-save can dirty a `.uasset` file. When someone then does `git add .` and pushes everything, they accidentally overwrite their teammates' work — and nobody knows where the problem came from.

This guide explains why it happens and how to prevent it with a simple workflow.

---

## Who This Is For

- Small to mid-size teams working on Unreal Engine projects with Git
- Artists, level designers, and generalists who are comfortable in Unreal but less familiar with Git
- Anyone who has run into the "I didn't touch that file" problem

---

## The One Rule That Matters

> **Only push the files you actually worked on.**

Not everything that shows up as modified. Just the stuff *you* intentionally changed.

---

## The Workflow — Every Session

### 1. Pull First, Always

Before you open Unreal, pull.

```bash
git pull
```

Or hit pull in GitHub Desktop / Fork before anything else.

**Why it matters:** If you start on an old version and push, you'll overwrite stuff your teammates already did. Just pull first and save everyone the headache.

---

### 2. Do Your Thing

Work on your files — your level, your materials, your assets. Try not to open other people's maps, even just to peek around.

**Why it matters:** The moment you open someone else's `.uasset` in Unreal, it gets marked as modified — even if you changed absolutely nothing. Git will pick it up and you'll accidentally push it along with your own work.

---

### 3. Check Every File Before You Commit

This is the big one. Before you hit commit, open your changes list and go through every single file.

For each file, ask: *did I actually work on this?*

If the answer is no — don't include it.

#### In GitHub Desktop
1. Open the **Changes** tab on the left.
2. You'll see checkboxes next to each file.
3. **Uncheck** anything you didn't work on.
4. Only the checked files will go into the commit.

#### In Fork
1. Go to the **Local Changes** tab at the top.
2. Everything modified shows up in the **Unstaged** section.
3. Only drag up (or click Stage on) the files you actually worked on.
4. Leave the rest unstaged — they won't be committed.
5. If you want to fully undo a file's changes, right-click it and hit **Discard Changes**.

#### In the Terminal
```bash
# See what's modified
git status

# Add only your files
git add Content/Levels/MyLevel.umap
git add Content/Materials/M_Carpet.uasset

# Never do this — it grabs everything indiscriminately
# git add .
```

---

### 4. Write a Real Commit Message

Just a short line saying what you actually did. Future you (and your teammates) will thank you.

```
✅ "Updated carpet material and adjusted lighting in Last level"
❌ "changes"
❌ "update"
❌ "push"
```

---

### 5. Push

Once you've checked everything and only staged your files — push.

```bash
git push
```

---

## Why Unreal Touches Files You Didn't Mean To

This trips up a lot of people, so here's what's actually going on:

| What happened | Why the file shows as modified |
|---|---|
| You opened someone else's level to look around | Unreal marks it modified on open |
| You changed a material that other levels reference | Those levels get flagged too |
| You accidentally moved something and undid it | Unreal still marks the file dirty |
| Unreal auto-saved or rebuilt lighting | Related files get touched in the process |

The fix is always the same — review before you commit, and only stage what you worked on.

---

## Common Mistakes to Avoid

| ❌ Don't | ✅ Do instead |
|---|---|
| `git add .` | Stage only your specific files |
| Push without checking the changes list | Always review every file first |
| Open teammates' maps out of curiosity | Stay in your own level |
| Push first and ask questions later | Check first, then push |
| Ignore files you don't recognise in the list | Don't push them — investigate first |

---

## Pre-Push Checklist

Run through this before every push:

- [ ] Pulled before I started working
- [ ] Only opened files I was assigned to work on
- [ ] Reviewed every file in the changes list
- [ ] Staged only the files I actually changed
- [ ] Wrote a clear, descriptive commit message
- [ ] Nothing from a teammate's map snuck in

---

## Contributing

Found something wrong or missing? PRs and issues are welcome. This guide is meant to grow with real-world experience.

---

## License

MIT — use it, share it, adapt it for your team.
