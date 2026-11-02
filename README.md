# docker-images

a bunch of docker images for general pupose

NOTE 2026/01/27: MTR will disconnect at the end of the year. For this reason we push no longer updates to this registry.

## Dependency updates

Renovate uses the [shared update policy](https://github.com/eumel8/renovate-config):
Monday mornings (Europe/Berlin), at most three open regular PRs, no auto-merge,
and major upgrades requested through the Dependency Dashboard.
Non-major image and downloaded-tool updates are grouped per image directory;
GitHub Actions updates have their own group.

Install the Renovate GitHub App for this repository and merge the shared preset
before merging the onboarding PR. Renovate replaces Dependabot version updates;
GitHub vulnerability alerts and Dependabot security updates are separate settings.
Existing Dependabot PRs are not automatically closed by this migration.

The kubectl download is tracked through the annotated `KUBECTL_VERSION` in its
Dockerfile. Updates stay on Kubernetes 1.36.x until `allowedVersions` in
`renovate.json` is deliberately changed. kubectl and nginx-non-root workflow tags
are derived from their Dockerfiles, and both workflows build pull requests
without publishing. Publishing runs only on pushes to `main`.

Floating base tags and unpinned APK packages still need rebuilds to pick up
changes. The Helm installer in the kubectl image currently selects Helm 3 at
build time and is not a pinned dependency managed by this initial rollout.
