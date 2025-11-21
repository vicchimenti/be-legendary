# Branching & Tagging Workflow for Be Legendary Vue App

This document defines the standard workflow for managing updates, releases, and backups for the **Be Legendary** single-page Vue app hosted in TerminalFour (T4).

---

## 1. Production Release Tag

When you deploy a version to T4, tag the commit as a release:

```bash
git checkout main
git pull origin main
git tag -a v1.1-2025-11-20 -m "Be Legendary – Skubal update + path fix"
git push origin v1.1-2025-11-20
```

✅ **Purpose:** This marks the version that is live in production. You can always restore or diff this tag to recreate the current deployed build.

---

## 2. Backup Tag (Pre-Development Snapshot)

Before starting any new work or maintenance cycle, create a backup tag:

```bash
git tag -a v1.1.1-backup -m "Backup before new working branch creation"
git push origin v1.1.1-backup
```

✅ **Purpose:** Serves as a restore point to roll back quickly if needed. It captures the clean state after the last successful deployment.

---

## 3. Create a New Maintenance Branch

After tagging the backup, create a new branch for ongoing updates (e.g., marketing content, images, or video changes):

```bash
git checkout -b su-maintenance-2025-12
git push -u origin su-maintenance-2025-12
```

✅ **Purpose:** Isolates upcoming updates from the production-ready `main` branch.

---

## 4. Active Development Flow

1. **Pull latest** from `main` if needed.
2. Make your edits in `src/` (e.g., update text, images, or video references).
3. Test locally:
   ```bash
   npm run dev
   ```
4. Build for T4 deployment:
   ```bash
   VITE_BASE=/media/seattle-university/be-legendary/ npm run build
   ```
5. Upload `/dist/assets/` and `index.html` output to T4 Media Library.

---

## 5. Tag the New Release After Deployment

Once the updated app is live and verified in T4:

```bash
git checkout main
git merge su-maintenance-2025-12
git push origin main
git tag -a v1.2-2025-12-XX -m "Be Legendary – December content update"
git push origin v1.2-2025-12-XX
```

✅ **Purpose:** Promotes the maintenance branch into production and preserves an immutable record of what was deployed.

---

## 6. Summary Diagram

```
main ────●─────●────────●───────────────▶
          v1.1  v1.1.1-backup  v1.2 (live)
                       \
                        \── su-maintenance-2025-12
```

---

## 7. Best Practices

- Always **commit and push** before building for T4.
- Keep one **active maintenance branch** at a time.
- Delete old maintenance branches after merging and tagging.
- Store all build artifacts under OneDrive:
  ```
  C:\Users\Victo\OneDrive - Seattle University\Marcom\Be Legendary\Releases\vX.X-YYYY-MM-DD
  ```

---

## 8. Quick Commands Reference

```bash
# Create a new backup tag
git tag -a v1.1.1-backup -m "Backup before new working branch creation"
git push origin v1.1.1-backup

# Create and push a new maintenance branch
git checkout -b su-maintenance-2025-12
git push -u origin su-maintenance-2025-12

# Build for T4 with correct base path
VITE_BASE=/media/seattle-university/be-legendary/ npm run build

# Merge maintenance branch and tag new release
git checkout main
git merge su-maintenance-2025-12
git push origin main
git tag -a v1.2-2025-12-XX -m "Be Legendary – December content update"
git push origin v1.2-2025-12-XX
```

---

**Maintainer:** Victor Chimenti  
**Last Updated:** November 20, 2025

