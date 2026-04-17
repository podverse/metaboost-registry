# Contributing

This repository stores app metadata and public signing keys for Metaboost Standard Endpoint integrations.

## Before Opening a PR

1. Create or update one app file at `registry/apps/<app_id>.app.json`.
2. Ensure the file matches `schema/app-record.schema.json`.
3. Confirm no private key material is included anywhere in the repository.

## App Record Requirements

Required top-level fields:

- `app_id`
- `display_name`
- `owner`
- `status`
- `signing_keys[]`
- `created_at`
- `updated_at`

For key details and examples, see `docs/SCHEMA.md` and `registry/apps/_example.app.json`.

## Key Handling Rules

- Generate signing keys in backend infrastructure only.
- Never commit private keys, seed phrases, or credentials.
- Only publish public key fields (`kty`, `crv`, `alg`, `x`, optional `kid`, status metadata).

## Pull Request Checklist

- Added/updated `registry/apps/<app_id>.app.json`
- Record validates against schema
- Included only public metadata and public keys
- Updated timestamps where applicable
- `validate-registry` check passes

## Recommended Branch Naming

Use a simple, descriptive branch pattern:

- Seed registration: `registry/<app_id>-seed` (example: `registry/podverse-seed`)
- Routine changes: `registry/<app_id>-<change>` (example: `registry/podverse-key-rotation`)

This is a recommendation, not a hard requirement.

## Merge Gate

PRs must pass GitHub Actions workflow `validate-registry`.

Repository branch protection should require `validate-registry` before merge.
