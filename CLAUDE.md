# Caelestia CLI — personal fork

This is **RobbeDelporte/cli**, a fork of `caelestia-dots/cli` — the Python CLI
that drives shell IPC, wallpaper/scheme management, screenshots, etc.

Location: `~/.local/share/caelestia-cli`. A shim at `~/.local/bin/caelestia`
execs `bin/caelestia` from this repo, and since `~/.local/bin` precedes
`/usr/bin` in `$PATH`, it **overrides the AUR `caelestia-cli`**.

Verify with: `which caelestia` → should print `/home/robbe/.local/bin/caelestia`.

## Remotes

- `origin`   → `https://github.com/RobbeDelporte/cli.git`
- `upstream` → `https://github.com/caelestia-dots/cli.git`

## Workflow

1. Branch off `main`:
   ```sh
   git checkout main && git pull upstream main
   git checkout -b <topic>
   ```
2. Edit Python under `src/caelestia/`. No build step — the wrapper re-runs
   `python -m caelestia` every invocation, so changes are picked up immediately.
3. Commit → push to `origin`.
4. Sync upstream: `git fetch upstream && git merge upstream/main`.
5. PR back with `gh pr create` against `caelestia-dots/cli:main`.

## Layout hints

- `src/caelestia/__main__.py` — argparse entry
- `src/caelestia/commands/`  — one module per subcommand
- `src/caelestia/utils/`     — shared helpers (IPC, paths, schemes)
- `bin/caelestia`            — thin shell wrapper (`cd src && python -m caelestia`)

## Do not

- Do not edit `/usr/bin/caelestia` or `/usr/lib/python*/site-packages/caelestia/`
  — those belong to the AUR package.
- Do not push to `upstream`.
