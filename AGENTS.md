# Fork Rules (rophy/guacamole-server)

This is a fork of apache/guacamole-server with custom patches.

## Branch Strategy

- **`main`**: Tracks upstream `apache/guacamole-server` main. Do not commit directly.
- **`develop`**: Based on `main`. Contains common changes shared across releases (CI workflows, AI rules, configs). Cherry-pick or merge into `releases/*` branches.
- **`releases/<version>`**: Based on an upstream tag (e.g. `releases/1.6.0` from tag `1.6.0`). Includes changes from `develop` plus version-specific patches.

## Tagging

- Upstream tags are semver (e.g. `1.6.0`).
- Fork tags append datetime: `<version>-YYYYMMDD-<seq>` (e.g. `1.6.0-20260820-1`). The sequence number (`-1`, `-2`, ...) disambiguates multiple tags on the same day.

## Rules

- All changes to `develop` and `releases/*` must go through a PR from a feature branch.
- No `git push` without explicit user instruction.
- Source code changes (C, build scripts) require re-running unit tests (`make check` inside Docker) before pushing.

## Running Unit Tests

```sh
docker build --target guacamole-server -t guacd-test-runner .
docker run --rm guacd-test-runner sh -c 'cd /tmp/guacamole-server && make check'
```
