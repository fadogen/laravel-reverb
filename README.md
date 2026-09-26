# Fadogen Reverb

The Laravel application used by Fadogen's local Reverb service. It requires PHP
8.4 or later. Composer resolves dependencies against PHP 8.4 so updates remain
compatible with the minimum supported interpreter.

This repository owns the application and its committed `composer.lock`.
Dependabot proposes dependency updates, including Laravel and the transitive
runtime packages, once a release is a week old. Major updates open individual
pull requests. Changes are validated before merging.

The packaging workflow in [fadogen/binaries](https://github.com/fadogen/binaries)
downloads an immutable revision of this repository and runs `composer install`
against that lockfile. It qualifies the final archive, publishes it and updates
Fadogen's existing `metadata-reverb.json` catalogue. Source or dependency changes
produce a new archive even when the Reverb version itself is unchanged.

Packaging never updates dependencies, generates an application key, migrates a
database, or publishes unmerged dependency changes. The checked-in `.env.example`
contains public local-development defaults; it must not contain real credentials.

For local validation:

```sh
cp .env.example .env
composer install
composer validate --strict
composer audit --locked --no-dev
php artisan test
```
