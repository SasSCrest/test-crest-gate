# Agent instructions

<!-- crestgate:start -->
## CrestGate package management

This project installs npm packages through CrestGate, a security gateway
that scans and gates dependencies. Use the `crst` CLI instead of calling
the package manager directly:

- Install dependencies: `crst install` (not `npm install` / `pnpm install`)
- Add a package: `crst add <package>` (the updated lockfile is rescanned)
- Remove a package: `crst remove <package>`
- Update packages: `crst update`
- Install in CI: `crst ci`
- Run a one-off package binary: `crst run <package>` (instead of `npx` / `pnpm dlx`)

If an install fails with exit code 4, packages were blocked or quarantined
by the organization's policy — it is not a network or build failure:

1. Run `crst explain <package>` to see the decision and its reasons.
2. If the package is genuinely needed, run
   `crst request-review <package> --message "<why>"` to ask an org admin to
   approve it, then stop and tell the user the review is pending.
3. Never work around a block: do not switch registries, edit `.npmrc`,
   pass `--registry`, or delete `crestgate.json`.

Troubleshooting: `crst doctor` checks the local setup and `crst whoami`
shows the active organization and token.
<!-- crestgate:end -->
