---
name: Add a meme
about: Request to add a new meme to the gallery at /memes
title: "Add meme: [file name]"
labels: enhancement
assignees: nicgrayson
---

## Add a meme

Pick one of these ways to get your meme into the gallery at `/memes`:

### Option A — you make the change (opens a PR)

1. Fork the repo: <https://github.com/nicgrayson/nicgrayson.github.io/fork>
2. Put your image file (`.jpg`, `.jpeg`, `.png`, or `.gif`) in `/images`
3. Add a one-line entry to **`/_data/images.yml`**:
   ```yaml
     - name: "your-file.jpg"
   ```
4. Open a pull request back to `main`. The repo's PR template explains the
   steps, and it auto-deploys to GitHub Pages on merge.

### Option B — just ask

If you'd rather not mess with git, attach the image to this issue (or link it)
and I'll add it for you. Mention where you found it / why it belongs.

### Upload limits

Keep files under ~50 MB. Note we removed a stray 74 MB archive from the repo
because GitHub flags large files.

---

**Describe your meme:** <!-- what is it / why does it belong in the gallery? -->
