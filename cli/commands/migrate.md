---
layout: default
title: migrate
parent: Commands
grand_parent: CLI
---

# migrate
{: .no_toc }
Migrates all eligible migration scripts
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
----

The `migrate` command will find, [sort](/workflows/migrate.html#sorting) and migrate all 
[eligible migration scripts](/workflows/migrate.html#eligibility) to the [target](/concepts/target.html) database.

## Usage
```text
cinch migrate <project> [options]
```

## Arguments

| argument  | description  |
|-----------|--------------|
| `project` | project name |

## Options

| option                | default              | description                                        |
|-----------------------|----------------------|----------------------------------------------------|
| `--deployer=DEPLOYER` | current user         | User or application performing the deployment      |
| `--tag=TAG`           | ULID                 | Tag assigned to deployment                         |
| `--dry-run`           | off                  | Performs all actions without deploying             |
| `--env=ENV`           | environments.default | Sets the [environment](/concepts/environment.html) |
{% include global_options.md %}