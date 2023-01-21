---
layout: default
title: env:add
parent: Commands
grand_parent: CLI
---

# env:add
{: .no_toc }
Adds an environment
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
----

The `migrate:add` command adds an [environments](/concepts/environment.html) to a [project](/concepts/project.html).

## Usage
```text
cinch env:add <project> <name> <target_dsn> [options]
```

## Arguments

| argument     | description         |
|--------------|---------------------|
| `project`    | project name        |
| `name`       | environment name    |
| `target_dsn` | target database DSN |

## Options

| option                   | default        | description                                     |
|--------------------------|----------------|-------------------------------------------------|
| `-H, --history=DSN`      | $target_dsn    | History database DSN                            |
| `-s, --schema=NAME`      | cinch_$project | History schema name                             |
| `--table-prefix=PREFIX`  | (empty)        | History table name prefix                       |
| `--deploy-timeout=SECS`  | 10             | Timeout seconds for a deploy lock               |
| `-a, --auto-create=BOOL` | true           | Auto-create history schema if it does not exist |
{% include global_options.md %}