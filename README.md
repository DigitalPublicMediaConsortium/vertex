# Project Vertex

## Development

### Requirements

- [Lando](https://docs.lando.dev/basics/installation.html)
- [Docker Desktop](https://docs.docker.com/engine/install/)

### Considerations for macOS

#### VirtioFS

Docker Desktop on macOS is notoriously slow -- Docker Desktop 4.6 introduced a
new directory sharing feature **VirtioFS** that improves performance
dramatically. Follow the steps below to enable and use this feature:

1. Install the latest version of Docker Desktop (at least 4.6).
   - Lando supports very specific versions of Docker Desktop and may complain
     about this -- ignore the warnings.
2. Install the latest version of macOS (at least 12.5).
3. Open Docker Desktop -> Preferences -> General and select "VirtioFS" under
   "Choose file sharing implementation for your containers".
4. Restart Docker Desktop.

### Quick start

1. `lando start`
2. `lando reset`
3. Click the one time login link to log in.

## Drupal basics

### Drush

[Drush](https://www.drush.org/) is a command line tool for managing Drupal.
Execute `drush list` for a detailed list of all available commands. Some
important common commands are:

#### `drush cache:rebuild`

Rebuilds all of Drupal's caches.

#### `drush config:import`

Imports site configuration from the [`config`](/config) directory. Should be
used whenever pulling updated configuration from vcs.

#### `drush config:export`

Exports configuration from the active site to the [`config`](/config) directory.
Should be used whenever site configuration changes are made and meant to be
stored in vcs.

#### `drush php:cli`

Opens an interactive shell on the site.

#### `drush updatedb`

Applies any pending database updates.

### Directory and file structure

See [Understanding Drupal: Directory Structure](https://www.drupal.org/docs/understanding-drupal/directory-structure)
for detailed information about Drupal's core directory structure.

#### `config`

Contains exported site configuration in YAML format. The `default` directory
holds config to be applied for all environments. The `dev` directory holds
config that is only used for the development ("dev") environment. These
environments are defined by the [Configuration Split](https://www.drupal.org/project/config_split)
module.

#### `.lando*` files

See [Landofile](https://docs.lando.dev/core/v3/#landofile) for documentation
about the various Lando configuration files.

#### `.phpcs.xml.dist` and `.phpstan.neon.dist`

Configuration files for `phpcs` and `phpstan` code quality tools respectively.
Execute `composer lint` to run code quality checks on custom code.

#### `web/sites/default/services.yml`

Service configurations for the site. Of note: used to enabled CORS. See also
[Structure of a service file](https://www.drupal.org/docs/drupal-apis/services-and-dependency-injection/structure-of-a-service-file).

#### `web/sites/default/settings.php`

Committed default site settings for all environments.

#### `web/sites/default/settings.local.php`

Overrides and general development settings for local development.
