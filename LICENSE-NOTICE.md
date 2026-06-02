# LICENSE-NOTICE — kinet-labs/ed25519-donna

Snapshot of [floodyberry/ed25519-donna](https://github.com/floodyberry/ed25519-donna),
Andrew Moon's portable Ed25519 reference implementation (RFC 8032).

| Field      | Value                                                    |
| ---------- | -------------------------------------------------------- |
| Upstream   | https://github.com/floodyberry/ed25519-donna             |
| Pinned     | commit `8757bd4cd209cb032853ece0ce413f122eef212c`        |
| License    | Public Domain (no LICENSE file upstream; declared in the |
|            | repository README and source headers)                    |
| SPDX       | `SPDX-License-Identifier: Unlicense` (Public Domain)     |
| Tag        | `v0.1.0-kinet-labs`                                          |

## Why a fork

kinet-labs/crypto/ed25519 consumes the upstream `ed25519.c` translation unit
directly via `#include` from a wrapper TU (`cpp/ed25519.cpp`). Pinning the
upstream commit via FetchContent keeps build reproducibility tight.

## Tag policy

* Semver tags only: `vX.Y.Z-kinet-labs` since upstream does not cut numbered
  releases — kinet-labs synthesizes a versioning surface.
* No `latest` / no `master` consumption — kinet-labs/crypto pins by tag.
* New tags are cut only after `ed25519` KATs in kinet-labs/crypto pass.

## Updating

1. `git fetch upstream master`
2. Audit the diff (upstream is rarely touched).
3. Run `ctest -R ed25519` against the candidate snapshot.
4. Tag a new `vX.Y.Z-kinet-labs` only after KATs pass.

Upstream is unmaintained Public Domain code. kinet-labs does NOT modify the
contents of this fork — kinet-specific shim headers (custom SHA-512 hook,
deterministic PRNG for batch verification) live in kinet-labs/crypto/ed25519/cpp/
and are placed earlier on the include path so they win over the upstream stubs
of the same name.
