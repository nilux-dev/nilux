# Security

## Reporting a vulnerability

Please do not open a public issue for a security problem — that tells everyone about it at the same
time as us.

Email **security@nilux.dev** with what you found, how to reproduce it, and what an attacker could
do with it. If you have a proof of concept, include it; if you only have a suspicion, send that too
— a false alarm costs us ten minutes.

You will get an acknowledgement within 48 hours and an assessment within a week. We will tell you
what we found, whether we agree it is exploitable, and when a fix ships. If you would like credit
once it is fixed, say so and we will name you.

## What is in scope

- The `@nilux-ai/code` CLI client — anything it does on your machine that it should not.
- The Nilux desktop app for Mac — the same, for the app and its updates.
- The API at `api.nilux.dev` — authentication, authorisation, data belonging to other accounts.
- The website and dashboard at `nilux.dev`.

## What is not

- Reports produced by an automated scanner with no demonstrated impact.
- Missing headers or configuration that cannot be turned into an actual attack.
- Denial of service through sheer volume.
- Social engineering of anyone involved in the project.

## Testing

Test against your own account only. Do not attempt to reach another account's data, degrade the
service for other users, or run destructive operations against production. If a test needs any of
those to prove a point, write to us first and we will arrange it.
