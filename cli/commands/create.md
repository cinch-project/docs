---
layout: default
title: create
parent: Commands
grand_parent: CLI
---

# create
{: .no_toc }
Creates a project
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
----

The `create` command creates a new [project](/concepts/project.html). This includes the project configuration, 
[migration store](/concepts/migration-store.html) and [history](/concepts/history.html). A project is required before 
being able to manage a database [target](/concepts/target.html).

## Usage
```text
cinch create <project> <target_dsn> [options]
```
## Arguments

| argument     | description         |
|--------------|---------------------|
| `project`    | project name        |
| `target_dsn` | target database DSN |

## Options

| option                   | default                  | description                                                          |
|--------------------------|--------------------------|----------------------------------------------------------------------|
| `-d, --description=DESC` | "$project project"       | Project description                                                  |
| `-H, --history=DSN`      | $target_dsn              | History database DSN                                                 |
| `-s, --schema=NAME`      | cinch_$project           | History schema name                                                  |
| `--table-prefix=PREFIX`  | (empty)                  | History table name prefix                                            |
| `--deploy-timeout=SECS`  | 10                       | Timeout seconds for a deploy lock                                    |
| `-a, --auto-create=BOOL` | true                     | Auto-create history schema if it does not exist                      |
| `-S, --store=DSN`        | "adapter=fs store_dir=." | Migration store DSN                                                  |
| `--env=ENV`              | $project                 | Sets the project's default [environment](/concepts/environment.html) |
{% include global_options.md %}

## Example

{% include photo.html photo="create-output.png" alt="create command output" %}