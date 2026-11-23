# Windows app updates

This directory is the release staging repo for `samplies/apps-and-vershons`. The six desktop apps check the stable JSON feed at `https://raw.githubusercontent.com/samplies/apps-and-vershons/main/apps-update.json` when they start.

`apps-update.json` maps each Windows app ID to its version, HTTPS setup URL, release tag, file size, and SHA-256. Setup EXEs are staged under `release-assets/<release-tag>/` and uploaded as GitHub Release assets. The feed is committed to the repository after the referenced versioned assets are published, so clients never see a new version before its setup is available.

Do not commit EXEs to Git history. To publish later builds, run `python apps/store_installer/build_release.py --write-update-feed`, authenticate a GitHub account with write access using `gh auth login`, then run `python apps/store_installer/publish_github_updates.py`. The publisher checks the repository is public, validates every size and SHA-256, refuses to replace an existing versioned asset, and pushes the updated feed after assets are present.

The feed includes the six rebuilt desktop apps plus Server Manager and Sam's Server setup EXEs.
