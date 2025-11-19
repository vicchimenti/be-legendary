# SeattleU Be Legendary – Post-Handoff Update Workflow

Once the Be Legendary Vue/Vite project is handed off, SeattleU Web Development will manage updates from Marketing, compile builds for T4, and maintain version control for ongoing enhancements.

---

## 🧭 Overview
Each update cycle generally follows this pattern:

1. **Pull latest vendor baseline** (if new updates exist)
2. **Add or replace assets** (images, videos, text copy)
3. **Test locally via `npm run dev`**
4. **Build production files via `npm run build`**
5. **Upload compiled output (`/dist/`) to TerminalFour**

---

## 🖼️ 1. Replacing or Adding Images
**Scenario:** Marketing sends new hero or campaign photos.

**Steps:**
1. Add new files to the `/assets/` directory (use lowercase, hyphenated, descriptive names).
   ```
   /assets/hero-video-placeholder-2025-03.mp4
   /assets/rally-cry-group-01.jpg
   ```
2. Update the image references in the appropriate Vue component, such as `App.vue` or `HeroSection.vue`.
   ```html
   <img src="/assets/rally-cry-group-01.jpg" alt="Seattle University students at rally" />
   ```
3. Test locally:
   ```bash
   npm run dev
   ```
4. Commit and push:
   ```bash
   git add .
   git commit -m "Replace hero image with March 2025 update"
   ```

---

## 🎥 2. Updating Video Assets
**Scenario:** Marketing provides a new Be Legendary intro video.

**Steps:**
1. Replace the existing video file in `/assets/`.
   - If renaming, also update references in the Vue component.
2. Confirm proper attributes for accessibility and autoplay behavior:
   ```html
   <video src="/assets/hero-video-v2.mp4" muted autoplay loop playsinline></video>
   ```
3. Test locally with `npm run dev`.
4. Commit and push changes.

---

## 📰 3. Updating Text or Rally Copy
**Scenario:** Marketing updates rally lines or campaign messaging.

**Steps:**
1. Open the relevant file (often `App.vue` or a sub-component).
2. Edit text content:
   ```html
   <p class="rally-line">Be unstoppable.</p>
   <p class="rally-line">Be legendary.</p>
   ```
3. Test and verify layout integrity.
4. Commit and push.

> **Tip:** Consider moving frequently edited text blocks into a JSON configuration later for easier updates.

---

## 🧩 4. Compiling & Deploying to T4

Once verified locally:

1. Run the build command:
   ```bash
   npm run build
   ```

2. Locate the compiled assets in `/dist/`:
   ```
   dist/assets/index-xxxx.js
   dist/assets/index-xxxx.css
   ```

3. Upload to the TerminalFour Media Library:
   ```
   /media/site-assets/js/be-legendary/
   /media/site-assets/css/be-legendary/
   ```

4. Update the T4 layout or Media Library HTML snippet with the new hashed filenames if necessary.

5. Upload any new `/assets/` media (images/videos) into their corresponding T4 folders.

---

## 🧱 5. Best Practices

| Category | Recommendation |
|-----------|----------------|
| **Branching** | Keep `main` for vendor source of truth. Use a working branch (e.g., `su-maintenance-2025-11`) for internal updates. |
| **Versioning** | Use descriptive commit messages: `Update March rally video and new hero image`. |
| **Media Naming** | Add version/date suffixes to prevent cache conflicts (`hero-video-v3.mp4`). |
| **Testing** | Always test both `npm run dev` (local) and `npm run build` (compiled). |
| **Backup** | Save compiled monthly builds under `/builds/YYYY-MM-BeLegendary/` for rollback. |
| **Performance** | Optimize images and compress videos before uploading to T4. |

---

## 🧩 Optional Enhancements (Future)
- Add a **T4 build script** that auto-copies compiled assets into a deploy-ready folder.
- Add **linting & Prettier hooks** for code consistency.
- Move text/copy into a **JSON file** for non-developer content updates.

---

### ✅ Summary
- Maintain `main` for vendor syncs.
- Use your maintenance branch for SeattleU updates.
- Replace media and text directly in `/assets/` and `src/components/`.
- Build with Vite and deploy the `/dist/` bundle into T4.
- Test every build before pushing live.

This ensures a stable, maintainable workflow between Marketing, Web Development, and T4 deployments.

