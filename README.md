# Windows app updates

This directory stages the public GitHub Releases feed and versioned setup EXEs for `samplies/apps-and-vershons`. The six desktop apps check the stable URL `https://github.com/samplies/apps-and-vershons/releases/download/apps-update/apps-update.json` at startup.

`apps-update.json` maps each app ID to its version, HTTPS setup URL, release tag, file size, and SHA-256. Setup EXEs are staged under `release-assets/<release-tag>/`. The publisher validates the manifest, executable signatures, sizes, and SHA-256 before creating versioned GitHub Releases. It updates the `apps-update` release after all versioned assets are present.

Do not commit the EXEs to Git history. They are GitHub Release assets. To publish a later build, run `python apps/store_installer/build_release.py --write-update-feed`, authenticate with `gh auth login`, then run `python apps/store_installer/publish_github_updates.py`. The publisher refuses non-public repositories and never replaces an existing versioned asset.

The current feed also includes the Server Manager and Sam's Server setup EXEs.
