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
Dockerfile, including newer Kubernetes minor releases. etcd, yq and mimirtool
downloads are also tracked through annotated version variables. kubectl, etcd,
Go, Grafana, Mimir and nginx workflow tags are derived from their Dockerfiles.

All ten image workflows build matching pull requests without registry login,
publishing or signing. Publishing runs on matching pushes to `main`, existing
tag triggers and monthly rebuilds on the default branch. Published builds pull
base images and disable the layer cache so floating downloads and unpinned
packages are refreshed. Signing requires the existing `COSIGN_KEY` secret.

### Image inventory

| Image | Versioned dependencies tracked by Renovate | Dependencies resolved during rebuild |
| --- | --- | --- |
| busybox | None with the current floating tag | `busybox:latest` |
| etcd-tools | Ubuntu base image, etcd release | APT packages |
| golang | Go base image, yq release | APK packages, stable kubectl, Helm 3, Kustomize |
| grafana | Grafana base image | Grafana plugins and plugin updates |
| kubectl | kubectl release | Alpine base, APK packages, Helm 3 |
| mimir | Mimir and mimirtool base images | BusyBox `uclibc` base |
| nginx-non-root | nginx base image | APK packages |
| s3cmd | None with the current floating tag | Python Alpine base, APK packages, pip s3cmd, stable kubectl |
| socat | None with the current floating tag | Alpine base, APK socat |
| utils | yq and mimirtool releases | Alpine base, APK packages, stable kubectl, Helm 3, Kustomize, Crossplane, vcluster, MinIO mc |

The workflows themselves are tracked by Renovate's GitHub Actions manager.
Direct binary downloads use BuildKit's `TARGETARCH` for amd64/arm64 builds.
Floating dependencies still have no reviewable version diff; pinning them is
separate work from enabling rebuilds and tracking existing version pins.

### Remaining download issue

On 2026-11-02, requests from the investigation environment to the MinIO mc binary
URLs returned HTTP 410 for both `linux-amd64` and `linux-arm64`. Whether GitHub
Actions sees the same response is not yet verified. No replacement source has
been selected or verified in this rollout.

### References

- [Renovate Dockerfile version annotations](https://docs.renovatebot.com/presets-customManagers/#custommanagersdockerfileversions)
- [Docker target-platform arguments](https://docs.docker.com/build/building/variables/#multi-platform-build-arguments)
- [Build action v5 inputs](https://github.com/docker/build-push-action/tree/v5#inputs)
- [GitHub schedule events](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows#schedule)
