# Copilot Instructions

## Repository purpose and architecture

- This is a Git-backed library of AI-generated media. Top-level, topic-named directories contain the deliverable assets, primarily MP4 files, with related images, audio, and occasional After Effects projects.
- `index.html` is the only application source. It is a dependency-free static page intended for GitHub Pages. On load, its inline JavaScript lists top-level repository directories through the GitHub Contents API, loads the selected directory's direct child `.mp4` files, and renders GitHub Pages links and native video players in a responsive grid. `chogo` is the default selection.
- `sora-data-files-export-{1,2,3}/generations.json` are exported Sora metadata. Each is a single JSON array whose records use `id`, `task_id`, `width`, `height`, `title`, `prompt`, and `url`. Preserve the source order and record values when editing or importing these exports.

## Commands

There is no package manifest, build step, linter, or automated test suite. Consequently, there is no single-test command.

- Preview the static page locally: `python3 -m http.server 8000`
- Then open `http://localhost:8000/`. The GitHub API requests still target the configured remote repository and the selected project directory.
- Validate a metadata export after editing: `python3 -m json.tool sora-data-files-export-1/generations.json >/dev/null`

## Repository conventions

- Keep asset files organized by their existing topic/project directories. Do not move or rename media casually: `index.html` constructs public URLs directly from each GitHub API `file.path`.
- For changes to the browser index, retain its dependency-free inline HTML/CSS/JavaScript structure unless the task explicitly introduces a build tool. Update `GITHUB_USER`, `GITHUB_REPO`, `GITHUB_BRANCH`, and `REPOSITORY_API_URL` together when changing the published repository or branch. Change `DEFAULT_FOLDER` to select a different initial project directory.
- The index intentionally lists only direct `.mp4` children of the configured directory; it does not recurse or show other formats.
- `.gitattributes` normalizes text files with LF. `.gitignore` excludes macOS `.DS_Store` files, but existing tracked copies remain part of the repository; do not bulk-remove media or project files as incidental cleanup.
