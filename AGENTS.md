# Maintaining the public Leaf Arcade skill

This repository distributes skill instructions and metadata. Keep private CLI
source, game assets, credentials and local session data out of it.

When publishing a meaningful skill update, update the README, confirm the
required CLI version is published on npm, and publish a GitHub Release at the
matching `vX.Y.Z` tag on the updated commit. Describe the skill changes and minimum
CLI version. Keep install examples on `@latest`. CLI-only changes and minor
README corrections do not require a new skill release. Do not move existing tags.

The npm package bundles the same skill. Compare its SKILL.md and agent metadata
with the published skill before announcing a release.
