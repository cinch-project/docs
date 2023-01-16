---
layout: default
title: Concepts
nav_order: 4
has_children: true
---

# Project

A project is an organizational unit for your database changes: containing configuration, migrations,
hooks scripts, history, logs, etc. There can be many projects managed by a single cinch installation.

## Project Name

Each project must have a unique name: sales, products, etc. The name is typically named after the target database.
It can contain any unicode character between `\u0001-\uffff` but is limited to (mysql) 64 characters and
(postgresql) 63 bytes.

{: .note}
The cinch CLI uses the project name, with a `cinch_` prefix, as the history schema name.
For this reason, projects managed by the cinch CLI are limited to (mysql) 58 characters and (postgresql)
57 bytes.

