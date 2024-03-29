---
layout: default
title: env
parent: Commands
grand_parent: CLI
---

# env
{: .no_toc }
Lists all environments
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
----

The `env` command lists all [environments](/concepts/environment.html) for a [project](/concepts/project.html).

## Usage

```text
cinch env <project> [options]
```

## Arguments

| argument  | description  |
|-----------|--------------|
| `project` | project name |

## Options

| options | default | description |
|---------|---------|--|
{% include global_options.md %}

## Example
The project used for this example has two environments: `sales` and `dev`. 

{% include photo.html photo="env-output.png" alt="env command output" %}
