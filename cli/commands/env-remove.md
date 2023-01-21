---
layout: default
title: env:remove
parent: Commands
grand_parent: CLI
---

# env:remove
{: .no_toc }
Removes an environment
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
----

The `migrate:remove` command removes an [environment](/concepts/environment.html) from a [project](/concepts/project.html).

## Usage
```text
cinch env:remove <project> <name> [options]
```

## Arguments

| argument  | description                       |
|-----------|-----------------------------------|
| `project` | project name                      |
| `name`    | name of the environment to remove |

## Options

| option                     | default        | description                                |
|----------------------------|----------------|--------------------------------------------|
| `-D, --delete-history=DSN` | off            | Delete environment's history schema/tables |
{% include global_options.md %}