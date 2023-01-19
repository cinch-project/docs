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

The `create` command creates a new project. This includes creating the project configuration, migration store and 
history. A project is required before being able to manage a database target.

## Usage
```bash
cinch create <project> <target_dsn> [options]
```

{% comment %}

| -e, –env=NAME | The environment to use when executing the command. The default is `environments.default` from the project file.                                                                         |

## Usage
```bash
cinch create <project> <target_uri> [options]
```

### Arguments
All arguments are required.

| argument   | description                                                                                                                                                                                                |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| project    | The name of the project to create. Project names can contain any character between `U+0001..U+ffff` and must be UTF-8 encoded. MySQL is limited to 58 characters while PostgreSQL is 57 bytes [^name-len]. |
| target_uri | The URI of the target database.                                                                                                                                                                            |

[^name-len]: Each natively supports 6 more bytes or characters, but the cinch CLI adds a `cinch_` prefix to the history schema name.

{% endcomment %}