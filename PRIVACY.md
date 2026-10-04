# Privacy notice — Turn Off AI Data Sharing

Last updated October 3, 2026.

Turn Off AI Data Sharing is a package of instructions and reference text. It has no publisher-operated service, account, telemetry, or storage. The publisher does not receive or retain audit content through this plugin.

## No code, no sign-in details, no network of its own

The package contains markdown and two JSON manifests. It bundles no MCP servers, hooks, agents, scripts, or `npx`/`uvx` launchers, and it contains no executable code. It does not read environment variables, configuration files, OS stored-login areas, or any other sign-in detail store, and it has no endpoint of its own to send anything to.

The reference files quote other vendors' settings, command names, and environment-variable names as documentation of those products. Those are descriptions of third-party software for the reader, not instructions the package executes.

### Vocabulary in the reference files

The subject of this package is account access and permission exposure in other companies' products. Describing that subject accurately means naming what each vendor's settings control.

The reference text is written to avoid wording that could be mistaken for an instruction to read a stored sign-in value from a machine. Where a vendor's own documentation makes a point about account access, it is summarised in this package's words and attributed, rather than reproduced. Literal identifiers that appear in code spans — OAuth scope names, setting keys, environment-variable names, URLs — are left exactly as the vendor publishes them, because an audit that renamed a control would send the reader to the wrong place.

Nothing in this package reads a stored sign-in value. There is no code that could: the plugin is markdown files, two JSON manifests, an icon, and a license, with no scripts, hooks, MCP servers, or network calls of its own. The https links in `plugin.json` are the listing's homepage, repository, documentation, support, and privacy-policy URLs.

## Data used in an audit

The skill asks Claude to read the vendor reference files bundled in this repository. When the user asks for a live read, it additionally asks Claude to open that user's own AI account settings pages in a browser the user is already signed into, using browser tooling the user has already installed and permitted, and to record the state of named settings.

Those pages may show personal data, including account email addresses, workspace names, and the names of connected third-party accounts. The skill instructs Claude to mask those by default in any report it produces.

Claude, the audited vendors, and any browser tooling the user has installed may process requests or content according to their own terms, permissions, and retention settings. Requests to a vendor's settings pages expose the requested URL and normal request metadata to that vendor, under the user's own authenticated session.

## What it will not do

The skill instructs Claude to treat the audit as read-only: to report and recommend, and never to change a setting, revoke a connector, delete a conversation, submit an objection form, or accept a consent dialog. It instructs Claude never to request, accept, or use another person's sign-in details, and to run only for the account owner or alongside them.

A report is written to the user's machine only when the user asks for one, at a path the user chooses. The repository's `reports/` directory is excluded from version control, and no real account data is committed to this repository.

These are instructions; the host's enabled tools and permissions determine what actions are technically possible. Users who need strict read-only access should configure it in their Claude environment and in any browser tooling they have installed.

For questions about this package, use the [repository issue tracker](https://github.com/RachaelQuisel/turn-off-ai-data-sharing/issues). For Claude or vendor data controls, use those providers' privacy settings and policies.
