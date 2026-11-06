# cppunit mirror

This repository automatically mirrors <https://git.libreoffice.org/cppunit> to
GitHub. The upstream source is on the [`master`](../../tree/master) branch.

The `main` branch contains only the mirror automation. Keep it as the GitHub
default branch: scheduled GitHub Actions workflows run from the default branch.

The workflow runs hourly at minute 17 (UTC), on changes to `main`, and manually
from the **Actions → Mirror LibreOffice cppunit → Run workflow** menu. It uses
the built-in `GITHUB_TOKEN` with `contents: write`; no extra secret is needed.

All upstream branches and tags are copied exactly, including force updates and
deletions. GitHub-only branches and tags are deleted, except for `main`. Do not
make downstream source changes here. Gerrit review refs and other internal refs
are not mirrored.

If upstream introduces a `main` branch, the sync stops with an error to protect
the automation. Move the automation to a different reserved branch, update the
workflow, and change the GitHub default branch before resuming.

Repository or organization rules must allow GitHub Actions and the mirror's
branch/tag updates. GitHub may disable scheduled workflows in public repositories
after 60 days without repository activity; re-enable the workflow in Actions if
that happens. Failed runs are visible in Actions and use GitHub's normal workflow
notification settings.
