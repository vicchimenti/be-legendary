# SeattleU Be Legendary – Git Maintenance Cheat Sheet

This workflow keeps your local Be Legendary Vue/Vite repo clean and safely in sync with vendor updates while preparing assets for T4.

---

## 🏁 Setup (One-Time)
Create a maintenance branch for SeattleU work based on the latest vendor `main` branch:

```bash
git checkout -b su-maintenance-2025-11
```

---

## ↺ When Vendor Pushes a New Update
Pull the latest vendor changes, then merge them into your local maintenance branch:

```bash
git checkout main
git pull origin main
git checkout su-maintenance-2025-11
git merge main
```

This syncs your local branch with vendor updates while keeping your changes intact.

---

## 🧠 When Making SeattleU Edits
Commit small, logical changes to your maintenance branch (for T4 prep, testing, or asset syncs):

```bash
git add .
git commit -m "Local T4 prep, asset sync, or testing updates"
```

Keep `main` clean — it remains your vendor baseline.

---

## 🚀 Optional – Push Maintenance Branch to GitHub
Push your maintenance branch so it’s backed up remotely or ready for review:

```bash
git push origin su-maintenance-2025-11
```

---

## 🧹 If Vendor Handoffs Are Complete
Once the vendor is finished, merge your final maintenance branch back into `main`:

```bash
git checkout main
git merge su-maintenance-2025-11
git push origin main
```

This establishes SeattleU’s branch as the ongoing source of truth for future updates.

---

### Notes
- Always pull vendor changes **into `main` first** before merging to your branch.
- Never edit vendor files directly in `main`.
- Commit early and often when testing or syncing media assets.
- You can safely delete old sync branches once merged.