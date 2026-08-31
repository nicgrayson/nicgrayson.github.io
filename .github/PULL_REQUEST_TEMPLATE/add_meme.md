---
about: Contribute a meme to the gallery at /images
title: "Add meme: [file name]"
---

## Add a meme

Thanks for contributing! To add a new meme to the gallery:

1. **Put your image file in `/images`** on your branch. Supported formats:
   `.jpg`, `.jpeg`, `.png`, `.gif`. Keep file sizes reasonable (GitHub has a
   100 MB per-file limit; we removed a stray archive because of this).
2. Add a one-line entry for it in **`/_data/images.yml`**:
   ```yaml
     - name: "your-file.jpg"
   ```
3. Optionally preview locally: `bundle exec jekyll serve`, then open
   `http://localhost:4000/memes/`.

The site builds automatically on push to `main` and deploys to GitHub Pages.

### Describe your meme

<!-- What is this meme / why does it belong in the gallery? -->
