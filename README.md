# vesign-proof

This repository is a public, tamper-evident record of when [Vesign](https://ve-sign.com)
generated its trading signals.

## What's in here

Every entry in this repo is a single SHA-256 hash, computed from a snapshot of
that day's signals at the moment they were generated — nothing more. The
snapshots themselves are **not** published here. They are created, hashed,
and archived privately at generation time; only the hash is committed to
this public repo, immediately, the same day.

Because this repo is on GitHub, every commit carries a public, third-party
timestamp that Vesign does not control and cannot backdate. That gives
anyone a way to verify, after the fact, that a given day's signals existed
no later than the date of the corresponding commit — without Vesign having
to reveal any signal content, methodology, or performance data before it
chooses to.

## File layout

```
YYYY/YYYY-MM-DD.sha256          — one per trading day
genesis-through-YYYY-MM-DD.sha256  — one-time baseline covering all signal
                                     history that existed as of that date
```

Each `.sha256` file contains exactly one line: the 64-character lowercase
hex SHA-256 digest, followed by a newline. Nothing else.

## What will happen at launch

At product launch, Vesign will publish the underlying daily snapshot files
that these hashes were computed from. At that point, anyone will be able to
independently confirm that a snapshot matches its hash — and therefore that
it existed at (or before) the time of that day's commit here.

## How to verify a published snapshot against its hash

Once a snapshot file (e.g. `2026-07-16.json`) is published:

1. Compute its SHA-256 digest:
   ```bash
   shasum -a 256 2026-07-16.json
   # or: sha256sum 2026-07-16.json
   ```
2. Compare the resulting hex digest to the contents of the matching file in
   this repo (e.g. `2026/2026-07-16.sha256`).
3. If they match, the snapshot is exactly what was hashed and committed on
   that date — byte for byte, nothing added or removed since.

The snapshot files are canonical JSON (UTF-8, sorted object keys, no
whitespace between tokens) so that hashing is unambiguous and anyone can
reproduce the same hash from the same data independently.

## What this repo is *not*

This repo contains no information about Vesign's model, methodology,
performance, or signal contents. It is purely a cryptographic timestamp
mechanism — a hash is all that is ever committed here before launch.
